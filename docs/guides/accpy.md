# Acc-Py Information

## Creating Virtual Environments

This is a page copying part of the content of 

https://wikis.cern.ch/display/ACCPY/Getting+started+with+Acc-Py

To access it from home you can use [`sshuttle`](http://abpcomputing.web.cern.ch/guides/sshtunnel/).

In order to run your own application in the Acc-Py environment, it is likely you will want to install some specific packages which are suited to the task at hand. 

The most appropriate way to customise your Python environment is to use Python virtual environments. These are essentially a directory in which you have permission to install Python packages using the Python package manager, and which has its own Python executable and associated files.

To enable it for the lifetime of your current shell a few key environment variables must be set by sourcing the setup script (from the technical network)

```
source /acc/local/share/python/acc-py/pro/setup.sh
```

Then you can create your virtual environment with a command similar to
```
acc-py venv ~/venv/mypy
```

and you can activate it by
```
source ~/venv/mypy/bin/activate
```

Now that you have a full Python environment with write permission, you can install Python packages into it:
```
python -m pip install pyarrow
```

That's it.

## Acc-Py Repository Packages and External Tools

Recently, GPN functionality Python packages such as `pyjapc`, `cmmnbuild-dep-manager`, `pjlsa`, `jpype1` and `pytimber` have been made installable from the `acc-py` repo only, which requires to install from inside the CERN GPN, and cannot be fetched from `PyPI`.
However, some python projects need to reconcile using functionality from these packages while also being installable from outside the CERN GPN - to, say, be accessible to collaborators. These packages will find their CI/CD setup failing, and will also be faced with the impossibility of deploying to `PyPI`.

As there are no plans to make packages from the `acc-py` repository installable from outside the CERN GPN in the foreseeable future, the current workaround is to declare these packages as optional dependencies (by creating [an extra in your `setup.py` or `pyproject.toml`](https://setuptools.readthedocs.io/en/latest/userguide/dependency_management.html#optional-dependencies){target=_blank}), and to gate or mock their import whenever needed. 
This comes with the caveat that `PyPI` will only accept the deployment of a package if its dependencies are also registered on `PyPI`, so the workaround necessitates that the maintainers of `pytimber`, `pjlsa` or any python package deployed on the `acc-py` repository keep a shallow clone of their packages on `PyPI`. 

It is also recommended to keep shallow clones for **security reasons**, as it would be easy for any attacker to register a package under the same name on `PyPI` containing malicious code.
Depending on the version number or the accessibility of the `acc-py` repository, this malware would then be installed instead of the `acc-py` package.
For further reading, see [this interesting article on medium.com](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610){target=_blank} and [this article about `PyPI` removing malicious packages](https://www.theregister.com/2021/03/02/python_pypi_purges/).

An example of the mocking, as implemented in `omc3`, can be seen below:
```python
import importlib


class CERNNetworkMockPackage:
    """
    Mock class to raise an error if the desired package functionality is called when the package is not
    actually installed. Designed for packages installable only from inside the CERN network,
    that are declared as an extra dependency.
    """
    def __init__(self, name: str):
        self.name = name

    def __getattr__(self, item):
        raise ImportError(
            f"The '{self.name}' package does not seem to be installed but is needed for this function. "
            "Install it with the 'cern' extra dependency, which requires to be on the CERN network and to "
            "install from the acc-py package index. Refer to the documentation for more information."
        )


def cern_network_import(package: str):
    """
    Convenience function to try and import packages only available (and installable) on the CERN network.
    If installed, the module is returned, otherwise a mock class is returned, which will raise an
    insightful ``ImportError`` on attempted use.
    Args:
        package (str): name of the package to try and import.
    """
    try:
        return importlib.import_module(package)
    except ImportError:
        return CERNNetworkMockPackage(package)
```

The usage is then:
```python
from your.mock.module import cern_network_import
pytimber = cern_network_import("pytimber")
db = pytimber.LoggingDB(source="nxcals")  # will raise if pytimber not installed
```
