# ODRL Landscape

This document is collaborative effort that attempts to collect all projects, tooling and implementations that work with the Open Digital Rights Language (ODRL).

## What is ODRL?

The [Open Digital Rights Language (ODRL) Information Model 2.2](https://www.w3.org/TR/odrl-model/) is a W3C Recommendation to express **usage control policies**.

ODRL policies define **who** can perform **which action** on **which resource**, and under **what conditions**. These policies are composed of one or more **rules**, which are based on **deontic concepts**:
- **Permission**: explicitly allows an action. (e.g. *"Alice may **read** Resource X on Monday, 15 September 2025, between 09:00 and 17:00."*)  
- **Prohibition**: explicitly forbids an action. (e.g. *"Alice is **not allowed** to write to Resource X."*)  
- **Obligation**: requires an action to be fulfilled before or during usage. (e.g. *"Alice must **pay 5 euros** in order to read Resource X."*)  

## Why this document matters?

Orignally, ODRL was originally designed for **Digital Rights Management (DRM)**, focusing on expressing rights and obligations for digital content. 
For the most recent version, the scope was thus mainly on expression: providing a common information model for representing such policies.

Since ~2020, organizations have started exploring ODRL for access and usage control **enforcement**.
This shift created a need for **software and tooling** capable of **evaluating** ODRL policies in operational environments. 
For example, projects like [Solid](https://solidproject.org/TR/protocol) considered ODRL for data usage control (see related github issues: [WAC-10](https://github.com/solid/web-access-control-spec/issues/10), [WAC-87](https://github.com/solid/web-access-control-spec/issues/87), [Solid-56](https://github.com/solid/specification/issues/56#issuecomment-872020854), [Authz](https://solid.github.io/authorization-panel/authorization-ucr/#conditional-time)), but these efforts stalled due to the lack of a formalized, systematic evaluation approach.
Dataspaces also mention to use ODRL as usage control policy language for enforcement (both Gaia-X and IDSA).

Recently, significant progress has been made toward formalizing ODRL semantics.
The [ODRL Formal Semantics Community Group](https://w3id.org/odrl-fs/) is working on **standardizing the inputs** required for policy evaluation, such as the state of the world, the evaluation request, and the policies themselves.
In parallel, they are defining the **expected outputs** through the [Compliance Report Model](https://w3id.org/force/compliance-report) and developing a formal semantics for ODRL to ensure consistent and **interoperable evaluations across different implementations**.
As of today (15 September 2025), these efforts are ongoing.
This document aims to provide an overview of existing tools, frameworks, and approaches for ODRL policy evaluation, helping practitioners and researchers navigate the current landscape and contribute to these standardization efforts.

## ODRL Evaluator implementations, projects using ODRL and ODRL tooling

### ODRL Evaluators

An ODRL Evaluator is defined as follows by the [ODRL Information Model 2.2](https://www.w3.org/TR/odrl-model/) as

>  A system that determines whether the Rules of an ODRL Policy expression have meet their intended action performance.

Thus, in this overview, we have added all evaluators that we know of. 
The table has three columns
- Name: what is the project name, with a link to the source
- Context: contains what it does (capabilities), which software language is used to implement it. 
  - Future work should include: the input (apart from the policies) and the output (yes/no vs compliance report vs ...)
- Authors: the group that created it and (if possible) a contact person

| Name                                                                                                 | Context                                                                                                                                                                                                                                 | Authors                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [ODRL Evaluator](https://w3id.org/force/evaluator)                                                   | An open implementation of an ODRL Evaluator that evaluates ODRL policies by generating Compliance Reports.<br> Written in Node.js and Notation3 (prolog evaluated); runs in the [browser](https://w3id.org/force/demo)                  | [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project <br/> maintainer: [Wout Slabbinck](mailto:wout.slabbinck@ugent.be) |
| [Open Digital Rights Enforcement (ODRE) Framework](https://github.com/ODRE-Framework/odre-framework) | An open implementation of an ODRL Evaluator in multiple languages. <br> there is [ODRE for Java](https://github.com/ODRE-Framework/odre-java) and [ODRE for Python](https://github.com/ODRE-Framework/odre-python)                      | [OEG](https://oeg.fi.upm.es/) from [UPM](https://www.upm.es/) <br> maintainer: Andrea Cimmino                                                              |
| [ODRL-PAP](https://github.com/wistefan/odrl-pap)                                                     | Evaluates ODRL policies by translating them to [Rego policies](https://www.openpolicyagent.org/docs/policy-language), which are then executed by the [Open Policy Agent (OPA)](https://www.openpolicyagent.org/).  <br> Written in Java | Created for the [DOME-marketplace](https://dome-marketplace.eu/about) project                                                                              |
| [Odrl-manager](https://github.com/Prometheus-X-association/odrl-manager)                             | A library designed to facilitate the interpretation and evaluation of ODRL (Open Digital Rights Language) policies in JSON format.     <br> written in Node.js                                                                          | Prometheus-X                                                                                                                                               |
| [MOSAICrOWN policy engine](https://github.com/mosaicrown/policy-engine)                              | Parses and evaluates MOSAICrOWN policies, which uses as basis ODRL, but adds purpose as a first class citizen at rule level.<br> Written in Python                                                                                      | Created for the [MOSAICrOWN](https://cordis.europa.eu/project/id/825333) project (H2020)                                                                   |
| [MYDATA Control Technologies](https://git.iese.fraunhofer.de/mydata)                                 | Transforms ODRL policies to the custom XML-based MYDATA policy and evaluates the latter <br> Written in Java                                                                                                                            | Fraunhofer                                                                                                                                                 |
| [Gaia-X Wizard (PDP) Policy Stepper](https://wizard.lab.gaia-x.eu/policyStepper)                     | A proof of concept for policy negotiation using ODRL Offer, ODRL Request and Verifiable Credentials [Gitlab](https://gitlab.com/gaia-x/lab/gaia-x-onboarding-prototypes/gx-signing-tool)                                                | Gaia-X Lab Team<br> maintainer: [Yassir Sellami](mailto:yassir.sellami@gaia-x.eu)                                                                          |
| [Polival](https://codeberg.org/elbtech/Polival)                                                      | Policy and semantic web evaluation <br> Written in Rust and SPAQRL                                                                                                                                                                      | [Elbtech](https://elbtech.dev/) <br> maintainer: Richard Stoffels                                                                                          |


### Frameworks using ODRL

- [ODRL-Test-Suite](https://w3id.org/force/test-suite)
  - Software that can execute, validate and measure the compliance of an ODRL evaluator over a set of test cases. The test case consists of inputs (a policy, a request and the state of the world) and the expected outcome ([Compliance Report Model](https://w3id.org/force/compliance-report)).
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project (maintainer: [Wout Slabbinck](mailto:wout.slabbinck@ugent.be)).
- [User-Managed Access (UMA) server](https://github.com/SolidLabResearch/user-managed-access)
  - A [User-Managed Access](https://docs.kantarainitiative.org/uma/wg/rec-oauth-uma-grant-2.0.html) infrastructure where the Authorization Server (AS) uses the [ODRL Evaluator](https://w3id.org/force/evaluator) as a Policy engine (Policy Decision Point)
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project.
- [FORCE specification suite](https://w3id.org/force)
  - The Framework for ODRL Rule Compliance through Evaluation (FORCE) specification suite is designed to assist in ODRL policy development and enhance comprehension of ODRL evaluation outputs. It also enables experimentation and prototyping of ODRL 3.0 proposals. The specification points to other relevant specifications for further details.
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) (maintainers: [Wout Slabbinck](mailto:wout.slabbinck@ugent.be) and [Beatriz Esteves](mailto:beatriz.esteves@ugent.be)).
- [FORCE UI](https://w3id.org/force/demo)
  - The FORCE Web editor is a user interface developed with as goal aiding understanding of ODRL Policy Evaluation and experimenting with new features for ODRL.
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) (maintainer: [Wout Slabbinck](mailto:wout.slabbinck@ugent.be)).
- [dokieli](https://dokie.li/)
  - A client-side editor and browser extension (an [authoring tool](https://www.w3.org/TR/ATAG/#def-Authoring-Tool)) for decentralised article publishing, annotations, and social interactions. ([Source](https://git.dokie.li/))
  - Users can check whether storage policies are compatible with their preferred policies to guide their choices.
  - The user interface enforces resource policies by disabling actions such as printing, archiving, transforming, exporting, modifying, reproducing, or versioning.
  - Created and maintained by [Sarven Capadisli](https://csarven.ca/#i) (@csarven), [Virginia Balseiro](https://virginiabalseiro.com/#me) (@VirginiaBalseiro), and community.
- [LOAMA](https://github.com/SolidLabResearch/loama/tree/feat/odrl): Low-code ODRL Access Management Application
  - Web User Interface to manage ODRL policies in decentralized ecosystems. *Currently only with aforementioned [UMA Server](https://github.com/SolidLabResearch/user-managed-access)*
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project (maintainer: [Wout Slabbinck](mailto:wout.slabbinck@ugent.be)).
- [Gaia-X Wizard](https://wizard.lab.gaia-x.eu/development)
  - A web interface that contains ODRL Policy Evaluation. In addition to playground capabilities which allows you to obtain [Verifiable Credentials](https://www.w3.org/TR/vc-data-model-2.0/) that attest Gaia-X compliance. It uses those credentials as Attribute Based Access Control (ABAC) in ODRL Policies.
  - This is based on the [ODRL VC Profile](https://gitlab.com/gaia-x/lab/policy-reasoning/odrl-vc-profile)
  - Maintained by [Yassir Sellami](mailto:yassir.sellami@gaia-x.eu)
- [odrl-evaluation-engine-testbed (Work in progress)](https://gitlab.com/gaia-x/lab/policy-reasoning/odrl-toolbox/-/tree/main/odrl-evaluation-engine-testbed)
  - The ODRL Evaluation testbed provides a basic level tests and compliance check for an ODRL evaluation engine.
  - Maintained by [Yassir Sellami](mailto:yassir.sellami@gaia-x.eu)
- [Eclipse Dataspace Connector (EDC)](https://github.com/eclipse-edc/Connector)
  - Implementation of a Dataspace Connector as defined by the [Dataspace Protocol (DSP)](https://eclipse-dataspace-protocol-base.github.io/DataspaceProtocol/) (see DSP in the [protocols section](#protocols-that-point-to-odrl)). In the control plane (the layer that deals with the contracts over the data), ODRL is used.
- [Solid Agent UCP demo](https://github.com/SolidLabResearch/Solid-Agent/tree/feat/sosy/documentation/ucp)
  - a Web agent-based solution where an agent decomposes ODRL policies into actionable tasks (such as granting and retracting access to resources) using declarative condition-action rules and takes care of executing such tasks, by modifying the Access Control Rules of [Solid](https://solidproject.org/TR/protocol) resources.
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project (maintainer: [Wout Slabbinck](mailto:wout.slabbinck@ugent.be)).
- [FIWARE Data Space Connector](https://github.com/FIWARE/data-space-connector/tree/main)
  - Implementation of the [DSBA Technical Convergence recommendations](https://data-spaces-business-alliance.eu/wp-content/uploads/dlm_uploads/Data-Spaces-Business-Alliance-Technical-Convergence-V2.pdf), related to dataspaces. It uses ODRL as one policy language in an XACML architecture, using the [ODRL-PAP](https://github.com/wistefan/odrl-pap) component.
- [sovity EDC Community Edition (EDC CE)](https://github.com/sovity/edc-ce/tree/main)
  - Extension of the [EDC](https://github.com/eclipse-edc/Connector)

### Protocols that point to ODRL

- [Dataspace Protocol (DSP)](https://eclipse-dataspace-protocol-base.github.io/DataspaceProtocol)
  - The Dataspace Protocol is a specification designed to facilitate interoperable data sharing between entities governed by usage control and based on Web technologies. For usage control and contracts, the ODRL Vocabulary is reused.
- [Eclipse Dataspace Decentralized Claims Protocol (DCP)](https://eclipse-dataspace-dcp.github.io/decentralized-claims-protocol/)
  - The DCP defines a set of protocols for asserting participant identities, issuing verifiable credentials, and presenting verifiable credentials using a decentralized architecture for verification and trust. 
    - Works orthogonally together with the DSP to solve the identity and trust gap.
- [Authorization for Data Spaces (A4DS)](https://spec.knows.idlab.ugent.be/A4DS/L1/latest/)
  - A [User-Managed Access](https://docs.kantarainitiative.org/uma/wg/rec-oauth-uma-grant-2.0.html) extension that uses ODRL as the policy language for usage control.
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project (maintainer: [Wouter Termont](mailto:wouter.termont@ugent.be)).

### ODRL utilities

- [MyData ODRL policy creator](https://odrl-pap.mydata-control.de/)
  - User interface to create ODRL (or [IDSA](https://international-data-spaces-association.github.io/DataspaceConnector/Documentation/v5/UsageControl)) policies in JSON-LD. Additionally, it provides a human readable snippet elaborating the policy.
- [ODRL Shape validation](https://github.com/woutslabbinck/ODRL-shape)
  - A repository that helps verify whether policies comply with the ODRL Information Model.
  It includes [SHACL](https://www.w3.org/TR/shacl/) (Shapes Constraint Language) shapes for ODRL, along with supporting code to execute SHACL validation locally.
- [ODRL Validation implementation](https://odrlapi.appspot.com/)
  - User interface for validating ODRL policies against the Information Model.
- [Deontic Policy Consistency Checker](https://knowledgeonwebscale.github.io/n3s-policy-consistency-checker/)
  - User interface to evaluate policies for internal inconsistencies. 
- [LLM4ODRL](https://github.com/Daham-Mustaf/LLM4ODRL)
  - An ontology-guided approach for converting instructions into ODRL usage policies using Large Language Models. The repository also contains [SHACL](https://www.w3.org/TR/shacl/) shapes for ODRL.
- [ODRL2SHACL](https://github.com/paolo7/ODRL2SHACL)
- [ODRL Toolbox ](https://gitlab.com/gaia-x/lab/policy-reasoning/odrl-toolbox)
  - A set of tools to validate, evaluate and check compliance for ODRL

## How to contribute

When there is something missing in this list, feel free to add it yourself by opening a [pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork).

<mark>Note</mark>: this document originated from [ODRL-Landscape](https://github.com/KNowledgeOnWebScale/ODRL-Landscape) by [Wout Slabbinck](mailto:wout.slabbinck@ugent.be) (part of the [KNowledge on Web Scale](https://knows.idlab.ugent.be/) research group).
