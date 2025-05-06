# Migració de CloudSim G4 a CloudSim G7

**CloudSim** és un framework de codi obert per modelar, simular i experimentar amb entorns de computació en núvol (cloud computing). Permet als investigadors i desenvolupadors provar estratègies de gestió de recursos, planificació de tasques i rendiment de centres de dades sense necessitat d'infraestructura física real.

---

## 📌 Objectiu del projecte

Aquest projecte parteix de la tesis doctoral d'un ex-alumne de la UdL, Sergi Vila Almenara, qui va realitzar modificacions al projecte open-source CloudSim 4.0 per tal d'incorporar-li noves funcionalitats, tècniques, càrregues de treball, algoritmes i eines.

L'anàlisi final de resultats mostra com les mètriques analitzades obtenen beneficis substancials gràcies a l'exploració polivalent de l'espai de cerca en el cas d'entorns estàtics i l'observació acurada i adaptada de les dades disponibles en entorns dinàmics per a una millor presa de decisions.

Actualment, el software oficial de CloudSim es troba en la versió 7.0 i ha evolucionat notablement des de la versió 4.0, optimitzant el codi existent i afegint noves funcionalitats.

L'objectiu d'aquest projecte és estudiar detalladament les diferències entre el CloudSim 4.0 i la versió del Sergi Almenara, per tal de poder crear una versió del CloudSim 7.0 millorada, amb les funcionalitats que va afegir l'ex-alumne i que encara no es troben implementades en aquesta nova versió.

---

## 🧪 Comparació entre CloudSim 4.0 i CloudSim-sergi

El cloudSim 4.0 presenta la següent estructura de directoris:

```cloudsim-4.0/
├── modules/
│   ├── cloudsim/
│   │   ├── src/
│   │   │   └── main/
│   │   │       └── java/
│   │   │           └── org/
│   │   │               └── cloudbus/
│   │   │                   └── cloudsim/
│   │   │                       ├── core/
│   │   │                       ├── network/
│   │   │                       ├── power/
│   │   │                       ├── resources/
│   │   │                       ├── schedulers/
│   │   │                       └── util/
│   │   └── pom.xml
│   └── cloudsim-examples/
│       ├── src/
│       │   └── main/
│       │       └── java/
│       │           └── org/
│       │               └── cloudbus/
│       │                   └── cloudsim/
│       │                       └── examples/
│       └── pom.xml
├── pom.xml
└── README.md
```

En un primer cop d'ull, podem veure que el Sergi va copiar la carpeta ```modules/cloudsim/src/main/java/org/cloudbus/cloudsim/``` del projecte original de CloudSim G4 i la va ubicar en la direcció ```cloud-sergi/src/main/java/org/cloudbus/cloudsim/``` del seu propi projecte

