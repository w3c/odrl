Author: Nicoletta Fornara, Universita' della Svizzera italiana, Lugano, Svizzera.

**Goal: monitor or control compliance with ODRL policies**

The semantics of ODRL policies is given by the semantics of:

1. Their **activation condition**: when something happens or a certain state of affairs is satisfied the rule inside a policy becomes active or in force. In ODRL 2.2 the activation condition is expressed by specifying a constraint of a Rule.
2. The **class of actions** regulated by the rule inside a policy: when an instance of the class of actions regulated by the rule is performed with all refinements satisfied, the rule is fulfilled or violated on the basis of its type.
3. Their **type**: if the rule is a duty (or obligation) performing an instance of the **class of actions** regulated by the rule brings about a fulfillment, if the type is prohibition performing an instance of the class of actions regulated by the rule brings about a violation, if the type is permission ...


**PROBLEM 1**: 

In ODRL 2.2 the **class** of actions regulated by one rule is expressed using an **individual** belonging to the odrl:Action class and the class of actions is constrained using a refinement (which is an instance of the odrl:Constraint class). It is not easy to automatically translate such an expression (an individual) into the description of a **class** of actions regulated by the rule and then perform a test of class membership for computing the fulfillment or violation of the rule. 
A second problem is that the norm designer who writes the policy using the ODRL policy language can in principle use in the refinement a leftOperand propery that is not meaningful for the  action refined, for example by using the "version" leftoperand for the "display" action.

**Example 1.1**

Suppose that I want to write the policy that contains the following Rule 1.1: "the permission for everybody to display the movie http://example.com/asset:9898.movie in Germany". 
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
   

**Solution 1**

Define an ontology with the Display class that is sublcass of the odrl:Action class and the object property "spatial": odrl:Action -> State. (By defining an ontology it is impossible to use a leftOperand that is not meaningful for the class of the action). We need to change the ODRL 2.2 model because instead of using the refinement property we can describe the actions regulated by the rule by using an anonymous individual that is an instance of the Display class having as value of the spacial property the country Germany, like here:

     {
      "@context": "http://www.w3.org/ns/odrl.jsonld",
      "@type": "Set",
      "uid": "http://example.com/policy:1010",
      "permission": [{
 	      "target": "http://example.com/asset:9898.movie",
	      "action": [{
	          "@type": "Display",
		  "spatial": "Germany"
              }]
       }]
    }


With this solution, it would be impossible to confuse a constraint of the rule (which usually is an activation condition or an expiration condition of the rule) with a refinement used for describing the class of actions regulated by the rule.

One drawback of solution 1 is that it is not easy to express certain constraints like ''less than'' or ''greater than''.

**Solution 2**

A second solution consists in expressing the class of actions regulated by one policy by using a conjunctive semantic formula over an ontology. 
Its syntax can be based on the Human Readable Syntax of the antecedent of SWRL rules https://www.w3.org/Submission/SWRL/#2.2 with the use of variables and the possibility to use built-ins for comparisons like swrlb:lessThan. The formalization of the Rule 1.0 (see above) becomes:


     {
      "@context": "http://www.w3.org/ns/odrl.jsonld",
      "@type": "Set",
      "uid": "http://example.com/policy:1010",
      "permission": [{
 	      "target": "http://example.com/asset:9898.movie",
	      "action": [{
	          Display(?a) and spatial(?a, germany)
              }]
       }]
    }


Problems:
1. The value of the property odrl:action is no longer an instance of the class odrl:Action. As a consequence, the rule (the permission) inside the policy is no longer an individual belonging to the class odrl:Rule.
2. Not all ODRL constraint operators can be represented right now using SWRL'a built-ins for comparisons, e.g. https://www.w3.org/TR/odrl-vocab/#term-isNoneOf and
http://www.w3.org/ns/odrl/2/andSequence have not a "direct" match in SWRL.
3. ODRL constraints are not exclusively for use with ODRL actions, they can also be used to constrain Asset and Party Collections (https://www.w3.org/TR/odrl-vocab/#term-refinement).


**Solution 3**

A third solution (which is also the most voted by the members of the sub-group) consists in using SHACL instead of SWRL for describing the class of actions regulated by one rule. 

References: https://www.w3.org/TR/shacl; https://www.w3.org/TR/shacl-af/#rules

By using SHACL it is possible to specify which **node** into a **data graph** must conform to a **shape**. 

The **data graph** contains one ODRL policy, for example:

     {
      "@context": "http://www.w3.org/ns/odrl.jsonld",
      "@type": "Set",
      "uid": "http://example.com/policy:1010",
      "permission": [{
 	      "target": "http://example.com/asset:9898.movie",
	      "action": "display"
       }]
    }
    
   
The **shape** written using SHACL has to match all the Diplay actions on the target "http://example.com/asset:9898.movie" performed in Germany. It is not actually a constraint because for the policy it is a permitted action.

_Insert here the SHACL expression._

The corresponding SPARQL query is:

```
SELECT ?a
WHERE {
?a rdf:type odrl:Display.
?a odrl:spatial "germany"ˆˆxsd:string.
?a odrl:target  http://example.com/asset:9898.movie.
}
```

PROBLEM: connecting the policy with the SHACL constraint or SPARQL query

-------------------------------------------------------

**References on policies monitoring and compliance checking**

N. Fornara and M. Colombetti. Using Semantic Web Technologies and Production Rules for Reasoning on Obligations, Permissions, and Prohibitions. AI Communications, vol. 32, no. 4, pp. 319-334, 2019. https://people.lu.usi.ch/fornaran/AIComm2019/AIComm32(2019)_Fornara.pdf

M. Sensoy, T. J. Norman, W. W. Vasconcelos, K. P. Sycara, OWL-POLAR: A framework for semantic policy representation and reasoning, J. Web Sem. 12 (2012) 148–160. URL:
https://doi.org/10.1016/j.websem.2011.11.005

N. Fornara, S. Roshankish, and M. Colombetti (2021) A Framework for Automatic Monitoring of Norms that regulate Time Constrained Actions. International Workshop on Coordination, Organizations, Institutions, Norms and Ethics for Governance of Multi-Agent Systems (COINE), co-located with AAMAS 2021, London, UK, 3rd May, 2021. https://arxiv.org/pdf/2105.00200.pdf

De Vos M., Kirrane S., Padget J., Satoh K. (2019) ODRL Policy Modelling and Compliance Checking. In: Fodor P., Montali M., Calvanese D., Roman D. (eds) Rules and Reasoning. RuleML+RR 2019. Lecture Notes in Computer Science, vol 11784. Springer, Cham. https://doi.org/10.1007/978-3-030-31095-0_3

ODRL Regulatory Compliance Profile Unofficial Draft 10 August 2020 https://ai.wu.ac.at/policies/orcp/regulatory-model.html

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
  7. (Staring from September 2021) Harshvardhan J. Pandit (me@harshp.com) postoc at Trinity College Dublin.
  8. (Starting from January 2022) Simon Steyskal (simon.steyskal@siemens.com) Siemens AG Austria Vienna.

 We can also send a message in the ODRL mailing list community group.
 
