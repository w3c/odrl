# Formal Semantics Examples

This folder contains examples of policies that are evaluated according to the [ODRL formal semantics document](https://w3c.github.io/odrl/formal-semantics/).

These examples are organised into two levels of sub-folders following the taxonomization of policy types described in the [ODRL formal semantics document](https://w3c.github.io/odrl/formal-semantics/). Within each policy type folder several examples are expected to be found, each example consist of at least 4 files: `policy.json`, `state.json` `evaluationrequest.json`, `compliancereport.json`. Following an overview of the tree structure is given: 

```console
.
└── odrl/formal-semantics/examples/
    ├── A Evaluation of Constraints and Refinements/
    │   ├── A1 Example of a constrained permission
    │   ├── A2 Example of a permission whose permitted action is refined
    │   └── ...
    │
    └── B Evaluation of Conditions (Duties)/
        ├── B1 Example of a conditioned permission
        ├── B2 Example of a permission whose condition has constraints
        └── ...
```

## How to contribute new examples

Contributors are invited to add new examples to the formal-semantics/examples folder. To this end, they **must fork the repository and propose a pull request with the contribution**. Adding a new example will consist on creating a new sub-folder following the format of the sub-folder and including the following files:

* (Mandatory) policy.json – the policy being evaluated in `JSON-LD 1.1`.
* (Mandatory) state.json – the system or context state of the world in `JSON-LD 1.1`.
* (Mandatory) evaluationrequest.json – the evaluation request in `JSON-LD 1.1`.
* (Mandatory) compliancereport.json – the result of the evaluation in `JSON-LD 1.1`.
* (Optional) README.md – a brief human-readable description of the example, its purpose, the authors and the context of the example (e.g., a research project or company use case).
* (Optional) Behaviour – a file containing one of the following words: default, close, or open. In the case this file is not provided, it is considered that the policy should be evaluated following the close behaviour.

Any of the previous RDF files can be submitted in `Turtle`, for this case, use the `.ttl` extension for the Turtle files.
