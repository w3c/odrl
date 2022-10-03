Author: Nicoletta Fornara, Universita' della Svizzera italiana, Lugano, Svizzera.

**Scenario 1 Policy Monitoring**: autonomous agents intect in an open interaction system and perform various type of actions, those actions are represented in a world state. A set of norms (N) regulate the behaviour of those agents. Policy monitoring consists of automatic computation of fulfilment or violation of norms in N based on the actions of agents.

**Goal 1: Check whether the behavior of agents constrained by ODRL policies is compliant with those policies**

**Scenario 2 Access Control to digital resources**:

**Goal 2:**

The semantics of an ODRL policiy is given by the semantics of its rules. The semantics of one ODRL Rule is expressed by:

1. Its **activation condition**: when something happens or a certain state of affairs is satisfied the rule becomes active or in force. In ODRL 2.2 the activation condition must be expressed by specifying the conditions applicable to a Rule by means of a set of constraints.
2. The **class of actions** regulated by the rule: when an instance of the class of actions regulated by the rule is performed with all refinements satisfied, the rule is fulfilled or violated on the basis of its type.
3. Its **type**: if the rule is a duty (or obligation), performing an instance of the **class of actions** regulated by the rule brings about a fulfillment. If the type is prohibition, performing an instance of the class of actions regulated by the rule brings about a violation. If the type is permission ...

In order to check whether the **activation condition** is satisfied it must be evaluated on the **state of the world**.

In order to check whether an individual belonging to the  **class of actions** regulated by the rule is actually performed there must be an individual in the **state of the world** that belongs to the class of actions. 

Therefore it is crucial that the activation condition and the class of actions regulated by the rule are expressed with an **ontology** that can be aligned or matched with the **ontology** used for expressing the state of the worl.

**PROBLEMS OF ODRL 2.2**

**PROBLEM 1**: 
In ODRL 2.2 the **class** of actions regulated by one rule is expressed using an **individual** belonging to the odrl:Action class and the class of actions is constrained using a refinement (which is an instance of the odrl:Constraint class). It is not easy to automatically translate such an expression (an individual) into the description of a **class** of actions regulated by the rule. Therefore, it is not easy to perform a class membership test for computing the fulfillment or violation of the rule. 

**PROBLEM 2**: Defining a new constraint language is not one of the goals of the ODRL working group, it is better to reuse an existing one.

**PROBLEM 3**: When a new Rule is formalized using ODRL 2.2, in the definition of its Refinement component, it is possible to use a leftOperand propery that is not meaningful for the action refined, for example it is possible to use the "version" leftoperand for the "display" action. 

**Running Example 1**

