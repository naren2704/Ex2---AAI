## Name: NARENDRAN B
## Reg No 212222240069
## Experiment 2
## Date: 04/09/2024
## Implementation of Exact Inference Method of Bayesian Network
## Aim:
To implement the inference Burglary P(B| j,⥗m) in alarm problem by using Variable Elimination method in Python.

## Algorithm:

Step 1: Define the Bayesian Network structure for alarm problem with 5 random variables, Burglary,Earthquake,John Call,Mary Call and Alarm.

Step 2: Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class from the pgmpy library.

Step 3: Add the CPDs to the network.

Step 4: Initialize the inference engine using the VariableElimination class from the pgmpy library.

Step 5: Define the evidence (observed variables) and query variables.

Step 6: Perform exact inference using the defined evidence and query variables.

Step 7: Print the results.


## Program :
```
from pgmpy.models import BayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.inference import VariableElimination
network=BayesianNetwork([('Burglary','Alarm'),('Earthquake','Alarm'),
                          ('Alarm','JohnCalls'),
                         ('Alarm','MarryCalls')])
cpd_burglary=TabularCPD(variable='Burglary',variable_card=2,values=[[0.999],[0.001]])
cpd_earthquake=TabularCPD(variable='Earthquake',variable_card=2,values=[[0.998],[0.002]])
cpd_alarm=TabularCPD(variable='Alarm',variable_card=2,values=[[0.999,0.71,0.06,0.05],[0.001,0.29,0.94,0.95]],evidence=['Burglary','Earthquake'],evidence_card=[2,2])
cpd_john_calls=TabularCPD(variable='JohnCalls',variable_card=2,values=[[0.95,0.1],[0.05,0.9]],evidence=['Alarm'],evidence_card=[2])
cpd_marry_calls=TabularCPD(variable='MarryCalls',variable_card=2,values=[[0.99,0.3],[0.01,0.7]],evidence=['Alarm'],evidence_card=[2])
network.add_cpds(cpd_burglary,cpd_earthquake,cpd_alarm,cpd_john_calls,cpd_marry_calls)
inference=VariableElimination(network)
evidence={'JohnCalls':1,'MarryCalls':0}
query_variable='Burglary'
result=inference.query(variables=[query_variable],evidence=evidence)
print(result)
```
## Output :
![image](https://github.com/user-attachments/assets/abeeb423-a89b-427c-9d75-8d9d2fb2bb44)


## Result :
Thus, Bayesian Inference was successfully determined using Variable Elimination Method
