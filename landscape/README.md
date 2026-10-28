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
For example, dataspaces mention to use ODRL as usage control policy language for enforcement (both Gaia-X and IDSA). Within the [Solid](https://solidproject.org/TR/protocol) project, several people advocated to use ODRL for data usage control (see github issue [SAI-55](https://github.com/solid/authorization-panel/issues/55)).

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

| Name                                                                                                 | Context                                                                                                                                                                                                                                                     | Authors                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [FORCE Evaluator](https://w3id.org/force/evaluator)                                                   | An open implementation of an ODRL Evaluator that evaluates ODRL policies by generating Compliance Reports.<br> Written in Node.js and [Notation3](https://w3c-cg.github.io/N3/spec/) (prolog evaluated); runs in the [browser](https://w3id.org/force/demo) | [KNoWS](https://knows.idlab.ugent.be/), IDLab, Ghent University |
| [Open Digital Rights Enforcement (ODRE) Framework](https://github.com/ODRE-Framework/odre-framework) (2024) | An open implementation of an ODRL Evaluator in multiple languages. <br> there is [ODRE for Java](https://github.com/ODRE-Framework/odre-java) and [ODRE for Python](https://github.com/ODRE-Framework/odre-python)                                          | [OEG](https://oeg.fi.upm.es/) from [Universidad Politécnica de Madrid](https://www.upm.es/) <br> maintainer: Andrea Cimmino                                                              |
| [ODRL Engine](https://github.com/DIPS-Tools/ODRL-Engine) (2026)                                             | An open implementation of an ODRL Evaluator supporting both Monitoring and Access Control scenarios, evaluating ODRL policies against a defined State of the World and/or access request, producing an evaluation report including allowed/not allowed results. Has [API](https://dips.soton.ac.uk/odrl-engine/api/docs) and [GUI](https://dips.soton.ac.uk/odrl-engine/odrl-engine-dashboard/) support. <br> Written in Python                                                                                      | University of Southampton                                                                                                                                  |
| [ODRL-PAP](https://github.com/wistefan/odrl-pap)                                                     | Evaluates ODRL policies by translating them to [Rego policies](https://www.openpolicyagent.org/docs/policy-language), which are then executed by the [Open Policy Agent (OPA)](https://www.openpolicyagent.org/).  <br> Written in Java                     | Created for the [DOME-marketplace](https://dome-marketplace.eu/about) project                                                                              |
| [Odrl-manager](https://github.com/Prometheus-X-association/odrl-manager)                             | A library designed to facilitate the interpretation and evaluation of ODRL (Open Digital Rights Language) policies in JSON format.     <br> written in Node.js                                                                                              | Prometheus-X                                                                                                                                               |
| [MOSAICrOWN policy engine](https://github.com/mosaicrown/policy-engine)                              | Parses and evaluates MOSAICrOWN policies, which uses as basis ODRL, but adds purpose as a first class citizen at rule level.<br> Written in Python                                                                                                          | Created for the [MOSAICrOWN](https://cordis.europa.eu/project/id/825333) project (H2020)                                                                   |
| [MYDATA Control Technologies](https://git.iese.fraunhofer.de/mydata)                                 | Transforms ODRL policies to the custom XML-based MYDATA policy and evaluates the latter <br> Written in Java                                                                                                                                                | Fraunhofer                                                                                                                                                 |
| [Gaia-X Wizard (PDP) Policy Stepper](https://wizard.lab.gaia-x.eu/policyStepper) (2024)              | A proof of concept for policy negotiation using ODRL Offer, ODRL Request and Verifiable Credentials [Gitlab](https://gitlab.com/gaia-x/lab/gaia-x-onboarding-prototypes/gx-signing-tool)                                                                    | Gaia-X Lab Team<br> maintainer: [Yassir Sellami](mailto:yassir.sellami@gaia-x.eu)                                                                          |
| [Polival](https://codeberg.org/elbtech/Polival)                                                      | Policy and semantic web evaluation <br> Written in Rust and SPAQRL                                                                                                                                                                                          | [Elbtech](https://elbtech.dev/) <br> maintainer: Richard Stoffels                                                                                          |
| [Evaluator in JavaScript (IPTC)](https://github.com/nitmws/odrl-wprofile-evaltest1/tree/master/evaluator) (2017)                                                                           | An ODRL evaluator from 2017, developed for an ODRL profile experiment. <br> Written in JavaScript | [IPTC](https://iptc.org/) (International Press Telecommunications Council) |
| [Marketdata](https://marketdata.md/) (2024)                                                                 | Listed as an ODRL implementation (2024) in the W3C ODRL Community Group implementations page; no further details given | Joshua Cornejo |
| [Ruby-odrl](https://github.com/cbeer/ruby-odrl)                                                      | Library for creating and evaluating ODRL (1.1) documents, acting as a policy decision point. <br> Written in Ruby | [Chris Beer](https://github.com/cbeer) |

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
- [FIWARE Data Space Connector](https://github.com/FIWARE/data-space-connector)
  - Implementation of the [DSBA Technical Convergence recommendations](https://data-spaces-business-alliance.eu/wp-content/uploads/dlm_uploads/Data-Spaces-Business-Alliance-Technical-Convergence-V2.pdf), related to dataspaces. It uses ODRL as one policy language in an XACML architecture, using the [ODRL-PAP](https://github.com/wistefan/odrl-pap) component.
- [sovity EDC Community Edition (EDC CE)](https://github.com/sovity/edc-ce)
  - Extension of the [EDC](https://github.com/eclipse-edc/Connector)
- [O-prime](https://github.com/ahmadvoc12/Solid-Monitoring-Addons)
  - Framework for transparent monitoring of personal data usage, policy violation detection, and provenance tracking in decentralized [Solid](https://solidproject.org/TR/protocol) ecosystems.

### Protocols that point to ODRL

- [Dataspace Protocol (DSP)](https://eclipse-dataspace-protocol-base.github.io/DataspaceProtocol): The Dataspace Protocol is a specification designed to facilitate interoperable data sharing between entities governed by usage control and based on Web technologies. For usage control and contracts, the ODRL Vocabulary is reused.
- [Eclipse Dataspace Decentralized Claims Protocol (DCP)](https://eclipse-dataspace-dcp.github.io/decentralized-claims-protocol/): The DCP defines a set of protocols for asserting participant identities, issuing verifiable credentials, and presenting verifiable credentials using a decentralized architecture for verification and trust. 
  - Works orthogonally together with the DSP to solve the identity and trust gap.
- [Authorization for Data Spaces (A4DS)](https://spec.knows.idlab.ugent.be/A4DS/L1/latest/) (2025): A [User-Managed Access](https://docs.kantarainitiative.org/uma/wg/rec-oauth-uma-grant-2.0.html) extension that uses ODRL as the policy language for usage control.
  - Created by [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project (maintainer: [Wouter Termont](mailto:wouter.termont@ugent.be)).
- [Linked Web Storage Protocol 1.0 (LWS)](https://www.w3.org/TR/lws10-core/) (2026): A W3C Working Draft of the Linked Web Storage Working Group (editors: Jesse Wright and Erich Bremer). Its Access Profile (`lws:AccessProfile`) is normatively based on the [ODRL Information Model 2.2](https://www.w3.org/TR/odrl-model/) and the [ODRL Vocabulary & Expression 2.2](https://www.w3.org/TR/odrl-vocab/), both normative references.
  - Servers must support the actions `read`, `modify` and `delete` (from the ODRL Vocabulary) and `create` (defined by LWS), which map to the HTTP methods.
  - Access policies have an assignee and optional targets (data resource, container or storage resource). Constraints follow the ODRL Constraint model (`leftOperand`, `operator`, `rightOperand`), with `client`, `format`, `type`, `purpose` and `dateTime` as required left operands.
- [Croissant 1.1](https://mlcommons.org/2026/02/croissant-1-1-standard/) (2026): The [MLCommons](https://mlcommons.org/) metadata format for machine learning datasets (announced 12 February 2026). It adds provenance, vocabulary linking, usage policies and support for complex data structures. Usage policies can be expressed with ODRL, as a finer-grained alternative to DUO consent codes. Embedding ODRL terms lets agents check automatically whether a proposed use is permitted.

### ODRL utilities

- [CODATA Policy Builder](https://odrl.dev.codata.org/policies): User interface to create and visualise ODRL policies in JSON-LD.
- [MyData ODRL policy creator](https://odrl-pap.mydata-control.de/): User interface to create ODRL (or [IDSA](https://international-data-spaces-association.github.io/DataspaceConnector/Documentation/v5/UsageControl)) policies in JSON-LD. Additionally, it provides a human readable snippet elaborating the policy. Created by the [Fraunhofer Institute](https://www.fraunhofer.de/).
- [ODRL Shape validation](https://github.com/woutslabbinck/ODRL-shape): A repository that helps verify whether policies comply with the ODRL Information Model.
  - It includes [SHACL](https://www.w3.org/TR/shacl/) (Shapes Constraint Language) shapes for ODRL, along with supporting code to execute [SHACL](https://www.w3.org/TR/shacl/) validation locally.
- [ODRL Validation implementation](https://odrlapi.appspot.com/) (2017): User interface for validating ODRL policies against the Information Model. Developed by Víctor Rodríguez-Doncel ([Universidad Politécnica de Madrid](https://www.upm.es/)) and [Wright State University](https://www.wright.edu/).
- [Deontic Policy Consistency Checker](https://knowledgeonwebscale.github.io/n3s-policy-consistency-checker/) (2025): User interface to evaluate policies for internal inconsistencies. Created by Patrick Hochstenbach, [KNoWS](https://knows.idlab.ugent.be/), IDLab, Ghent University.
- [LLM4ODRL](https://github.com/Daham-Mustaf/LLM4ODRL) (2024): An ontology-guided approach for converting instructions into ODRL usage policies using Large Language Models. The repository also contains [SHACL](https://www.w3.org/TR/shacl/) shapes for ODRL. Created by Daham Mustafa, Fraunhofer-Institut für Angewandte Informationstechnik FIT (Bonn).
- [ODRL2SHACL](https://github.com/paolo7/ODRL2SHACL)
- [ODRL Toolbox ](https://gitlab.com/gaia-x/lab/policy-reasoning/odrl-toolbox): A set of tools to validate, evaluate and check compliance for ODRL
- [bpmn2odrl](https://github.com/manabcodes/bpmn2odrl) (2026): Converts Business Process Model and Notation ([BPMN](https://www.bpmn.org/)) workflows into ODRL policies. Created by Meem Arafat Manab and team ([Universidad Politécnica de Madrid](https://www.upm.es/)).
- [BAMBON](https://github.com/isotiropoulos/BayesianNegotiator): A learning-based negotiator that automatically negotiates ODRL based on the constraints imposed by the involved parties.
- [ODRL Atomization](https://github.com/woutslabbinck/ODRL-Atomization): Transforms compact ODRL policies with composite rules into policies with atomic rules.
- [ODRL Validator](https://github.com/elenamolino/odrl-validator): Validates ODRL policies using [SHACL](https://www.w3.org/TR/shacl/) and detects policy conflicts with [Notation3](https://w3c-cg.github.io/N3/spec/) reasoning. Created by Elena Molino, [Universidad de Sevilla](https://www.us.es/).
- [Risk Detector Application (risk-e-tos)](https://github.com/isa-group/risk-e-tos): Explores ODRL policy risk assessment and mitigation suggestions using [Notation3](https://w3c-cg.github.io/N3/spec/) reasoning. Created by Elena Molino, [Universidad de Sevilla](https://www.us.es/).
- [ODRL Engine](https://github.com/DIPS-Tools/ODRL-Engine) (2026): The ODRL Engine includes the following utility tools: a generator of synthetic ODRL policies, a generator of synthetic States of the World objects, and an ODRL validator. 
- [ODRL Editor](https://github.com/DIPS-Tools/ODRL_Editor_Demo_v2): The ODRL Editor is a web based tool that facilitates the creation of ODRL Policies, it includes the dynamic loading of vocabularies (ODRL Profiles), a configurable UI, and its functionality can be embedded as an iFrame. A live version is hosted [here](https://dips.soton.ac.uk/odrl-editor-demo/).
- [ODRL/JPEG Trust Manifest](https://16.61.203.65/add-metadata): A demo that attaches ODRL policies to JPEG Trust manifests as metadata (hosted on a bare IP address, so no domain name).
- [ODRL License Platform (Encypher)](https://encypher.com/): A licensing platform that uses ODRL. A (free) account is needed to see the use of ODRL.
- [DALICC](https://github.com/dalicc/dalicc): The Data Licenses Clearance Center makes software and data licenses machine readable. Each license is modelled as an ODRL policy over a controlled vocabulary of actions, and an answer-set-programming reasoner (available through an [API](https://api.dalicc.net)) detects conflicts to decide whether a set of licenses can be combined. License data is CC BY 4.0. Created by Giray Havur and others, [Vienna University of Economics and Business](https://www.wu.ac.at/en/) (WU), Austria. Funded by the Austrian Research Promotion Agency (FFG) and netidee.
- [Policy Patterns for Usage Control in Data Spaces](https://github.com/fhstp/dataspaces-policies) (2023): A catalogue of about 22 ODRL usage-control policy patterns (e.g. time restriction, access count, rate limiting, billing, deletion, purpose limitation, encryption, anonymization, activity logging), each with an example policy in Turtle. Patterns are classified as preventive or detective and list the stakeholders and the PIP/PAP/PDP roles. It also provides an [ODRL profile for data spaces](https://w3id.org/dataspaces-policies/) (extra actions and operands) and an OWL ontology. Described in the [paper](https://arxiv.org/abs/2309.11289) by Tobias Dam, Andreas Krimbacher and Sebastian Neumaier ([FH St. Pölten](https://www.fhstp.ac.at/)), presented at the Fifth International Workshop on a Semantic Data Space for Transport at SEMANTiCS 2023. Licensed under GPL-3.0.
- [ODRL API (ODRLAPI)](http://oeg-upm.github.io/odrlapi/): Java API for manipulating ODRL 2.0 RDF expressions. By the [Ontology Engineering Group (OEG)](https://oeg.fi.upm.es/), Universidad Politécnica de Madrid. This API is old; for validation see the [ODRL Validation implementation](https://odrlapi.appspot.com/) above, which still works.
- [w3odrl21](https://github.com/xmljim/w3odrl21): Java library for parsing and serializing ODRL 2.1 to and from JSON and XML.
- [IPTC RightsML / ODRL JavaScript library](https://github.com/iptc/rightsml-dev/tree/master/rightsml-lib-js) and [experimental API](https://github.com/iptc/rightsml-dev/tree/master/licensed): tooling for ODRL 2.0/2.1 and RightsML by [IPTC](https://iptc.org/).

### Legacy implementations (ODRL 1.1)

- [OpenSDRM](http://sourceforge.net/projects/opensdrm/): Digital object rights management solution built on open-source components and open standards.
- [OpenIPMP](http://sourceforge.net/projects/openipmp): Open-source DRM project using numerous standards.
- [OMA DRM REL](https://en.wikipedia.org/wiki/OMA_DRM#Implementations_and_usage): The ODRL profile used in the Open Mobile Alliance DRM Rights Expression Language; the page lists commercial providers.
- [RightsPro](http://rightspro.com): Tool for creating licensing agreements and sending or receiving payment.

### Further resources

- [ODRL 2.2 implementation report](https://w3c.github.io/poe/test/implementors) (November 2017). Various profiles have been created since.
- [ODRL Profiles](https://www.w3.org/community/odrl/wiki/ODRL_Profiles) (W3C ODRL Community Group wiki).
- [Automated machine-readable data access agreements by applying ODRL to a FAIR Data Train](https://essay.utwente.nl/essays/103662) (2024): MSc thesis (Business Information Technology) by S.P. Veltmaat, [University of Twente](https://www.utwente.nl/). It uses ODRL to create machine-readable data access agreements in the FAIR Data Train framework, with scenarios and RDF agreements validated through stakeholder surveys in a real-world use case.
- Source of the above additions: [W3C ODRL Community Group implementations page](https://www.w3.org/community/odrl/implementations/). ODRE also has a [paper](https://arxiv.org/abs/2409.17602) and a [website](https://odre-framework.github.io/odre-framework/); the Gaia-X Policy Decision Point and the Ghent University ODRL Evaluator are already listed above.

## How to contribute

When there is something missing in this list, feel free to add it yourself by opening a [pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork).

<mark>Note</mark>: this document originated from [ODRL-Landscape](https://github.com/KNowledgeOnWebScale/ODRL-Landscape) by [Wout Slabbinck](mailto:wout.slabbinck@ugent.be) (part of the [KNowledge on Web Scale](https://knows.idlab.ugent.be/) research group).
