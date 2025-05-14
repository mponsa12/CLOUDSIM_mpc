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

```
cloudsim-4.0/
├── modules/
│   ├── cloudsim/
│   │   ├── src/
│   │       └── main/
│   │           └── java/
│   │               └── org/
│   │                   └── cloudbus/
│   │                       └── cloudsim/
│   └── cloudsim-examples/
│       ├── src/
│           └── main/
│               └── java/
│                   └── org/
│                       └── cloudbus/
│                           └── cloudsim/
│                               └── examples/
├── documentation/                                       
└── distribution/  
```

Fent ús del software *Merge*, podem veure que en Sergi va copiar la carpeta ```modules/cloudsim/src/main/java/org/cloudbus/cloudsim/``` del projecte original CloudSim G4 i la va ubicar en el directori ```cloud-sergi/src/main/java/org/cloudbus/cloudsim/```. Va fer petites modificacions en alguns fitxers i va afegir el directori EXAMPLES.


```
cloud_sergi/
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
│   │   │   │   ├── ORG             # Conté l'estructura del CloudSim G4 
│   │   │   │   │   └── cloudbus
│   │   │   │   │       └── cloudsim
│   │   │   │   │           ├── container
│   │   │   │   │           ├── core
│   │   │   │   │           ├── distributions
│   │   │   │   │           ├── EXAMPLES                # Directori afegit
│   │   │   │   │           │   ├── container
│   │   │   │   │           │   ├── network
│   │   │   │   │           │   │   └── datacenter
│   │   │   │   │           │   └── power
│   │   │   │   │           │       ├── planetlab
│   │   │   │   │           │       └── random
│   │   │   │   │           ├── lists
│   │   │   │   │           ├── network
│   │   │   │   │           ├── power
│   │   │   │   │           ├── provisioners
│   │   │   │   │           └── util
│   │   │   │   ├── shedulers
│   │   │   │   ├── simulator
│   │   │   │   ├── svila
│   │   │   │   ├── system
│   │   │   │   ├── ut
│   │   │   │   └── util
│   │   │   └── resources
│   │   └── test
│   └── target
├── jmetal
├── jmetal-algorithm
├── jmetal-core
├── jmetal-exec
├── jmetal-problem
└── uncommons-maths-1.2.3
```

### 📁 Fitxers Modificats

