# Guidelines for code distribution and maintenance in ABP

## Minimal requirements

Software projects within ABP should comply with the following basic guidelines:

1. The source code should be hosted in an online **git repository**. 
    -  Common choices are:
        - The CERN GitLab platform (https://gitlab.cern.ch). Project hosted there can be public, restricted to people with a CERN account, or to smaller groups. Contributions (pull requests) can be submitted only by people having a CERN account.
        - The GitHub platform (http://github.com), which is used by millions of developers in thr world and hosts  several major open source projects (e.g. linux kernel, python). The source code for projects hosted on GitHub needs to be public, as CERN does not provide GitHub pro accounts. Contributions (pull requests) can be submitted by anybody.
    - Production code should not be hosted in personal GitLab or GitHub profiles. GitHub organizations or GitLab groups should be used instead.
    - More information about the usage of git for collaborative code development can be found [here](gitinfo.md).  
 2. One or more **"ready-to-run" examples** should be made available in the repository, illustrating the main features of the code.
    - Please make sure that the example are still updated and working when making modifications to the code!
 3. A simple **"Getting started guide"** should be made available, illustrating how to install the code and run an example. This can be provided as:
    - A simple README file within the repository in text or markdown (both GitLab and GitHub render mardkown files).
    - For larger documentation an MkDocs site like the present one can be used (instructions can be found [here](mkdocs_site.md)).
    - Alternatively the GiHub wiki space associated with the repository can be used.

A general paper describing a set of good computing practices that every researcher can adopt, regardless of their current level of computational skill is ["Good enough practices in scientific computing"](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005510).

## Python packages

Python tools should follow a standardized package structure.

 * More details and a template package can be found in the [dedicated section](python_packages.md).

## Versioning

It is recommended to use version numbers associated to changes in the code.

   - A convenient choice is to version numbers in the form X.Y.Z (e.g. v2.2.1) where X is the major version number (used only for major changes, typically backward incompatible), Y is the minor number, Z is used for bug-fixes and patches.
   - Year based version numbers e.g. 2021.1.3 are a valid alternative.

Versions should be associated to releases in GitHub or GitLab, making it easy to retrieve previous versions.

## Testing

The examples discussed above can provide a first-level set of checks to validate new versions.

Automatic testing (e.g. [unit testing](https://en.wikipedia.org/wiki/Unit_testing)) and [continuos integration](https://docs.github.com/en/free-pro-team@latest/actions/guides/about-continuous-integration) are strongly encouraged. 


