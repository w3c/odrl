## W3C Workshop on the Future of ODRL 2026 - Summary and Recommendations

The W3C Workshop on the Future of ODRL was held in London on 20–21 July 2026, bringing together participants from standards organisations, industry, academia and the broader policy, data and rights communities. The workshop was explicitly positioned as a turning point for ODRL: the community was being asked to consider what ODRL 3.0 should become, and whether a new W3C Working Group should be established to take that work forward.

The workshop covered media, core semantics, banking and finance, data spaces, legal and regulatory applications, new language features, and finally detailed planning for a future Working Group.

This report strongly supports the conclusion that the workshop reached substantial consensus on the direction of travel, although many technical questions remain to be resolved. The emerging vision is considerably broader than simply producing another revision of the ODRL vocabulary. ODRL 3.0 is being conceived as a foundation for machine-readable, interoperable and increasingly machine-actionable policies, capable of operating across sectors and integrating with complementary standards for identity, provenance, legal information, data spaces and digital contracts.

⸻

### Why ODRL 3.0 is needed now

The workshop opened by placing ODRL in historical context. ODRL began around 2000 and subsequently evolved through several versions before becoming a W3C Recommendation. The community emphasised that ODRL has continued to find practical applications, including the Open Mobile Alliance, IPTC RightsML, DCAT, the TDM Reservation Protocol and financial-market data profiles.

This growing adoption creates a new challenge. ODRL is no longer simply a specialist rights-expression language. It increasingly sits at the intersection of data governance, digital rights, legal compliance, provenance, AI, data spaces and automated usage control.

The workshop therefore identified five broad areas for future work:

1. Improve and extend the ODRL information model.
2. Extend the core vocabulary to address emerging requirements.
3. Develop useful profiles.
4. Establish clearer semantics and evaluation mechanisms.
5. Establish conformance procedures so that different implementations can reliably understand and process policies in the same way.

The workshop explicitly identifies improving the information model, extending the core vocabulary, developing useful profiles, and providing semantics and conformance procedures as key objectives for the future work.

This last point is particularly important. The workshop repeatedly returned to the idea that interoperability requires more than a common syntax.

⸻

### From policy expression to policy processing

One of the strongest themes of the workshop was the need to distinguish between describing a policy and processing a policy.

ODRL 2.2 provides a standard model for expressing policies, but the behaviour of software processing those policies is not sufficiently standardised. The workshop therefore discussed a future in which conformance would apply not merely to the structure of an ODRL policy but to the behaviour of software that consumes those policies.

Such software could include:

* Policy enforcement engines
* Access-control systems
* Monitoring systems
* Compliance checkers
* Policy importers and exporters
* Policy converters
* Policy visualisers
* Human-readable policy explainers
* Tools that translate between ODRL and other policy representations

The workshop explicitly identified these different categories of software as potential processors of ODRL policies. ODRLWS-complete.txt

The workshop’s emerging recommendation is that ODRL 3.0 should be grounded in use cases, with explicit requirements derived from those use cases, and conformance tests tied directly to those requirements.

That provides a much stronger engineering basis for the specification than simply adding features to the vocabulary.

⸻

### A much stronger semantics and conformance framework

Several presentations identified limitations in the current semantics of ODRL. Particular attention was given to collections, actions, constraints, temporal and spatial conditions, policy conflicts and deterministic evaluation.

For example, discussions around policy processing highlighted that ODRL policies can require multiple stages of instantiation and processing, rather than necessarily being evaluated in a single pass.

The workshop therefore points towards a more formal computational semantics for ODRL: given a policy and a defined state of the world, different implementations should be able to reach compatible conclusions.

This is closely connected to conformance testing.

The proposed approach is not simply to say that an implementation supports ODRL, but to define test cases with inputs and expected outputs. The test suite would provide evidence that an implementation actually satisfies the requirements.

The workshop also discussed the possibility of multiple conformance levels. A simple implementation might support a basic subset of ODRL suitable for straightforward permission/prohibition scenarios, while more sophisticated implementations could support additional semantics and domain-specific features.

This would help address one of the recurring criticisms of ODRL: that it can be unnecessarily complex for simple applications.

⸻

### ODRL needs to become easier to use

A particularly practical message came from the media and copyright communities.

People who need to express rights policies are often not ODRL experts and may not even be software developers. The workshop therefore discussed the importance of templates, higher-level interfaces and tooling that can make ODRL easier to use.

This suggests an important design principle for ODRL 3.0 - The specification should become easier to consume without necessarily making the underlying language less expressive.

Templates, variables, profiles, visual editors and higher-level abstractions can provide this usability layer.

