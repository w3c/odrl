     
**Requirement: Monitoring or compliance checking of ODRL policies**

1. Semantics of the **activation condition**: when something happens or a certain state of affairs is satisfied the policy becomes active or in force. In ODRL 2.2 the activation condition is expressed using a constraint.

2. Semantics of the **policy**: it depends on the type of the policy, i.e. duty (obligation), prohibition, or permission. Computing the fulfilment or violation of policies requires to check if a real action belongs to the **class of actions** regulated by the policy (testing class membership).

**PROBLEM**: 

In ODRL 2.2 the activation condition of the policy and the class of actions regulated by the policy are expressed using individuals, they are not expressed using classes. This is probably due to the fact that the value of the "action" property cannot be a class in OWL 2.
This creates a problem when there is the requirement to match the description of the class of actions regulated by one policy with real actions.

**Example**

For example in the following ODRL policy (taken from the ODRL Implementation Best Practices (https://w3c.github.io/odrl/bp/#examples)) the class of actions regulated is the display of the specific movie asset:9898.movie in Germany. This class is represented with the "display" individual that belongs to the ordl:Action class (it is also possible to constraint the class of the regulated actions by using the odrl:constraint or odrl:refinement property).

The following policy express: "the permission for everybody to display the movie http://example.com/asset:9898.movie in Germany".
      
    Example 1.2A in ODRL 2.2
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


**Testing class membership**

Approaches for testing class membership:
   
  1. Translating the class of actions described in one ODRL policy (using an individual) into a SPARQL query and searching the instances of the class of actions regulated by the policy.
  2. Translating the class of actions described in one ODRL policy into a production rule and searching the matching between the class of actions regulated by the policy and the real actions performed by the agents.

In both approaches we need to define an Action Ontology with a hierarchy of classes that can be created using the ODRL Vocabulary https://www.w3.org/TR/odrl-vocab/.

**Question**: Is it possible to automatically translate the class of actions described in one ODRL policy into a SPARQL query or production rule?

If yes, we are able to compute the fulfilment or violation of policies. 

If no, we need to propose a new version of the ODRL language!!


**Could you please write here your opinion?**

..............



**State of the art on policies monitoring**

N. Fornara and M. Colombetti. Using Semantic Web Technologies and Production Rules for Reasoning on Obligations, Permissions, and Prohibitions. AI Communications, vol. 32, no. 4, pp. 319-334, 2019. https://people.lu.usi.ch/fornaran/AIComm2019/AIComm32(2019)_Fornara.pdf

M. Sensoy, T. J. Norman, W. W. Vasconcelos, K. P. Sycara, OWL-POLAR: A framework for semantic policy representation and reasoning, J. Web Sem. 12 (2012) 148–160. URL:
https://doi.org/10.1016/j.websem.2011.11.005

N. Fornara, S. Roshankish, and M. Colombetti (2021) A Framework for Automatic Monitoring of Norms that regulate Time Constrained Actions. International Workshop on Coordination, Organizations, Institutions, Norms and Ethics for Governance of Multi-Agent Systems (COINE), co-located with AAMAS 2021, London, UK, 3rd May, 2021. https://arxiv.org/pdf/2105.00200.pdf

Wiki of the The Permissions and Obligations Expression (POE) Working Group. Discussion on Policy Inference. https://www.w3.org/2016/poe/wiki/Policy_Inference#Semantics_of_Action_Relations

Policy Evaluator Wiki discussion on the need of checking the activation of policies https://www.w3.org/2016/poe/wiki/Evaluator

The PROV Ontology (PROV-O) provides a set of classes, properties, and restrictions that can be used to represent and interchange provenance information generated in different systems and under different contexts. https://www.w3.org/TR/prov-o/

DALICC is a software framework that supports the automated clearance of rights https://www.dalicc.net/
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

We can invite:
   - Simon Steyskal (simon.steyskal@gmail.com) Ph.D. student at TU Vienna
   - Harshvardhan J. Pandit (me@harshp.com) postoc at Trinity College Dublin
  
 We can also send a message in the ODRL mailing list community group.
 
