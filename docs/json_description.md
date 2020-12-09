# Introduction

This documents describes the structure of .json file that is the input to the MNA algorithm. Important fields for MNA are described below.

# JSON Content Description

[JSON file](https://en.wikipedia.org/wiki/JSON) is a file that stores simple data structures and objects (dictionaries, lists, etc.). It is a standard data interchange format. In JSON file provided by Typhoon Schematic Editor there are several sections important for MNA
* **dev_partitions** contains all the required data about the circuit - what are the components, what are their properties and how are they connected.
* **nodes** contains the list of all nodes. Each element of this list represents a single electrical node. Nodes section is a sub-section of dev_partitions
* **components** contains the list of all components in the model. Each element of this list represents a single component
```
"dev_partitions": [
        {
            "_cls": "DevPartition",
            "nodes": [],
            "components": []
]
```
## "nodes" and a "node"

Nodes section contains all node entries that exist in the model. Each node represents an electrical node. Each node contains a list of electrical terminals of components that are connected to it. Electrical terminals are represented within a node by a their unique id. Each node has it's own unique id. Example of a a two node circuit is shown below.
```
"nodes": [
         {
             "_cls": "Node",
             "id": 2083470920288,
             "terminals": [
                 2083470955520,
                 2083470946368,
                 2083470898752,
                 2083472317024,
                 2083472315008,
                 2083472538256,
                 2083472317264,
                 2083472301936
             ]
         },
         {
             "_cls": "Node",
             "id": 2083470919280,
             "terminals": [
                 2083472317456,
                 2083470955184,
                 2083472317120,
                 2083472300208,
                 2083470900528,
                 2083470774128,
                 2083472317360,
                 2083470900720
             ]
         }
     ],
```
##  "components" and a "component"
Components section contains all component entries that exist in the model. Each component has the following important sub-sections:
* **id** represent it's unique ID
* **name** fully qualified name of a component, it is also unique
* **comp_type** entry that describes the type of a component
* **properties** a list of all properties of a component. This list contains much more than required for MNAm therefor only the required ones should be used. Example: for inductor, only inductance and inital_current are sufficient.
* **terminals** all terminals of an electrical component. Terminals have a unique ID the will be used within the node objects. A terminal can be assigned to only one electrical node.
```
{
  "_cls": "Component",
  "id": 2083470770288,
  "name": "L1",
  "vars": {
      "inductance": 0.001
  },
  "comp_type": "pas_inductor",
  "lib_fqn": "Passive Components.Inductor",
  "composite": false,
  "properties": [
      {
          "_cls": "Property",
          "name": "visible",
          "value": true,
          "vector": false,
          "calc_type": "bool"
      },
      {
          "_cls": "Property",
          "name": "inductance",
          "value": 0.001,
          "vector": false,
          "calc_type": "real"
      },
      {
          "_cls": "Property",
          "name": "pole_shift_ignore",
          "value": false,
          "vector": false,
          "calc_type": "bool"
      },
      {
          "_cls": "Property",
          "name": "initial_current",
          "value": 0.0,
          "vector": false,
          "calc_type": "real"
      }
  ],
  "terminals": [
      {
          "_cls": "Terminal",
          "id": 2083470955520,
          "name": "p_node",
          "kind": "pe",
          "dimension": [],
          "direction": null,
          "sp_type": null,
          "feedthrough": true
      },
      {
          "_cls": "Terminal",
          "id": 2083470774128,
          "name": "n_node",
          "kind": "pe",
          "dimension": [],
          "direction": null,
          "sp_type": null,
          "feedthrough": true
      }
  ],
```