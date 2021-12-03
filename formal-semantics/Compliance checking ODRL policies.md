Author: Nicoletta Fornara, Universita' della Svizzera italiana, Lugano, Svizzera.

**Goal: monitor or control compliance with ODRL policies**

The semantics of ODRL policies is given by the semantics of:

1. Their **activation condition**: when something happens or a certain state of affairs is satisfied the policy becomes active or in force. In ODRL 2.2 the activation condition is expressed by specifying a constraint of a Rule.
2. The **class of actions** regulated by the policy: when an instance of the class of actions regulated by the policy is performed with all refinements satisfied, the policy is fulfilled or violated on the basis of its type.
3. Their **type**: if the type is duty (obligation) performing an instance of the **class of actions** regulated by the policy brings about a fulfillment, if the type is prohibition performing an instance of the class of actions regulated by the policy brings about a violation, if the type is permission ...


**PROBLEM 1**: 

In ODRL 2.2 the class of actions regulated by one policy is expressed using an individual of the class odrl:Action and the class of actions is constrained using a refinement (which is an instance of the odrl:Constraint class). It is not easy to automatically translate such an expression into a class of actions regulated by the policy and then perform a test of class membership.

**Example**
Suppose that I want to write the following policy: "the permission for everybody to display the movie http://example.com/asset:9898.movie in Germany". 
I have to create a refinement of the action "display" in the following way (this example is partially taken from Example 1.2A in https://w3c.github.io/odrl/bp/#examples): 

     {
      "@context": "http://www.w3.org/ns/odrl.jsonld",
      "@type": "Set",
      "uid": "http://example.com/policy:1010",
      "permission": [{
 	      "target": "http://example.com/asset:9898.movie",
	      "action": "display",
	      "refinement": [{
                  "leftOperand": "spatial",
                  "operator": "eq",
                  "rightOperand":  "https://www.wikidata.org/wiki/Q183",
	          "comment": "i.e Germany"
              }]
       }]
    }

Problem 1: the norm designer can use a leftOperand that is not meaningful for the "display" action, for example the "version" leftoperand.
Problem 2: how is it possible to perform a test of class membership? What is the class of actions regulated by the policy?

Solution 1: 
Define an ontology with the Display class that is sublcass of the odrl:Action class and the object property "spatial": odrl:Action -> State. 
We need to change the ODRL 2.2 model because instead of using the refinement property we can describe the actions regulated by the rule by using an anonymous individual that is an instance of the Display class having as value of the spacial property the state Germany, like here:

     {
      "@context": "http://www.w3.org/ns/odrl.jsonld",
      "@type": "Set",
      "uid": "http://example.com/policy:1010",
      "permission": [{
 	      "target": "http://example.com/asset:9898.movie",
	      "action": [{
	          "@type": Display,
		  "spatial": germany
              }]
       }]
    }


With this solution, it would be impossible to confuse a constraint of the rule (which usually is an activation condition or an expiration condition of the rule) with a refinement used for describing the class of actions regulated by the rule.

Solution 2:



Please let me know your opinion.





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
 