Suppose we want to write the policy that contains the following rule: "the permission for everybody to display the movie http://example.com/asset:9898.movie in Germany" (this example is taken from Example 1.2A in https://w3c.github.io/odrl/bp/#examples): 

``` 
{
 "@context": "http://www.w3.org/ns/odrl.jsonld",
 "@type": "Set",
 "uid": "http://example.com/policy:1010",
 "permission": [{
 	"target": "http://example.com/asset:9898.movie",
	"action": "display",
	"constraint": [{
           "leftOperand": "spatial",
           "operator": "eq",
           "rightOperand":  "https://www.wikidata.org/wiki/Q183",
	   "comment": "i.e Germany"
       }]
 }]
}
```
       
**SOLUTION TO PROBLEM 3**:  

Define the following ontology for expressing the rules inside policies and the state of the world where the real actions of the agents are represented:
 - the odrl:Display class is sublcass of the odrl:Action class
 - the object property odrl:spatial has as domain the class odrl:Action and as range a class odrl:State
 - the object property odrl:target has as domain the class odrl:Action (instead of odrl:Policy or odrl:Rule).

For example the ontolgy could contain the following information: 
- Robert performs a display action of the movie 9898.movie in Germany. 
- Anna performs a display action of the movie 9898.movie in Switzerland.
  
 **Solution TO PROBLEM 1 and 2**:
 
Use SHACL (Shapes Constraint Language) for describing the class of actions regulated by one ODRL Rule. 
References for SHACL: https://www.w3.org/TR/shacl; https://www.w3.org/TR/shacl-af/#rules

This is a SHACL shape that checks whether a focus node (in this case any instance of type odrl:Display class) conforms to the **state constraints** (having as target "http://example.com/asset:9898.movie" and being performed in Germany):

```
ex:SampleShape a sh:NodeShape ;
        sh:targetClass odrl:Display ;
        sh:property [
                sh:path odrl:spatial ;
                sh:hasValue "Germany" ;
                sh:minCount 1 ;
                sh:maxCount 1;
        ] ;
        sh:property [
                sh:path odrl:target ;
                sh:hasValue <http://example.com/asset:9898.movie>;
                sh:minCount 1 ;
                sh:maxCount 1;
        ] .
```

If it is required to get all actions that conform to those constraints (and not use any of SHACL's Advanced Features https://www.w3.org/TR/shacl-af/#SPARQLTarget) it is possible to get them like this:

```
ex:SampleShape a sh:NodeShape ;
        sh:targetClass odrl:Display ;
        sh:not [
                sh:and (
                  [
                    sh:property [
                      sh:path odrl:spatial ;
                      sh:hasValue "Germany" ;
                      sh:minCount 1 ;
                      sh:maxCount 1;
                    ]
                 ]
                 [
                   sh:property [
                    sh:path odrl:target ;
                    sh:hasValue <http://example.com/asset:9898.movie>;
                    sh:minCount 1 ;
                    sh:maxCount 1;
                ]
            ])
        ] .
```
i.e. state the negation which leads to all actions being reported that actually do conform to your initial query. (cf https://s.zazuko.com/2reFCP)

**OPEN PROBLEMS**:
 - How to connect a rule with a SHACL expression for expressing the **activation condition** of the rule; (For example for formalizing that the permission in Example 1 is valid between the first and the fifth of July 2022).

- How to connect a rule with a SHACL expression used to formalize the **class of actions regulated by the rule**; Is it ok to treat it as a text?

- How to use a SHACL expression for constraining an asset or a party like in ODRL 2.2?

- What ontology do we want to use for formalizing the ODRL examples? (for example is it possible to use the ODRL2.2 vocabulary?).

**References on policies monitoring and compliance checking**

N. Fornara and M. Colombetti. Using Semantic Web Technologies and Production Rules for Reasoning on Obligations, Permissions, and Prohibitions. AI Communications, vol. 32, no. 4, pp. 319-334, 2019. https://people.lu.usi.ch/fornaran/AIComm2019/AIComm32(2019)_Fornara.pdf

M. Sensoy, T. J. Norman, W. W. Vasconcelos, K. P. Sycara, OWL-POLAR: A framework for semantic policy representation and reasoning, J. Web Sem. 12 (2012) 148–160. URL:
https://doi.org/10.1016/j.websem.2011.11.005

N. Fornara, S. Roshankish, and M. Colombetti (2021) A Framework for Automatic Monitoring of Norms that regulate Time Constrained Actions. International Workshop on Coordination, Organizations, Institutions, Norms and Ethics for Governance of Multi-Agent Systems (COINE), co-located with AAMAS 2021, London, UK, 3rd May, 2021. https://arxiv.org/pdf/2105.00200.pdf

De Vos M., Kirrane S., Padget J., Satoh K. (2019) ODRL Policy Modelling and Compliance Checking. In: Fodor P., Montali M., Calvanese D., Roman D. (eds) Rules and Reasoning. RuleML+RR 2019. Lecture Notes in Computer Science, vol 11784. Springer, Cham. https://doi.org/10.1007/978-3-030-31095-0_3

H. Dibowski, S. Schmid, Y. Svetashova, C. Henson, T. Tran. Using Semantic Technologies to Manage a Data Lake: Data Catalog, Provenance and Access Control. In T. Liebig, A. Fokoue, Z. Wu, editors, Proceedings of the 12th International Workshop on Scalable Semantic Web Knowledge Base Systems co-located with 19th International Semantic Web Conference (ISWC 2020), Athens, Greece, November 2, 2020. Volume 2757 of CEUR Workshop Proceedings, pages 65-80, CEUR-WS.org, 2020. http://ceur-ws.org/Vol-2757/SSWS2020_paper5.pdf

ODRL Regulatory Compliance Profile Unofficial Draft 10 August 2020 https://ai.wu.ac.at/policies/orcp/regulatory-model.html

Wiki of the The Permissions and Obligations Expression (POE) Working Group. Discussion on Policy Inference. https://www.w3.org/2016/poe/wiki/Policy_Inference#Semantics_of_Action_Relations

Policy Evaluator Wiki discussion on the need of checking the activation of policies https://www.w3.org/2016/poe/wiki/Evaluator

The PROV Ontology (PROV-O) provides a set of classes, properties, and restrictions that can be used to represent and interchange provenance information generated in different systems and under different contexts. https://www.w3.org/TR/prov-o/

DALICC is a software framework that supports the automated clearance of rights https://www.dalicc.net/

The SPECIAL Policy Log Vocabulary: A vocabulary for privacy-aware logs, transparency and compliance - version 1.0 https://ai.wu.ac.at/policies/policylog/

-----------------------------

**Meeting on ODRL Semantics:**

1. Thursday 1st April 2021
2. Tueasday 11th May 2021
3. Monday 21st June 2021
4. Monday 27th September 2021

**Participants:**
  
  1. Nicoletta Fornara (nicoletta.fornara@usi.ch),  Univeristà della Svizzera italiana, Lugano, Switzerland
  2. Soheil Roshanskish (Ph.D. student) (soheil.roshanskish@usi.ch), Univeristà della Svizzera italiana, Lugano, Switzerland
  3. Víctor Rodríguez Doncel (vrodriguez@fi.upm.es), Ontology Engineering Group, Departamento de Inteligencia Artificial – Universidad Politécnica de Madrid (UPM)
  4. Rana Saniei (Ph.D. student) (r.saniei@upm.es), Ontology Engineering Group, Departamento de Inteligencia Artificial – Universidad Politécnica de Madrid (UPM)
  5. Beatriz Esteves (Ph.D. student) (beatriz.gesteves@upm.es), Ontology Engineering Group, Departamento de Inteligencia Artificial – Universidad Politécnica de Madrid (UPM)
  6. Benedict Whittam Smith, (ben@deonticdata.com) Refinitiv an LSEG (London Stock Exchange Group)
  7. (Staring from September 2021) Harshvardhan J. Pandit (me@harshp.com) postoc at Trinity College Dublin.
  8. (Starting from January 2022) Simon Steyskal (simon.steyskal@siemens.com) Siemens AG Austria Vienna.

 We can also send a message in the ODRL mailing list community group.
 