| Fitxer | Canvi | Motiu |
|--------|-------|-------|
|```cloudsim/network/datacenter/TopologicalGraph.java```|Afegeix comentari ```// WORKING ON private Map<Node> nodeMap;```| ...|
|```cloudsim/network/datacenter/TopologicalNode.java```|<ul><li>Afegeix mètode public *setNodeLabel(String name)*<br></li><li>Afegeix setter `setNodeLabel(String name)`</li></ul>| ... |
|```cloudsim/power/models/PowerModelSpecPower.java```|<ul><li>Afegeix condició: <code>if (utilization > 1 && utilization < 1.0001){<br>utilization = 1;<br>}</code>al mètode <code>getPower()</code></li></ul>|...|
|```cloudsim/power/PowerDatacenter.java```|<ul><li>Afegeix la variable pública *snapshots* de tipus *List&lt;Snapshot&gt;*</li><li>Afegeix la variable pública *migrationDelay* de tipus *migrationDelay*</li><li>Afegeix la variable privada *datacenterBroker* de tipus *datacenterBroker*</li><li>Afegeix la variable privada *slotNum* de tipus *int*</li><li>Inicialitza dins el constructor les variables *snapshots* i *slotNum*</li><li>Afegeix setter de *datacenterBroker*</li><li>Afegeix setter de *migrationDelayer*</li><li>Afegeix mètode públic *updateMigrationDelayer()*</li><li>Afegeix mètode privat *migrationDelayerAllowsMigrations()*</li><li>Al mètode *updateCloudletProcessing()*:<ul><li>Afegeix un comptador de VMs per host</li><li>Executa *updateMigrationDelayer()*</li><li>Fa un *snapshot* del sistema</li><li>Inclou diferents maneres per calcular el *delay* de migració<li>Assigna *slotNum* per calcular el temps discret</li></ul></li><li>Afegeix un *StaticLog.showHostInfo()* al mètode *updateCloudletProcessingWithoutSchedulingFutureEventsForce()*</li><li>Afegeix un *JSONOutput.addPowerDatacenterState()* al mètode *updateCloudletProcessingWithoutSchedulingFutureEventsForce()*</li></ul>|...|
|```cloudsim/power/PowerHost.java```|<ul><li>Afegeix mètode *toString()*<br></li><li>Afegeix mètode *toJSON()*</li></ul>|...|
|```cloudsim/power/PowerHostUtilizationHistory.java```|Canvia el mètode *getUtilizationHistory()* de *protected* a *public*|...|
|```cloudsim/power/PowerVm.java```|Canvia el mètode *getUtilizationHistory()* de *protected* a *public*|...|
|```cloudsim/power/PowerVmAllocationPolicyAbstract.java```|<ul><li>Afegeix getter i setter de *VmSelectionPolicy*</li><li>Afegeix condició: <code>if(vm.hasPreAssignedHost) {vm.hasPreAssignedHost = false;</br>return vm.preAssignedHost;</br>}</code>al mètode *findHostForVm()*</li></ul>|...|
|```cloudsim/power/PowerVmAllocationPolicyMigrationAbstract.java```|<ul><li>Borra la variable privada vmSelectionPolicy</li><li>Borra la variable privada vmSelectionPolicy</li><li>Crea el mètode public *getSavedAllocationBackDoor()* de tipus *List<Map<String,Object>>*</li><li>Afegeix un constructor amb paràmetre *hostList* de tipus *List<? extends Host>*</li><li>Crea el mètode public *showMigrationMap()*</li><li>Canvia el mètode *getMigrationMapFromUnderUtilizedHosts()* de *protected* a *public*</li><li>Inicialitza la variable *underUtilizedHost* a *null* en el mètode *getMigrationMapFromUnderUtilizedHosts()*</li><li>Afegeix condició: <code>if(vm.hasPreAssignedHost) {vm.hasPreAssignedHost = false; return vm.preAssignedHost;}</code>al mètode *findHostForVm()*</li><li>Canvia el mètode *getNewVmPlacement()* de *protected* a *public*</li><li>Canvia el mètode *getVmsToMigrateFromHosts()* de *protected* a *public*</li><li>Canvia el mètode *getOverUtilizedHosts()* de *protected* a *public*</li><li>Canvia el mètode *isHostOverUtilized()* de *protected* a *public*</li><li>Canvia el mètode *saveAllocation()* de *protected* a *public*</li><li>Canvia el mètode *restoreAllocation()* de *protected* a *public*</li><li>Borra el setter i el getter de *vmSelecionPolicy*</li></ul>|...|
|```cloudsim/power/PowerVmAllocationPolicyMigrationInterQuartileRange.java```|<ul><li>Canvia el mètode *isHostOverUtilized()* de *protected* a *public*</li><li>Afegeix un *println* per mostrar informació pel terminal (hostID, isMigrationRequired)</li></ul>|...|
|```cloudsim/power/PowerVmAllocationPolicyMigrationLocalRegression.java```|Canvia el mètode *isHostOverUtilized()* de *protected* a *public*|...|
|```cloudsim/power/PowerVmAllocationPolicyMigrationMedianAbsoluteDeviation.java```|Canvia el mètode *isHostOverUtilized()* de *protected* a *public*|...|
|```cloudsim/power/PowerVmAllocationPolicyMigrationStaticThreshold.java```|Canvia els mètodes *isHostOverUtilized()* i *getUtilizationThreshold()* de *protected* a *public*|...|
|```cloudsim/power/PowerVmSelectionPolicy.java```|<ul><li>Afegeix getter i setter de AllocationPolicy</li><li>Afegeix getter i setter de PowerDatacenter</li></ul>|...|
|```cloudsim/power/PowerVmSelectionPolicyMaximumCorrelation.java```|<ul><li>Canvia el mètode *getCorrelationCoefficients()* de *protected* a *public*</li><li>Afegeix un *println* al principi i al final del mètode *getVmToMigrate()* per mostrar informació pel terminal (hostID)</li></ul>|...|
|```cloudsim/util/WorkloadFileReader.java```|Afegeix un ```@see Task```|...|
|```cloudsim/util/WorkloadModel.java```|Canvia un ```@see Workload``` per un ```@see Task```|...|
|```cloudsim/DatacenterBroker.java```|<ul><li>Crea els getters i setters de:<ul><li><code>fullTopology</code></li><li><code>centralTopology</code></li><li><code>treeTopology</code></li><li><code>leafTopology</code></li><li><code>vmsTopology</code></li><li><code>baseTopology</code></li><li><code>initialTopology</code></li><li><code>interactionsContainer</code></li></ul></li></ul><ul><li>Crea el mètode public *createSubTopologiesFromFullTopology()*</li><li>Crea el mètode public *createBaseTopologyFromFullTopology()*</li><li>Inicialitza les variables *vmHostMap* i *vmIdMap* en el constructor</li><li>Dins del mètode *processVmCreate()* afegeix un <code>vmHostMap.put(vm, vm.getHost()); vmIdMap.put(vm.getId(), vm);</code> si <code>result == CloudSimTags.TRUE</code></li><li>Afegeix condició: <code>if(finishTime == 0) {finishTime = CloudSim.clock();}</code> en el mètode *shutdownEntity()*</li>|...|
|```cloudsim/Host.java```|VARIS CANVIS, MIRAR COM POSAR-HO|...|
|```cloudsim/HostDynamicWorkload.java```|<ul><li>Afegeix el mètode *extraInfo()* i l'usa dins de *updateVmsProcessing()*</li><li>Comenta les línies ```if (vm.getCurrentRequestedTotalMips() == 0){vmsToRemove.add(vm);}``` del mètode *getCompletedVms()*</li></ul>|...|
|```cloudsim/UtilizationModelPlanetLabInMemory.java```|<ul><li>Canvia la variable *schedulingInverval* de *private* a *protected*</li><li>Canvia la variable *data* de *private* a *protected*</li></ul>|...|
|```cloudsim/Vm.java```|<ul><li>Fa un implements de *NetworkElement* a la classe</li><li>VARIS CANVIS... MIRAR COM POSAR-HO</li></ul>|...|
|```cloudsim/VmAllocationPolicy.java```|<ul><li>Afegeix la variable publica *vmSelectionPolicy* de tipus *PowerVmSelectionPolicy*</li><li>Afegeix la variable privada *powerDatacenter* de tipus *PowerDatacenter*</li><li>Afegeix getter i setter de *powerDatacenter*</li><li>Canvia el mètode *setHostList()* de *protected* a *public*</li></ul>|...|
|```cloudsim/VmSchedulerTimeShared.java```|Afegeix dos logs dins del mètode *allocatePesForVm()*|...|

---

## 🧰 Requisits previs

Assegura’t de tenir instal·lat:

* Java JDK (versió 8 o superior)
* Apache Maven o Gradle (segons la versió)
* IntelliJ IDEA o qualsevol IDE Java
---

## 🛠️ Instal·lació

*1. Descomprimir el fitxer zip corresponent*
  - [CloudSim 4.0 i 7.0](https://github.com/cloudslab/cloudsim/releases)
  - [CloudSim-sergi](https://bitbucket.org/svila_phd/metacloudsim/src/vmAllocation/)

*2. Importar el projecte al teu IDE Java*

*3. Executar un exemple*
   - Ves a ```cloudsim-examples/src/main/java/org/cloudbus/cloudsim/examples/```
   - Executa una classe com ```CloudSimExample1.java```

---