The workshop therefore appeared to favour a layered architecture: a powerful underlying policy model combined with simpler domain-specific representations and tooling.

This also aligns with the proposal for modularisation. Rather than expecting every implementation to support the entire conceptual complexity of ODRL, the future specification could provide modules that can be combined with other standards and application domains.

⸻

### ODRL as a cross-sector “lingua franca”

Perhaps the most commercially significant theme was the idea of ODRL becoming a cross-sector policy language.

The workshop discussed how established communities such as media, music, news and data spaces already have highly developed standards for metadata, identifiers and business processes.

The problem occurs when assets cross those boundaries.

The workshop therefore explored whether ODRL could provide a common policy layer between otherwise specialised ecosystems. The challenge would not be to replace DDEX, IPTC RightsML or other standards, but to provide translation mechanisms and interoperability between them.

This suggests a major strategic opportunity for ODRL 3.0 -  Not another vertical rights standard, but a common policy interoperability layer across vertical standards.

Such an approach would allow specialised communities to retain their own domain vocabularies and workflows while using ODRL to express interoperable permissions, prohibitions, duties and constraints.

⸻

### Automated licensing and remuneration

The workshop pushed the vision of machine-actionable policies further into automated licensing and remuneration.

If an asset can be identified, its creator or rights holder authenticated, its usage policies discovered and its conditions interpreted by machines, then it becomes possible to automate aspects of licensing and remuneration.

A potential architecture could combine:

* Provenance and authenticity
* Attribution
* Verifiable credentials
* Asset identification and fingerprinting
* ODRL usage policies
* Pricing information
* Licensing agreements
* Automated payment mechanisms

The ultimate objective is to reduce the gap between using an asset and remunerating its creator.

Tokenisation was also raised as a possible area for future consideration. The workshop did not conclude that ODRL itself should become a token or payment language. Rather, it considered how ODRL policies might provide the machine-readable rules needed by systems that automate licensing and remuneration.

This should therefore be regarded as an important future use case rather than a settled ODRL 3.0 requirement.

⸻

### Data spaces, credentials and trust

Another major direction was integration with verifiable credentials and trusted identities.

The Gaia-X presentation demonstrated how ODRL can be combined with verifiable credentials to implement attribute-based access control. Credentials provide trusted attributes about participants, while ODRL expresses the policies governing access and usage.

This reinforces a broader architectural pattern emerging from the workshop:

* Identity --> Credentials --> Policy  --> Enforcement  --> Evidence

ODRL does not need to provide all of these functions itself. Instead, ODRL can serve as the policy layer within a wider ecosystem of interoperable standards.

This is particularly relevant to data spaces, where policy enforcement depends not only on the policy itself but also on trustworthy information about participants, assets and their respective authorities.

⸻

### Legal and regulatory policy

A second major expansion of scope concerned legal rules and regulatory compliance.

The workshop discussed work translating requirements from legislation and regulation into ODRL policy models. These models can then be processed by inference or compliance engines.

This raises an important question for ODRL 3.0 - Should ODRL remain primarily a language for usage policies, or should it become capable of representing a wider class of legal rights, obligations, delegations and authorities?

The discussion suggested that this deserves serious investigation.

Participants specifically discussed integration with LegalRuleML, LOMO and legal identifiers such as Akoma Ntoso and LegalDocML. The discussion recognised potential synergies between ODRL and legal-rule modelling while also highlighting the need to investigate mappings, gateways and possible information loss.

The emerging recommendation is therefore not necessarily to absorb legal-rule modelling into ODRL, but to investigate modular integration with established legal-policy standards.

⸻

### Requirements should drive the specification

One of the most valuable methodological outcomes was the emphasis on requirements engineering.

An experiment presented at the workshop used generative AI to analyse:

* GitHub issues
* Research papers
* Public ODRL mailing-list discussions

The purpose was to extract candidate requirements from the history of ODRL discussions since 2018.

These requirements were subsequently reviewed by humans and organised into clusters including:

* Formal semantics and evaluation
* Operationalisation
* Profiles
* Interoperability
* Specification and vocabulary quality

The transcript notes that approximately 30 requirements were identified, although not all are mutually compatible and not all should necessarily become requirements for ODRL 3.0.

The resulting principle is therefore:

* Use cases  --> Requirements --> Specification design  --> Implementations  --> Conformance tests

This is arguably the most important process recommendation from the workshop.

The use of generative AI was presented as a valuable requirements-discovery and brainstorming technique, but the workshop also made clear that human review and judgement remain necessary.

⸻

### Proposed direction for the new W3C Working Group

The workshop concluded with considerable consensus that the next step should be the creation of a new W3C Working Group focused on ODRL 3.0.

The intended process is the normal W3C Recommendation track:

