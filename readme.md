# readme
Repo containing the docker-compose file

## Run, pressuming dokcer-compose.yml is in cwd
``` shell
docker-compose up
```
## Concepts
The functionality offerent by the services tie into the concepts and aims that we wish to fulfill. 
### Mining different perspectives
The simulation model can be understood as a executable model that is comprised of a series of different perspectives. In essence a layered cake.

![](./process_cake.svg)

#### Control flow perspecive
This can be understood as the base layer. Here we discover a process model from the event log. This can be represneted in different formats, such as petri-net, process tree, BPMN model, etc. While these representations are vastly different, they encode the same information. The benefit of petri-nets being its formalism, and the benefit of BPMN that its easy to understand. 

The discovered model is in essence just a series of nodes and arcs. The model specicically encode how these relate to each other and therefore the process *flow*. Specifically, we have places, transitions, arcs. In the event where transitions have multiple incoming out outgoing arcs then these are called splits. 

##### Representational bias and model validity
The process model is first mined by use of the inductive miner. While there are many diferent mining algorithms, such as the alpha miner and heuristic miner, the inductive miner has been proven superior. 

There have been written works that cover the upsides and downsides of different mining algorithms. See [this work](https://ieeexplore.ieee.org/document/8368306/). While there is no single algorithms that is perfect for every usecase, the inductive miner was choosen because of the quality of its resulting model (see section of qulity dimensions) and also because it guarantees soudness.

*The results of the empirical evaluation show that methods that seek to produce block-structured process models (Inductive Miner and Evolutionary Tree Miner) achieve the best performance in terms of fitness or precision, and com- plexity.*

There are three variants of the inductive miner. The base verison is used in this project, while there exists version that are tailored to handling incomplete traces and infrequent behavior. The aformentioned work is suggested for further reading.

The validity or quality of a model is ensured by calculating metrics on the four quality dimension. 


## Services
### GUI

### Discovery
Process mining service built on Flask and PM4PY. Warps some needed functinoality such as control flow discovery, role discovery, model transoformation, etc.
Please see the swagger.yaml file in the repo for available endpoints.
1. #### /doc
   1. for rendering the swagger documentation in swagger UI
2. #### /discover
   1. for discovering process model from .xes log
   2. uses the inductive miner to produce process tree
3. #### /translate
   1. for translating process tree to BPMN 2.0 model
4. #### /evaluate
   1. for performing model quality assessment. Supports the following:
      1. **Replay Fitness**  
        *The calculation of the replay fitness aim to calculate how much of the behavior in the log is admitted by the process model. We propose two methods to calculate replay fitness, based on token-based replay and alignments respectively.*
         1. **Token-based replay**  
         ( Berti, Alessandro, and Wil MP van der Aalst. "Reviving Token-based Replay: Increasing Speed While Improving Diagnostics." ATAED@ Petri Nets/ACSD. 2019. )
         1. **Alignment-based replay**  
         **need to locate source on this**
      2. **Precision**  
      *a model is precise if it does not allow for too much behaviour. It would likely be possible to construct a simple petri net that had great fitness and is very simple, but this would have terrible precision as it would in essence allow for too much behaviour. A model that is not precise is underfitting, which is when the model over-generalizes the example behaviour in the log, i.e allows for behaviour that are very different from those present in the log.*
         1. **ETConformance**   
         (Muñoz-Gama, Jorge, and Josep Carmona. "A fresh look at precision in process conformance." International Conference on Business Process Management. Springer, Berlin, Heidelberg, 2010)
         1. **Align-ETConformance**  
         (Adriansyah, Arya, et al. "Measuring precision of modeled behavior." Information systems and e-Business Management 13.1 (2015): 37-67.)
      1. **Generalization**  
        *A model should generalize and not just be limited to the behaviour seen in the log. A model that does not generalize is overfitting, which is the problem that occurs when the model is tailored to the behaviour seen in the log, when it is obvious that this is just example behaviour.*  
      (Buijs, Joos CAM, Boudewijn F. van Dongen, and Wil MP van der Aalst. "Quality dimensions in process discovery: The importance of fitness, precision, generalization and simplicity." International Journal of Cooperative Information Systems 23.01 (2014): 1440001. )
      1. **Simplicity**  
      *with high fitness often comes high complexity, which is naturally unwanted. The simplest model that can explain the behaviour seen in the log is the best model, i.e Occams razor*
      ( Blum, Fabian Rojas. Metrics in process discovery. Technical Report TR/DCC-2015-6, Computer Science Department, University of Chile, 2015. )
5. #### /rolediscovery
   1. For discovering role. A role can be understood as a set of activities that are executed by  a similar (multi)set of resources. 
   2. Can help with understanding which activities are executed by what roles
   3. Initiallye each activity is related to a unique role. After discovering the roles we can merge similar roles and create a set that is more representative of the actual roles.
   4. Article: Burattin, Andrea, Alessandro Sperduti, and Marco Veluscek. “Business models enhancement through discovery of roles.” 2013 IEEE Symposium on Computational Intelligence and Data Mining (CIDM). IEEE, 2013. 
6.  ##### /decisonpointdiscovery
    1.  For performing decision mining. Used to retrieve the features of the cases that go in the different directions. Allows for calculating a decision tree that explains the decisions. 
    2.  Performed by specifying waht decision poin to mine for. Then we get back a dataframe with the features of all traces that followed a specific branch. 
7.  #### /performanceanalysis



