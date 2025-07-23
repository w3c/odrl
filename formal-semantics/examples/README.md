# Formal Semantics Examples

This folder contains examples of policies that are evaluated according to the [ODRL formal semantics document](https://w3c.github.io/odrl/formal-semantics/).

These examples are organised into two levels of sub-folders following the taxonomization of policy types described in the [ODRL formal semantics document](https://w3c.github.io/odrl/formal-semantics/). Within each policy type folder several examples are expected to be found, each example consist of at least 4 files: `policy.json`, `state.json` `evaluationrequest.json`, `compliancereport.json`. Following an overview of the tree structure is given: 

```console
.
└── odrl/formal-semantics/examples/
    ├── A Evaluation of Constraints/
    │   ├── A1 Example of a constrained permission
    │   │  └── A1.1 Input Output
    │   │  └── A1.2 Input Output   
    │   ├── A2 Example of a constrained prohibition
    │   └── ...
    ├── B Evaluation of Refinements/

    ├── C Evaluation of Conditions (Duties)/
    │   ├── C1 Example of a conditioned permission
    │   ├── C2 Example of a permission whose condition has constraints
    │   └── ...
    │
    └── ...
```

## How to contribute new examples

Contributors are invited to add new examples to the formal-semantics/examples folder. To this end, they **must fork the repository and propose a pull request with the contribution**. Adding a new example will consist on creating a new sub-folder following the format of the sub-folder and including the following files:

* (Mandatory, main folder of the example) policy.json – the policy being evaluated in `JSON-LD 1.1`.
* (Mandatory INPUT subfolder of the example) state.json – the system or context state of the world in `JSON-LD 1.1`.
* (Mandatory INPUT subfolder of the example) evaluationrequest.json – the evaluation request in `JSON-LD 1.1`.
* (Optional INPUT subfolder of the example) Behaviour – a file containing one of the following words: default, close, or open. In the case this file is not provided, it is considered that the policy should be evaluated following the close behaviour.
* (Mandatory OUTPUT subfolder of the example) compliancereport.json – the result of the evaluation in `JSON-LD 1.1`.
* (Optional main folder of the example) README.md – a brief human-readable description of the example, its purpose, the authors and the context of the example (e.g., a research project or company use case).

Any of the previous RDF files can be submitted in `Turtle`, for this case, use the `.ttl` extension for the Turtle files.