1. Develop a Working Group charter.
2. Develop use cases and requirements.
3. Produce Working Drafts.
4. Develop implementations.
5. Develop a comprehensive test suite.
6. Progress towards Candidate Recommendation.
7. Demonstrate the required implementation experience.
8. Progress to Proposed Recommendation.
9. Complete formal W3C Advisory Committee review.
10. Publish the resulting specification(s) as W3C Recommendations.

The workshop explicitly emphasised the importance of requirements, independent implementations and testing as part of this process.

The workshop’s closing discussion confirmed that the Workshop chairs would prepare a workshop report and draft Working Group charter. The intention was to socialise the charter at TPAC 2026 in Dublin, with the objective of moving into the next phase of ODRL 3.0 by the end of 2026.

⸻

### Key Recommendations Emerging from the Workshop

The workshop’s outcomes can be distilled into ten principal recommendations:

1 -  Establish the new W3C ODRL 3.0 Working Group

There was substantial consensus that the core ODRL community activities move from the current Community Group environment into a formal W3C Working Group capable of producing one or more new W3C Recommendations.

2 -  Start with use cases and explicit requirements

The Working Group should begin with real-world use cases and derive explicit, testable requirements from them rather than beginning with an unconstrained list of vocabulary changes.

3 - Strengthen the formal semantics of ODRL

ODRL 3.0 should provide clearer semantics for policy evaluation, including the treatment of constraints, actions, temporal conditions, collections, conflicts and other complex policy constructs.

4 -  Define conformance for policy-processing software

Conformance should address the behaviour of software processing ODRL policies, rather than being limited to syntactic or structural validity.

5 -  Develop a comprehensive conformance test suite

Requirements should be mapped to test cases with defined inputs and expected results. This should provide the basis for demonstrating interoperability.

6 -  Adopt modular and potentially multi-level conformance

ODRL should support simple use cases without forcing every implementation to support the full complexity of the language. Profiles and modularisation could provide different levels of capability.

7 - Improve usability

Templates, profiles, variables, visual interfaces, wizards and other higher-level tooling should make ODRL accessible to users who do not need to understand the full underlying information model.

8 - Position ODRL as an interoperability layer

ODRL should work alongside established sector-specific standards rather than attempting to replace them. Mappings, parsers and translators should enable policies to move between ODRL and domain-specific standards.

9 -  Investigate integration with complementary standards

The future work should investigate relationships with:

* Verifiable Credentials
* Data spaces
* LegalRuleML
* JPEG Trust
* Data Contracts
* Provenance standards
* Identity frameworks
* Domain-specific rights standards

10 -  Explore future machine-actionable applications

The community should investigate applications including automated compliance, automated licensing, remuneration, data governance, AI governance and potentially tokenised transactions, while carefully distinguishing exploratory use cases from the normative scope of ODRL 3.0.

⸻

### Overall Assessment

The workshop marks an important change in the character of ODRL.

The original ODRL problem was essentially:

*“How can we express rights and permissions in a machine-readable form?”*

The emerging ODRL 3.0 question is much broader:

*“How can interoperable policy information be represented, interpreted, evaluated and acted upon by machines across heterogeneous digital policy ecosystems?”*

That is a considerably more ambitious proposition.

The strongest message from the two days was not that ODRL needs a long list of new vocabulary terms. Rather, it needs to become a more rigorous, modular, interoperable and implementable digtial policy framework.

The future specification should be grounded in real use cases, supported by formal requirements, and validated through implementations and conformance testing.

At the same time, the workshop demonstrated that there is already a substantial ecosystem into which ODRL 3.0 could fit:

* JPEG Trust and digital media
* DDEX and music
* IPTC/RightsML and news
* Gaia-X and data spaces
* Data contracts
* AI and regulatory compliance
* Verifiable credentials
* Legal information systems

This makes the timing particularly significant.

The workshop did not simply ask:

*“What features should ODRL 3.0 have?”*

It effectively asked:

*“What role should ODRL play in the emerging machine-readable policy infrastructure of the Web?”*

The consensus emerging from the workshop appears to be that ODRL should become a common digtial policy language and interoperability layer, capable of connecting specialised domain standards while providing a stronger semantic and computational foundation than ODRL 2.2 currently provides.

The next critical step is therefore to turn this broad consensus into a precise W3C Working Group charter, use-case and requirements document, and ultimately a technically coherent ODRL 3.0 architecture.

The workshop concluded with the view that there was sufficient consensus to proceed, and that the immediate task was now to document the outcomes and move into the formal W3C process.


⸻


*NOTE: This report was primarily created with a GenAI tool from the raw transcripts of the 2 day workshop.*
