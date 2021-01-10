
Our simulation tools alternatives:
Scylla - Extensible and open source. Based on DESMO-J
Create a mapping function from bpmnsim to executable model
http://www.msc-les.org/proceedings/wams/2012/WAMS2012_125.pdf
jBPM - free and open source. Very strong track record
BIMP - free academic license but not open source


Sunday
- finish section of DES basics
- write section on bpmn
- why not use other formalism that has already been proven, such as cpn?
 - see the master tesis for arguments 
- write section on why modeling using bpmn is beneficial
- write section on how bpmn is not very well suited for modeling simulations
  - see the dedicated paper on simulation and bpmn + the master thesis
- present an overview of other popular simulation solutions
  - what options do we have and what are our requirements

test out jbpm 
try to run a simulation in jbpm
fint the request and start to reverse engineer

use jbpm simulation engine or find some work that translated bpmn to cpn and use this instead?


Todo:
make the simulatione engine available via a web server. This way it can be included in future research projects and products
There are currently many different simulation engines. We make two distinctions.

Business process simulation engines and generic simulation engines. This separation is however not very clear. Generic simulation engines could for exampe be CPN or some other java bases engine such as DESMO-J.

Some BPS specific implementations could be jBPM, but this uses DESMO-J as its simulation engine. So its really just doint the model transformation for you.

My options are:
 - extend jBPM simulation to support the latest bpsim specification. Currently supports v.1
 - create a wrapper for the scylla project that supports the latest bpsim spec. They currently have their own format which is very weird.
 - somehow manage to translate bpsim to cpn. All papers that i have found that address this translation fail to actually show any working implementations. They all describe applications and even show pictures, but fail to upload the code anywhere. I would have to either beg for a implementation or try to reimplement it myself.

Leaning towards first trying to extend jBPM.

My requirement being that the simulation engine is fully open source. New advances cannot be made if the application is not fully available for scrutiny.




options
1. use jbpm simulation, extend it to bpsim 2.0 and wrap it in a web server
2. implement bpism 2.0 in the scylla project and wrap in sever
3. translate bpsim or bpmn 2.0 to cpn 