```cloud-sergi/
├── cloudsim
│   ├── output
│   │   ├── json
│   │   └── log
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   ├── PSO
│   │   │   │   ├── PSOMO
│   │   │   │   ├── PSOMO2
│   │   │   │   ├── genetic
│   │   │   │   ├── geneticOrder
│   │   │   │   ├── geneticsimulator
│   │   │   │   ├── gridsim
│   │   │   │   ├── hybridTechnique
│   │   │   │   ├── jmetal54
│   │   │   │   ├── org
│   │   │   │   │   └── cloudbus
│   │   │   │   │       └── cloudsim
│   │   │   │   │           ├── container
│   │   │   │   │           │   ├── containerPlacementPolicies
│   │   │   │   │           │   ├── containerProvisioners
│   │   │   │   │           │   ├── containerSelectionPolicies
│   │   │   │   │           │   ├── containerVmProvisioners
│   │   │   │   │           │   ├── core
│   │   │   │   │           │   ├── hostSelectionPolicies
│   │   │   │   │           │   ├── lists
│   │   │   │   │           │   ├── resourceAllocatorMigrationEnabled
│   │   │   │   │           │   ├── resourceAllocators
│   │   │   │   │           │   ├── schedulers
│   │   │   │   │           │   ├── utils
│   │   │   │   │           │   └── vmSelectionPolicies
│   │   │   │   │           ├── core
│   │   │   │   │           │   └── predicates
│   │   │   │   │           ├── distributions
│   │   │   │   │           ├── examples
│   │   │   │   │           │   ├── container
│   │   │   │   │           │   ├── network
│   │   │   │   │           │   │   └── datacenter
│   │   │   │   │           │   └── power
│   │   │   │   │           │       ├── planetlab
│   │   │   │   │           │       └── random
│   │   │   │   │           ├── lists
│   │   │   │   │           ├── network
│   │   │   │   │           │   └── datacenter
│   │   │   │   │           ├── power
│   │   │   │   │           │   ├── lists
│   │   │   │   │           │   └── models
│   │   │   │   │           ├── provisioners
│   │   │   │   │           └── util
│   │   │   │   ├── shedulers
│   │   │   │   │   └── energy
│   │   │   │   ├── simulator
│   │   │   │   ├── svila
│   │   │   │   │   ├── Brokers
│   │   │   │   │   ├── CustomCloudSimulator
│   │   │   │   │   │   └── events
│   │   │   │   │   ├── GridCloudBridge
│   │   │   │   │   ├── WorkloadGenerator
│   │   │   │   │   ├── algorithms
│   │   │   │   │   ├── cloudMOGA
│   │   │   │   │   ├── containersExperiment
│   │   │   │   │   ├── evaluation
│   │   │   │   │   ├── mann
│   │   │   │   │   ├── mesd
│   │   │   │   │   ├── planetlabNetwork
│   │   │   │   │   │   ├── Executers
│   │   │   │   │   │   ├── correlation
│   │   │   │   │   │   │   └── techniques
│   │   │   │   │   │   ├── generators
│   │   │   │   │   │   ├── optimizeAllocation
│   │   │   │   │   │   └── results
│   │   │   │   │   ├── policiesFactories
│   │   │   │   │   ├── policiesHostOverSaturation
│   │   │   │   │   ├── policiesHostUnderUtilisation
│   │   │   │   │   ├── policiesVmMigration
│   │   │   │   │   ├── policiesVmOptimizer
│   │   │   │   │   ├── policiesVmSelection
│   │   │   │   │   ├── serialization
│   │   │   │   │   ├── staticAllocation
│   │   │   │   │   │   └── schedulingTechniques
│   │   │   │   │   │       ├── ACO
│   │   │   │   │   │       ├── DE
│   │   │   │   │   │       └── extra
│   │   │   │   │   └── vmOptimizerFix
│   │   │   │   ├── system
│   │   │   │   │   ├── eaclustersim
│   │   │   │   │   └── jobs
│   │   │   │   ├── ut
│   │   │   │   └── util
│   │   │   └── resources
│   │   └── test
│   ├── target

│   │   │   │   ├── resFailure
│   │   │   │   └── util
│   │   │   ├── hybridTechnique
│   │   │   ├── jmetal54
│   │   │   ├── org
│   │   │   │   └── cloudbus
│   │   │   │       └── cloudsim
│   │   │   │           ├── container
│   │   │   │           │   ├── containerPlacementPolicies
│   │   │   │           │   ├── containerProvisioners
│   │   │   │           │   ├── containerSelectionPolicies
│   │   │   │           │   ├── containerVmProvisioners
│   │   │   │           │   ├── core
│   │   │   │           │   ├── hostSelectionPolicies
│   │   │   │           │   ├── lists
│   │   │   │           │   ├── resourceAllocatorMigrationEnabled
│   │   │   │           │   ├── resourceAllocators
│   │   │   │           │   ├── schedulers
│   │   │   │           │   ├── utils
│   │   │   │           │   └── vmSelectionPolicies
│   │   │   │           ├── core
│   │   │   │           │   └── predicates
│   │   │   │           ├── distributions
│   │   │   │           ├── examples
│   │   │   │           │   ├── container
│   │   │   │           │   ├── network
│   │   │   │           │   │   └── datacenter
│   │   │   │           │   └── power
│   │   │   │           │       ├── planetlab
│   │   │   │           │       └── random
│   │   │   │           ├── lists
│   │   │   │           ├── network
│   │   │   │           │   └── datacenter
│   │   │   │           ├── power
│   │   │   │           │   ├── lists
│   │   │   │           │   └── models
│   │   │   │           ├── provisioners
│   │   │   │           └── util
│   │   │   ├── shedulers
│   │   │   │   └── energy
│   │   │   ├── simulator
│   │   │   ├── svila
│   │   │   │   ├── Brokers
│   │   │   │   ├── CustomCloudSimulator
│   │   │   │   │   └── events
│   │   │   │   ├── GridCloudBridge
│   │   │   │   ├── WorkloadGenerator
│   │   │   │   ├── algorithms
│   │   │   │   ├── cloudMOGA
│   │   │   │   ├── containersExperiment
│   │   │   │   ├── evaluation
│   │   │   │   ├── mann
│   │   │   │   ├── mesd
│   │   │   │   └── staticAllocation
│   │   │   │       └── schedulingTechniques
│   │   │   │           ├── ACO
│   │   │   │           ├── DE
│   │   │   │           └── extra
│   │   │   ├── system
│   │   │   │   ├── eaclustersim
│   │   │   │   └── jobs
│   │   │   ├── ut
│   │   │   └── util
│   │   └── test-classes
│   │       └── org
│   │           └── cloudbus
│   │               └── cloudsim
│   │                   ├── lists
│   │                   ├── power
│   │                   │   └── models
│   │                   ├── provisioners
│   │                   └── util
│   └── ~
│       └── Results
│           ├── ContainerMigration
│           │   ├── ContainerCloudSimExample-1
│           │   ├── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_Cor_FirstFit_80.0
│           │   └── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_MaxUsage_MostFull_80.0
│           ├── EnergyConsumption
│           │   ├── ContainerCloudSimExample-1
│           │   ├── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_Cor_FirstFit_80.0
│           │   └── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_MaxUsage_MostFull_80.0
│           ├── NewlyCreatedVms
│           │   ├── ContainerCloudSimExample-1
│           │   ├── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_Cor_FirstFit_80.0
│           │   └── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_MaxUsage_MostFull_80.0
│           ├── log
│           │   └── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_MaxUsage_MostFull_80.0
│           ├── stats
│           ├── time_before_host_shutdown
│           │   └── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_Cor_FirstFit_80.0
│           └── time_before_vm_migration
│               └── FirstFit_MSThreshold-Under_0.80_0.70_VmMaxC_Cor_FirstFit_80.0
├── jmetal
│   ├── jmetal-algorithm
│   │   └── src
│   │       ├── main
│   │       │   ├── java
│   │       │   │   └── org
│   │       │   │       └── uma
│   │       │   │           └── jmetal54
│   │       │   │               └── algorithm
│   │       │   │                   ├── multiobjective
│   │       │   │                   │   ├── abyss
│   │       │   │                   │   │   └── util
│   │       │   │                   │   ├── cellde
│   │       │   │                   │   ├── dmopso
│   │       │   │                   │   ├── gde3
│   │       │   │                   │   ├── gwasfga
│   │       │   │                   │   │   └── util
│   │       │   │                   │   ├── ibea
│   │       │   │                   │   ├── mocell
│   │       │   │                   │   ├── mochc
│   │       │   │                   │   ├── moead
│   │       │   │                   │   │   └── util
│   │       │   │                   │   ├── mombi
│   │       │   │                   │   │   └── util
│   │       │   │                   │   ├── nsgaii
│   │       │   │                   │   ├── nsgaiii
│   │       │   │                   │   │   └── util
│   │       │   │                   │   ├── omopso
│   │       │   │                   │   ├── paes
│   │       │   │                   │   ├── pesa2
│   │       │   │                   │   │   └── util
│   │       │   │                   │   ├── randomsearch
│   │       │   │                   │   ├── rnsgaii
│   │       │   │                   │   │   └── util
│   │       │   │                   │   ├── smpso
│   │       │   │                   │   ├── smsemoa
│   │       │   │                   │   ├── spea2
│   │       │   │                   │   │   └── util
│   │       │   │                   │   └── wasfga
│   │       │   │                   │       └── util
│   │       │   │                   └── singleobjective
│   │       │   │                       ├── coralreefsoptimization
│   │       │   │                       ├── differentialevolution
│   │       │   │                       ├── evolutionstrategy
│   │       │   │                       │   └── util
│   │       │   │                       ├── geneticalgorithm
│   │       │   │                       └── particleswarmoptimization
│   │       │   └── resources
│   │       │       ├── MOEAD_Weights
│   │       │       ├── cec2005CompetitionResources
│   │       │       │   ├── supportData
│   │       │       │   └── testData
│   │       │       ├── mombi2-weights
│   │       │       │   └── weight
│   │       │       │       ├── gecco
│   │       │       │       └── many_objective
│   │       │       └── tspInstances
│   │       └── test
│   │           ├── java
│   │           │   └── org
│   │           │       └── uma
│   │           │           └── jmetal
│   │           │               └── algorithm
│   │           │                   ├── multiobjective
│   │           │                   │   ├── abyss
│   │           │                   │   ├── dmopso
│   │           │                   │   ├── gde3
│   │           │                   │   ├── mocell
│   │           │                   │   ├── mombi2
│   │           │                   │   ├── nsgaii
│   │           │                   │   ├── omopso
│   │           │                   │   ├── smpso
│   │           │                   │   ├── smsemoa
│   │           │                   │   └── wasfga
│   │           │                   └── singleobjective
│   │           │                       ├── differentialevolution
│   │           │                       └── geneticalgorithm
│   │           └── resources
│   │               ├── MOEAD_Weights
│   │               ├── pareto_fronts
│   │               └── referenceFronts
│   ├── jmetal-core
│   │   └── src
│   │       ├── main
│   │       │   ├── java
│   │       │   │   └── org
│   │       │   │       └── uma
│   │       │   │           └── jmetal54
│   │       │   │               ├── algorithm
│   │       │   │               │   └── impl
│   │       │   │               ├── measure
│   │       │   │               │   └── impl
│   │       │   │               ├── operator
│   │       │   │               │   └── impl
│   │       │   │               │       ├── crossover
│   │       │   │               │       ├── localsearch
│   │       │   │               │       ├── mutation
│   │       │   │               │       └── selection
│   │       │   │               ├── problem
│   │       │   │               │   └── impl
│   │       │   │               ├── qualityindicator
│   │       │   │               │   └── impl
│   │       │   │               │       └── hypervolume
│   │       │   │               │           └── util
│   │       │   │               ├── solution
│   │       │   │               │   ├── impl
│   │       │   │               │   └── util
│   │       │   │               └── util
│   │       │   │                   ├── archive
│   │       │   │                   │   └── impl
│   │       │   │                   ├── binarySet
│   │       │   │                   ├── comparator
│   │       │   │                   │   └── impl
│   │       │   │                   ├── chartcontainer
│   │       │   │                   ├── distance
│   │       │   │                   │   └── impl
│   │       │   │                   ├── evaluator
│   │       │   │                   │   └── impl
│   │       │   │                   ├── experiment
│   │       │   │                   │   ├── component
│   │       │   │                   │   └── util
│   │       │   │                   ├── extremevalues
│   │       │   │                   │   └── impl
│   │       │   │                   ├── fileinput
│   │       │   │                   │   └── util
│   │       │   │                   ├── fileoutput
│   │       │   │                   │   └── impl
│   │       │   │                   ├── front
│   │       │   │                   │   ├── imp
│   │       │   │                   │   └── util
│   │       │   │                   ├── naming
│   │       │   │                   │   └── impl
│   │       │   │                   ├── neighborhood
│   │       │   │                   │   ├── impl
│   │       │   │                   │   └── util
│   │       │   │                   ├── point
│   │       │   │                   │   ├── impl
│   │       │   │                   │   └── util
│   │       │   │                   │       ├── comparator
│   │       │   │                   │       └── distance
│   │       │   │                   ├── pseudorandom
│   │       │   │                   │   └── impl
│   │       │   │                   ├── referencePoint
│   │       │   │                   │   └── impl
│   │       │   │                   └── solutionattribute
│   │       │   │                       └── impl
│   │       │   └── resources
│   │       │       ├── MOEAD_Weights
│   │       │       ├── cec2005CompetitionResources
│   │       │       │   ├── supportData
│   │       │       │   └── testData
│   │       │       ├── mombi2-weights
│   │       │       │   └── weight
│   │       │       │       ├── gecco
│   │       │       │       └── many_objective
│   │       │       ├── pareto_fronts
│   │       │       └── tspInstances
│   │       └── test
│   │           ├── java
│   │           │   └── org
│   │           │       └── uma
│   │           │           └── jmetal
│   │           │               ├── measure
│   │           │               │   └── impl
│   │           │               ├── operator
│   │           │               │   └── impl
│   │           │               │       ├── crossover
│   │           │               │       ├── localsearch
│   │           │               │       ├── mutation
│   │           │               │       └── selection
│   │           │               ├── qualityindicator
│   │           │               │   └── impl
│   │           │               │       └── hypervolume
│   │           │               ├── referencePoint
│   │           │               │   └── impl
│   │           │               ├── solution
│   │           │               │   ├── impl
│   │           │               │   └── util
│   │           │               └── util
│   │           │                   ├── archive
│   │           │                   │   └── impl
│   │           │                   ├── comparator
│   │           │                   ├── distance
│   │           │                   │   └── impl
│   │           │                   ├── front
│   │           │                   │   ├── imp
│   │           │                   │   └── util
│   │           │                   ├── naming
│   │           │                   │   └── impl
│   │           │                   ├── neighborhood
│   │           │                   │   ├── impl
│   │           │                   │   └── util
│   │           │                   ├── point
│   │           │                   │   ├── impl
│   │           │                   │   └── util
│   │           │                   ├── pseudorandom
│   │           │                   │   └── impl
│   │           │                   └── solutionattribute
│   │           │                       └── impl
│   │           └── resources
│   │               ├── MOEAD_Weights
│   │               ├── arrayFront
│   │               ├── lambda
│   │               └── pareto_fronts
│   ├── jmetal-exec
│   │   └── src
│   │       └── main
│   │           └── java
│   │               └── org
│   │                   └── uma
│   │                       └── jmetal54
│   │                           ├── experiment
│   │                           ├── qualityIndicator
│   │                           ├── runner
│   │                           │   ├── multiobjective
│   │                           │   └── singleobjective
│   │                           ├── utility
│   │                           └── workingTest
│   └── jmetal-problem
│       └── src
│           ├── main
│           │   ├── java
│           │   │   └── org
│           │   │       └── uma
│           │   │           └── jmetal54
│           │   │               └── problem
│           │   │                   ├── multiobjective
│           │   │                   │   ├── UF
│           │   │                   │   ├── cdtlz
│           │   │                   │   ├── cec2015OptBigDataCompetition
│           │   │                   │   ├── dtlz
│           │   │                   │   ├── ebes
│           │   │                   │   ├── glt
│           │   │                   │   ├── lz09
│           │   │                   │   ├── mop
│           │   │                   │   ├── wfg
│           │   │                   │   └── zdt
│           │   │                   └── singleobjective
│           │   │                       └── cec2005competitioncode
│           │   └── resources
│           │       ├── MOEAD_Weights
│           │       ├── cec2005CompetitionResources
│           │       │   ├── supportData
│           │       │   └── testData
│           │       ├── cec2015Comp
│           │       ├── ebes
│           │       └── tspInstances
│           └── test
│               ├── java
│               │   └── org
│               │       └── uma
│               │           └── jmetal
│               │               └── problem
│               │                   └── multiobjective
│               └── resources
│                   ├── MOEAD_Weights
│                   └── pareto_fronts
├── jmetal-algorithm
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   └── org
│   │   │   │       └── uma
│   │   │   │           └── jmetal54
│   │   │   │               └── algorithm
│   │   │   │                   ├── multiobjective
│   │   │   │                   │   ├── abyss
│   │   │   │                   │   │   └── util
│   │   │   │                   │   ├── cellde
│   │   │   │                   │   ├── dmopso
│   │   │   │                   │   ├── gde3
│   │   │   │                   │   ├── gwasfga
│   │   │   │                   │   │   └── util
│   │   │   │                   │   ├── ibea
│   │   │   │                   │   ├── mocell
│   │   │   │                   │   ├── mochc
│   │   │   │                   │   ├── moead
│   │   │   │                   │   │   └── util
│   │   │   │                   │   ├── mombi
│   │   │   │                   │   │   └── util
│   │   │   │                   │   ├── nsgaii
│   │   │   │                   │   ├── nsgaiii
│   │   │   │                   │   │   └── util
│   │   │   │                   │   ├── omopso
│   │   │   │                   │   ├── paes
│   │   │   │                   │   ├── pesa2
│   │   │   │                   │   │   └── util
│   │   │   │                   │   ├── randomsearch
│   │   │   │                   │   ├── rnsgaii
│   │   │   │                   │   │   └── util
│   │   │   │                   │   ├── smpso
│   │   │   │                   │   ├── smsemoa
│   │   │   │                   │   ├── spea2
│   │   │   │                   │   │   └── util
│   │   │   │                   │   └── wasfga
│   │   │   │                   │       └── util
│   │   │   │                   └── singleobjective
│   │   │   │                       ├── coralreefsoptimization
│   │   │   │                       ├── differentialevolution
│   │   │   │                       ├── evolutionstrategy
│   │   │   │                       │   └── util
│   │   │   │                       ├── geneticalgorithm
│   │   │   │                       └── particleswarmoptimization
│   │   │   └── resources
│   │   │       ├── MOEAD_Weights
│   │   │       ├── cec2005CompetitionResources
│   │   │       │   ├── supportData
│   │   │       │   └── testData
│   │   │       ├── mombi2-weights
│   │   │       │   └── weight
│   │   │       │       ├── gecco
│   │   │       │       └── many_objective
│   │   │       └── tspInstances
│   │   └── test
│   │       ├── java
│   │       │   └── org
│   │       │       └── uma
│   │       │           └── jmetal
│   │       │               └── algorithm
│   │       │                   ├── multiobjective
│   │       │                   │   ├── abyss
│   │       │                   │   ├── dmopso
│   │       │                   │   ├── gde3
│   │       │                   │   ├── mocell
│   │       │                   │   ├── mombi2
│   │       │                   │   ├── nsgaii
│   │       │                   │   ├── omopso
│   │       │                   │   ├── smpso
│   │       │                   │   ├── smsemoa
│   │       │                   │   └── wasfga
│   │       │                   └── singleobjective
│   │       │                       ├── differentialevolution
│   │       │                       └── geneticalgorithm
│   │       └── resources
│   │           ├── MOEAD_Weights
│   │           ├── pareto_fronts
│   │           └── referenceFronts
│   └── target
│       ├── classes
│       │   ├── MOEAD_Weights
│       │   ├── cec2005CompetitionResources
│       │   │   ├── supportData
│       │   │   └── testData
│       │   ├── mombi2-weights
│       │   │   └── weight
│       │   │       ├── gecco
│       │   │       └── many_objective
│       │   ├── org
│       │   │   └── uma
│       │   │       └── jmetal54
│       │   │           └── algorithm
│       │   │               ├── multiobjective
│       │   │               │   ├── abyss
│       │   │               │   │   └── util
│       │   │               │   ├── cellde
│       │   │               │   ├── dmopso
│       │   │               │   ├── gde3
│       │   │               │   ├── gwasfga
│       │   │               │   │   └── util
│       │   │               │   ├── ibea
│       │   │               │   ├── mocell
│       │   │               │   ├── mochc
│       │   │               │   ├── moead
│       │   │               │   │   └── util
│       │   │               │   ├── mombi
│       │   │               │   │   └── util
│       │   │               │   ├── nsgaii
│       │   │               │   ├── nsgaiii
│       │   │               │   │   └── util
│       │   │               │   ├── omopso
│       │   │               │   ├── paes
│       │   │               │   ├── pesa2
│       │   │               │   │   └── util
│       │   │               │   ├── randomsearch
│       │   │               │   ├── rnsgaii
│       │   │               │   │   └── util
│       │   │               │   ├── smpso
│       │   │               │   ├── smsemoa
│       │   │               │   ├── spea2
│       │   │               │   │   └── util
│       │   │               │   └── wasfga
│       │   │               │       └── util
│       │   │               └── singleobjective
│       │   │                   ├── coralreefsoptimization
│       │   │                   ├── differentialevolution
│       │   │                   ├── evolutionstrategy
│       │   │                   │   └── util
│       │   │                   ├── geneticalgorithm
│       │   │                   └── particleswarmoptimization
│       │   └── tspInstances
│       └── test-classes
│           ├── MOEAD_Weights
│           ├── org
│           │   └── uma
│           │       └── jmetal
│           │           └── algorithm
│           │               ├── multiobjective
│           │               │   ├── abyss
│           │               │   ├── dmopso
│           │               │   ├── gde3
│           │               │   ├── mocell
│           │               │   ├── mombi2
│           │               │   ├── nsgaii
│           │               │   ├── omopso
│           │               │   ├── smpso
│           │               │   ├── smsemoa
│           │               │   └── wasfga
│           │               └── singleobjective
│           │                   ├── differentialevolution
│           │                   └── geneticalgorithm
│           ├── pareto_fronts
│           └── referenceFronts
├── jmetal-core
│   ├── bin
│   │   ├── src
│   │   │   ├── main
│   │   │   │   ├── java
│   │   │   │   │   └── org
│   │   │   │   │       └── uma
│   │   │   │   │           └── jmetal
│   │   │   │   │               ├── algorithm
│   │   │   │   │               │   └── impl
│   │   │   │   │               ├── measure
│   │   │   │   │               │   └── impl
│   │   │   │   │               ├── operator
│   │   │   │   │               │   └── impl
│   │   │   │   │               │       ├── crossover
│   │   │   │   │               │       ├── localsearch
│   │   │   │   │               │       ├── mutation
│   │   │   │   │               │       └── selection
│   │   │   │   │               ├── problem
│   │   │   │   │               │   └── impl
│   │   │   │   │               ├── qualityindicator
│   │   │   │   │               │   └── impl
│   │   │   │   │               │       └── hypervolume
│   │   │   │   │               │           └── util
│   │   │   │   │               ├── solution
│   │   │   │   │               │   ├── impl
│   │   │   │   │               │   └── util
│   │   │   │   │               └── util
│   │   │   │   │                   ├── archive
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── binarySet
│   │   │   │   │                   ├── comparator
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── chartcontainer
│   │   │   │   │                   ├── distance
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── evaluator
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── experiment
│   │   │   │   │                   │   ├── component
│   │   │   │   │                   │   └── util
│   │   │   │   │                   ├── extremevalues
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── fileinput
│   │   │   │   │                   │   └── util
│   │   │   │   │                   ├── fileoutput
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── front
│   │   │   │   │                   │   ├── imp
│   │   │   │   │                   │   └── util
│   │   │   │   │                   ├── naming
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── neighborhood
│   │   │   │   │                   │   ├── impl
│   │   │   │   │                   │   └── util
│   │   │   │   │                   ├── point
│   │   │   │   │                   │   ├── impl
│   │   │   │   │                   │   └── util
│   │   │   │   │                   │       ├── comparator
│   │   │   │   │                   │       └── distance
│   │   │   │   │                   ├── pseudorandom
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   ├── referencePoint
│   │   │   │   │                   │   └── impl
│   │   │   │   │                   └── solutionattribute
│   │   │   │   │                       └── impl
│   │   │   │   └── resources
│   │   │   │       ├── MOEAD_Weights
│   │   │   │       ├── cec2005CompetitionResources
│   │   │   │       │   ├── supportData
│   │   │   │       │   └── testData
│   │   │   │       ├── mombi2-weights
│   │   │   │       │   └── weight
│   │   │   │       │       ├── gecco
│   │   │   │       │       └── many_objective
│   │   │   │       ├── pareto_fronts
│   │   │   │       └── tspInstances
│   │   │   └── test
│   │   │       ├── java
│   │   │       │   └── org
│   │   │       │       └── uma
│   │   │       │           └── jmetal
│   │   │       │               ├── measure
│   │   │       │               │   └── impl
│   │   │       │               ├── operator
│   │   │       │               │   └── impl
│   │   │       │               │       ├── crossover
│   │   │       │               │       ├── localsearch
│   │   │       │               │       ├── mutation
│   │   │       │               │       └── selection
│   │   │       │               ├── qualityindicator
│   │   │       │               │   └── impl
│   │   │       │               │       └── hypervolume
│   │   │       │               ├── referencePoint
│   │   │       │               │   └── impl
│   │   │       │               ├── solution
│   │   │       │               │   ├── impl
│   │   │       │               │   └── util
│   │   │       │               └── util
│   │   │       │                   ├── archive
│   │   │       │                   │   └── impl
│   │   │       │                   ├── comparator
│   │   │       │                   ├── distance
│   │   │       │                   │   └── impl
│   │   │       │                   ├── front
│   │   │       │                   │   ├── imp
│   │   │       │                   │   └── util
│   │   │       │                   ├── naming
│   │   │       │                   │   └── impl
│   │   │       │                   ├── neighborhood
│   │   │       │                   │   ├── impl
│   │   │       │                   │   └── util
│   │   │       │                   ├── point
│   │   │       │                   │   ├── impl
│   │   │       │                   │   └── util
│   │   │       │                   ├── pseudorandom
│   │   │       │                   │   └── impl
│   │   │       │                   └── solutionattribute
│   │   │       │                       └── impl
│   │   │       └── resources
│   │   │           ├── MOEAD_Weights
│   │   │           ├── arrayFront
│   │   │           ├── lambda
│   │   │           └── pareto_fronts
│   │   └── target
│   │       ├── classes
│   │       │   ├── MOEAD_Weights
│   │       │   ├── cec2005CompetitionResources
│   │       │   │   ├── supportData
│   │       │   │   └── testData
│   │       │   ├── mombi2-weights
│   │       │   │   └── weight
│   │       │   │       ├── gecco
│   │       │   │       └── many_objective
│   │       │   ├── pareto_fronts
│   │       │   └── tspInstances
│   │       └── test-classes
│   │           ├── MOEAD_Weights
│   │           ├── arrayFront
│   │           ├── lambda
│   │           └── pareto_fronts
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   └── org
│   │   │   │       └── uma
│   │   │   │           └── jmetal54
│   │   │   │               ├── algorithm
│   │   │   │               │   └── impl
│   │   │   │               ├── measure
│   │   │   │               │   └── impl
│   │   │   │               ├── operator
│   │   │   │               │   └── impl
│   │   │   │               │       ├── crossover
│   │   │   │               │       ├── localsearch
│   │   │   │               │       ├── mutation
│   │   │   │               │       └── selection
│   │   │   │               ├── problem
│   │   │   │               │   └── impl
│   │   │   │               ├── qualityindicator
│   │   │   │               │   └── impl
│   │   │   │               │       └── hypervolume
│   │   │   │               │           └── util
│   │   │   │               ├── solution
│   │   │   │               │   ├── impl
│   │   │   │               │   └── util
│   │   │   │               └── util
│   │   │   │                   ├── archive
│   │   │   │                   │   └── impl
│   │   │   │                   ├── binarySet
│   │   │   │                   ├── comparator
│   │   │   │                   │   └── impl
│   │   │   │                   ├── chartcontainer
│   │   │   │                   ├── distance
│   │   │   │                   │   └── impl
│   │   │   │                   ├── evaluator
│   │   │   │                   │   └── impl
│   │   │   │                   ├── experiment
│   │   │   │                   │   ├── component
│   │   │   │                   │   └── util
│   │   │   │                   ├── extremevalues
│   │   │   │                   │   └── impl
│   │   │   │                   ├── fileinput
│   │   │   │                   │   └── util
│   │   │   │                   ├── fileoutput
│   │   │   │                   │   └── impl
│   │   │   │                   ├── front
│   │   │   │                   │   ├── imp
│   │   │   │                   │   └── util
│   │   │   │                   ├── naming
│   │   │   │                   │   └── impl
│   │   │   │                   ├── neighborhood
│   │   │   │                   │   ├── impl
│   │   │   │                   │   └── util
│   │   │   │                   ├── point
│   │   │   │                   │   ├── impl
│   │   │   │                   │   └── util
│   │   │   │                   │       ├── comparator
│   │   │   │                   │       └── distance
│   │   │   │                   ├── pseudorandom
│   │   │   │                   │   └── impl
│   │   │   │                   ├── referencePoint
│   │   │   │                   │   └── impl
│   │   │   │                   └── solutionattribute
│   │   │   │                       └── impl
│   │   │   └── resources
│   │   │       ├── MOEAD_Weights
│   │   │       ├── cec2005CompetitionResources
│   │   │       │   ├── supportData
│   │   │       │   └── testData
│   │   │       ├── mombi2-weights
│   │   │       │   └── weight
│   │   │       │       ├── gecco
│   │   │       │       └── many_objective
│   │   │       ├── pareto_fronts
│   │   │       └── tspInstances
│   │   └── test
│   │       ├── java
│   │       │   └── org
│   │       │       └── uma
│   │       │           └── jmetal
│   │       │               ├── measure
│   │       │               │   └── impl
│   │       │               ├── operator
│   │       │               │   └── impl
│   │       │               │       ├── crossover
│   │       │               │       ├── localsearch
│   │       │               │       ├── mutation
│   │       │               │       └── selection
│   │       │               ├── qualityindicator
│   │       │               │   └── impl
│   │       │               │       └── hypervolume
│   │       │               ├── referencePoint
│   │       │               │   └── impl
│   │       │               ├── solution
│   │       │               │   ├── impl
│   │       │               │   └── util
│   │       │               └── util
│   │       │                   ├── archive
│   │       │                   │   └── impl
│   │       │                   ├── comparator
│   │       │                   ├── distance
│   │       │                   │   └── impl
│   │       │                   ├── front
│   │       │                   │   ├── imp
│   │       │                   │   └── util
│   │       │                   ├── naming
│   │       │                   │   └── impl
│   │       │                   ├── neighborhood
│   │       │                   │   ├── impl
│   │       │                   │   └── util
│   │       │                   ├── point
│   │       │                   │   ├── impl
│   │       │                   │   └── util
│   │       │                   ├── pseudorandom
│   │       │                   │   └── impl
│   │       │                   └── solutionattribute
│   │       │                       └── impl
│   │       └── resources
│   │           ├── MOEAD_Weights
│   │           ├── arrayFront
│   │           ├── lambda
│   │           └── pareto_fronts
│   └── target
│       ├── classes
│       │   ├── MOEAD_Weights
│       │   ├── cec2005CompetitionResources
│       │   │   ├── supportData
│       │   │   └── testData
│       │   ├── mombi2-weights
│       │   │   └── weight
│       │   │       ├── gecco
│       │   │       └── many_objective
│       │   ├── org
│       │   │   └── uma
│       │   │       └── jmetal54
│       │   │           ├── algorithm
│       │   │           │   └── impl
│       │   │           ├── measure
│       │   │           │   └── impl
│       │   │           ├── operator
│       │   │           │   └── impl
│       │   │           │       ├── crossover
│       │   │           │       ├── localsearch
│       │   │           │       ├── mutation
│       │   │           │       └── selection
│       │   │           ├── problem
│       │   │           │   └── impl
│       │   │           ├── qualityindicator
│       │   │           │   └── impl
│       │   │           │       └── hypervolume
│       │   │           │           └── util
│       │   │           ├── solution
│       │   │           │   ├── impl
│       │   │           │   └── util
│       │   │           └── util
│       │   │               ├── archive
│       │   │               │   └── impl
│       │   │               ├── binarySet
│       │   │               ├── comparator
│       │   │               │   └── impl
│       │   │               ├── chartcontainer
│       │   │               ├── distance
│       │   │               │   └── impl
│       │   │               ├── evaluator
│       │   │               │   └── impl
│       │   │               ├── experiment
│       │   │               │   ├── component
│       │   │               │   └── util
│       │   │               ├── extremevalues
│       │   │               │   └── impl
│       │   │               ├── fileinput
│       │   │               │   └── util
│       │   │               ├── fileoutput
│       │   │               │   └── impl
│       │   │               ├── front
│       │   │               │   ├── imp
│       │   │               │   └── util
│       │   │               ├── naming
│       │   │               │   └── impl
│       │   │               ├── neighborhood
│       │   │               │   ├── impl
│       │   │               │   └── util
│       │   │               ├── point
│       │   │               │   ├── impl
│       │   │               │   └── util
│       │   │               │       ├── comparator
│       │   │               │       └── distance
│       │   │               ├── pseudorandom
│       │   │               │   └── impl
│       │   │               ├── referencePoint
│       │   │               │   └── impl
│       │   │               └── solutionattribute
│       │   │                   └── impl
│       │   ├── pareto_fronts
│       │   └── tspInstances
│       └── test-classes
│           ├── MOEAD_Weights
│           ├── arrayFront
│           ├── lambda
│           ├── org
│           │   └── uma
│           │       └── jmetal
│           │           ├── measure
│           │           │   └── impl
│           │           ├── operator
│           │           │   └── impl
│           │           │       ├── crossover
│           │           │       ├── localsearch
│           │           │       ├── mutation
│           │           │       └── selection
│           │           ├── qualityindicator
│           │           │   └── impl
│           │           │       └── hypervolume
│           │           ├── referencePoint
│           │           │   └── impl
│           │           ├── solution
│           │           │   ├── impl
│           │           │   └── util
│           │           └── util
│           │               ├── archive
│           │               │   └── impl
│           │               ├── comparator
│           │               ├── distance
│           │               │   └── impl
│           │               ├── front
│           │               │   ├── imp
│           │               │   └── util
│           │               ├── naming
│           │               │   └── impl
│           │               ├── neighborhood
│           │               │   ├── impl
│           │               │   └── util
│           │               ├── point
│           │               │   ├── impl
│           │               │   └── util
│           │               ├── pseudorandom
│           │               │   └── impl
│           │               └── solutionattribute
│           │                   └── impl
│           └── pareto_fronts
├── jmetal-exec
│   ├── bin
│   │   └── src
│   │       └── main
│   │           └── java
│   │               └── org
│   │                   └── uma
│   │                       └── jmetal
│   │                           ├── experiment
│   │                           ├── qualityIndicator
│   │                           ├── runner
│   │                           │   ├── multiobjective
│   │                           │   └── singleobjective
│   │                           ├── utility
│   │                           └── workingTest
│   ├── src
│   │   └── main
│   │       └── java
│   │           └── org
│   │               └── uma
│   │                   └── jmetal54
│   │                       ├── experiment
│   │                       ├── qualityIndicator
│   │                       ├── runner
│   │                       │   ├── multiobjective
│   │                       │   └── singleobjective
│   │                       ├── utility
│   │                       └── workingTest
│   └── target
│       └── classes
│           └── org
│               └── uma
│                   └── jmetal54
│                       ├── experiment
│                       ├── qualityIndicator
│                       ├── runner
│                       │   ├── multiobjective
│                       │   └── singleobjective
│                       ├── utility
│                       └── workingTest
├── jmetal-problem
│   ├── bin
│   │   ├── src
│   │   │   ├── main
│   │   │   │   ├── java
│   │   │   │   │   └── org
│   │   │   │   │       └── uma
│   │   │   │   │           └── jmetal
│   │   │   │   │               └── problem
│   │   │   │   │                   ├── multiobjective
│   │   │   │   │                   │   ├── UF
│   │   │   │   │                   │   ├── cdtlz
│   │   │   │   │                   │   ├── cec2015OptBigDataCompetition
│   │   │   │   │                   │   ├── dtlz
│   │   │   │   │                   │   ├── ebes
│   │   │   │   │                   │   ├── glt
│   │   │   │   │                   │   ├── lz09
│   │   │   │   │                   │   ├── mop
│   │   │   │   │                   │   ├── wfg
│   │   │   │   │                   │   └── zdt
│   │   │   │   │                   └── singleobjective
│   │   │   │   │                       └── cec2005competitioncode
│   │   │   │   └── resources
│   │   │   │       ├── MOEAD_Weights
│   │   │   │       ├── cec2005CompetitionResources
│   │   │   │       │   ├── supportData
│   │   │   │       │   └── testData
│   │   │   │       ├── cec2015Comp
│   │   │   │       ├── ebes
│   │   │   │       └── tspInstances
│   │   │   └── test
│   │   │       ├── java
│   │   │       │   └── org
│   │   │       │       └── uma
│   │   │       │           └── jmetal
│   │   │       │               └── problem
│   │   │       │                   └── multiobjective
│   │   │       └── resources
│   │   │           ├── MOEAD_Weights
│   │   │           └── pareto_fronts
│   │   └── target
│   │       ├── classes
│   │       │   ├── MOEAD_Weights
│   │       │   ├── cec2005CompetitionResources
│   │       │   │   ├── supportData
│   │       │   │   └── testData
│   │       │   ├── cec2015Comp
│   │       │   ├── ebes
│   │       │   └── tspInstances
│   │       └── test-classes
│   │           ├── MOEAD_Weights
│   │           └── pareto_fronts
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   └── org
│   │   │   │       └── uma
│   │   │   │           └── jmetal54
│   │   │   │               └── problem
│   │   │   │                   ├── multiobjective
│   │   │   │                   │   ├── UF
│   │   │   │                   │   ├── cdtlz
│   │   │   │                   │   ├── cec2015OptBigDataCompetition
│   │   │   │                   │   ├── dtlz
│   │   │   │                   │   ├── ebes
│   │   │   │                   │   ├── glt
│   │   │   │                   │   ├── lz09
│   │   │   │                   │   ├── mop
│   │   │   │                   │   ├── wfg
│   │   │   │                   │   └── zdt
│   │   │   │                   └── singleobjective
│   │   │   │                       └── cec2005competitioncode
│   │   │   └── resources
│   │   │       ├── MOEAD_Weights
│   │   │       ├── cec2005CompetitionResources
│   │   │       │   ├── supportData
│   │   │       │   └── testData
│   │   │       ├── cec2015Comp
│   │   │       ├── ebes
│   │   │       └── tspInstances
│   │   └── test
│   │       ├── java
│   │       │   └── org
│   │       │       └── uma
│   │       │           └── jmetal
│   │       │               └── problem
│   │       │                   └── multiobjective
│   │       └── resources
│   │           ├── MOEAD_Weights
│   │           └── pareto_fronts
│   └── target
│       ├── classes
│       │   ├── MOEAD_Weights
│       │   ├── cec2005CompetitionResources
│       │   │   ├── supportData
│       │   │   └── testData
│       │   ├── cec2015Comp
│       │   ├── ebes
│       │   ├── org
│       │   │   └── uma
│       │   │       └── jmetal54
│       │   │           └── problem
│       │   │               ├── multiobjective
│       │   │               │   ├── UF
│       │   │               │   ├── cdtlz
│       │   │               │   ├── cec2015OptBigDataCompetition
│       │   │               │   ├── dtlz
│       │   │               │   ├── ebes
│       │   │               │   ├── glt
│       │   │               │   ├── lz09
│       │   │               │   ├── mop
│       │   │               │   ├── wfg
│       │   │               │   └── zdt
│       │   │               └── singleobjective
│       │   │                   └── cec2005competitioncode
│       │   └── tspInstances
│       └── test-classes
│           ├── MOEAD_Weights
│           ├── org
│           │   └── uma
│           │       └── jmetal
│           │           └── problem
│           │               └── multiobjective
│           └── pareto_fronts
└── uncommons-maths-1.2.3
    ├── docs
    │   └── api
    │       ├── org
    │       │   └── uncommons
    │       │       └── maths
    │       │           ├── binary
    │       │           ├── combinatorics
    │       │           ├── number
    │       │           ├── random
    │       │           └── statistics
    │       └── resources
    ├── lib
    └── src
```




---

## 🛠️ Instal·lació

Per executar el projecte:

- Java 8 o superior
- Maven o Gradle (per compilar)
- IDE com IntelliJ o Eclipse (opcional)

---

## 🚀 Instruccions d’instal·lació

1. **Clonar aquest repositori:**

```bash
git clone https://github.com/usuari/cloudsim-comparativa.git
cd cloudsim-comparativa```
You just need to unpack the CloudSim file to install.
If you want to remove CloudSim, then remove the whole cloudsim directory.
You do not need to compile CloudSim source code. The JAR files are
provided to compile and to run CloudSim applications:

  * jars/cloudsim-<VERSION>.jar                    -- contains the CloudSim class files
  * jars/cloudsim-<VERSION>-sources.jar            -- contains the CloudSim source code files
  * jars/cloudsim-examples-<VERSION>.jar           -- contains the CloudSim examples class files
  * jars/cloudsim-examples-<VERSION>-sources.jar   -- contains the CloudSim examples source code files



---

## CLOUDSIM 4.0




---

## CLOUDSIM 7.0
