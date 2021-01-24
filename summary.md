# My current project scope
Simulation as a stretegic tool to explore different process alternatives and outcomes. Allows for efficient and inexpensive exploration.
While there are many commercial offerings that offer facilities for business process simulation there are no open source offerings with the same featureset 
or of similar availability. This project details the creation and design choices of a working prototype that is used for creating simulation models that run on CPN Tools. The process of creating, simulating, and analyzing the reusults has all been added to the same workflow as offered by the application, whilst also being built in such a way tht allows for individual reuse of the large components for future research.
 

Summarized list of issues with current tools:
 - Lack for formal validation in commercial tools.
    - BPMN has poor semantics, therefore not possible to use it directly as a simulation model
    - Commercial tools offer the simulation of BPMN models, this implies some funky transformations.
    - Without the option to formally validate the simulation model then it is arguably difficult to trust. 
    - Commercial tools likely perform some propriatery and subjective model transformation from their representational format to the simulation enine input format.
    - There are many works that address the shortcomings of existing offerings. These shortcomings will be addresses in due time.
 - The "base case" simulation model should be proven accurate before new alternatives can be explored
    - From process mining we have learned that the "ideal" process and "real" process can be very diverging.
    - By use of process mining techniques we are able to discover the real process from a process log. (The discovered process is only representative of its input log)
    - 

----

Simulations are executed by use of simulation models. The simulation engine selected for this work is CPN Tools. CPN tools allows for the execution of petri coloured petri nets, which have formal semantics. However, creating such simulation models in the CPN formalism is not trivial and requires expert knowledge. 

Provided that the this work is in the context of business process simulation, we are of course interested in the modeling of business processes by use of BPMN. However, the BPMN notation cannot be used as input for out simulation engine due to the poor semantics of BPMN. There is however a core subset of elements which have simple mappings from BPMN to petri nets and with this very limied set of elements the model is far easier to read by non-experts.

This project therefore creates a tool for the initial mining and creation of BPMN models for use as simulation models in CPN tools. There have been many works that explore the exact issues of using BPMN as a notation for formal modeling. This work expands upon the great effort presented in https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.175.6944&rep=rep1&type=pdf where the author details the process of simulating business processes in CPN and also offers a description of a model transformation from BPMN to CPN. This project directly employt this described model transformation in practice to create CPN simulation models.


The meta-model as described in the previous work will be presented next.
**Business process simulation model**  
The meta-model captures the data required for simulating a business process. The model extends the meta-model of BPMN by attaching simulation parameters to tasks, events, and gateways. The model is simple and holds only basic simulation objects. The model is rather incomplete and uses only basic objects required to set up the simulation.

A simulation workflow can be understood as being comprised of the following steps@.
 - Model resources, timetables, etc
 - Model the process
 - Attach simulation data to the task, probabilities to gateways
 - Create and aset up simulation profile
 - Simulate the process and analyze the results
> The proposed application aims to gather these steps in one single workflow. Current open soruce practice requires the use of different tools and manual transformations. This makes the overall workflow very slow.

The meta model is comprised of three parts:
    - Classes that hold basic types such as resoruces, timetables, roles, etc
    - Classes to attach metadata to tasks and gateways
    - Classes to hold simulation profiles



--Notes
Create simulation model
    - 