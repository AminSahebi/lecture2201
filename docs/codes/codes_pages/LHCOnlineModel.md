# LHCOnlineModel

## Short description

 The beam based model, aka online model, extends the (ideal) LHC accelerator model by including measured parameters of the machine. 

* Orbit
* Optics (beta beating)
* Applied corrections (tune, orbit corrector magnets)
* Powering errors
* Magnetic field deviations (new implementation of WISE as Java app)
* Alignment errors

Such model is more accurate and it provides higher predictive power. It allows calculating, for example, 

* Feed-down effects due to imperfect orbit
* Modification of global parameters due to beta function beating or alignment errors

The project aims at providing tools that allow  

* Easy access to more accurate and up-to-date beam parameters. The principal example is the aperture meter application that displays available aperture along the machine taking into account the measured orbit and beta beating.
* Simulating more accurately the beam behavior upon a knob or parameter change.
* Easy comparison between the model and the available measurements. Facilitating data analysis throughout all different machine configurations hopefully lets understand the sources of the discrepancies and leads to even more accurate machine model.

## Web resources

 <ul><li>  Web page:     <a href="http://lhcmodel.web.cern.ch/lhcmodel/" target="_blank">http://lhcmodel.web.cern.ch/lhcmodel/</a>
</li> <li> Source codes: <ul>
<li> <a href="https://svnweb.cern.ch/cern/wsvn/lhcmodel" target="_blank">https://svnweb.cern.ch/cern/wsvn/lhcmodel</a>
</li> <li> <a href="https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/accsoft/om/" target="_blank">https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/accsoft/om/</a>
</li> <li> <a href="https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-extractor/" target="_blank">https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-extractor/</a>
</li> <li> <a href="https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-wise-errorestimators/" target="_blank">https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-wise-errorestimators/</a>
</li> <li> <a href="https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-wise-ui/" target="_blank">https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-wise-ui/</a>
</li> <li> <a href="https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-fidel-extractor/" target="_blank">https://svnweb.cern.ch/cern/wsvn/acc-co/trunk/lhc/lhc-model-fidel-extractor/</a>
</li></ul>
</li></ul>

 <ul><li> Wiki pages:      <a href="https://wikis.cern.ch/display/OnlineModel/Home" target="_blank">https://wikis.cern.ch/display/OnlineModel/Home</a>
</li></ul>

## Technical information

[Provide the following information] 

* Programming Languages used for implementation: 
  
    - Java
    - Python
  
  
  
* Parallelization strategy: 
  
    - None
  
  
  
* Operating systems: 
  
    - Linux, inside cern only, and in some cases on technical network only
  
  
  
* Other prerequisites:

## Other information

 

* __Developed by:__ \[Piotr Skowronski\] [
  ](mailto:piotr.skowronski@cernNOSPAMPLEASE.ch)
* __License:__ Default CERN
* __Contact persons:__ Piotr Skowronski, Tobias Persson
* Being actively developed and supported: Yes

 
