<H3>Enter Name RAKESH K S</H3>
<H3>Enter Register No. 212224040264</H3>
<H3>Experiment 2</H3>
<H3>Date 25/07/2026</H3>
<h1 align =center>Implementation of Exact Inference Method of Bayesian Network</h1>

## Aim:
To implement the inference Burglary P(B| j,⥗m) in alarm problem by using Variable Elimination method in Python.

## Algorithm:

Step 1: Define the Bayesian Network structure for alarm problem with 5 random variables, Burglary,Earthquake,John Call,Mary Call and Alarm.<br>
Step 2: Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class from the pgmpy library.<br>
Step 3: Add the CPDs to the network.<br>
Step 4: Initialize the inference engine using the VariableElimination class from the pgmpy library.<br>
Step 5: Define the evidence (observed variables) and query variables.<br>
Step 6: Perform exact inference using the defined evidence and query variables.<br>
Step 7: Print the results.<br>

## Program :
```py
# Defining network structure

alarm_model = DiscreteBayesianNetwork(
    [
        ("Burglary", "Alarm"),
        ("Earthquake", "Alarm"),
        ("Alarm", "JohnCalls"),
        ("Alarm", "MaryCalls"),
    ]
)

# Defining the parameters using CPT
from pgmpy.factors.discrete import TabularCPD

cpd_burglary = TabularCPD(
    variable="Burglary", variable_card=2, values=[[0.999], [0.001]]
)
cpd_earthquake = TabularCPD(
    variable="Earthquake", variable_card=2, values=[[0.998], [0.002]]
)
cpd_alarm = TabularCPD(
    variable="Alarm",
    variable_card=2,
    values=[[0.999, 0.71, 0.06, 0.05], [0.001, 0.29, 0.94, 0.95]],
    evidence=["Burglary", "Earthquake"],
    evidence_card=[2, 2],
)
cpd_johncalls = TabularCPD(
    variable="JohnCalls",
    variable_card=2,
    values=[[0.95, 0.1], [0.05, 0.9]],
    evidence=["Alarm"],
    evidence_card=[2],
)
cpd_marycalls = TabularCPD(
    variable="MaryCalls",
    variable_card=2,
    values=[[0.99, 0.3], [0.01, 0.7]],
    evidence=["Alarm"],
    evidence_card=[2],
)

# Associating the parameters with the model structure
alarm_model.add_cpds(
    cpd_burglary, cpd_earthquake, cpd_alarm, cpd_johncalls, cpd_marycalls
)
```
```py
alarm_model.check_model()
```
```py
inference=VariableElimination(alarm_model)
```
```py
evidence={"JohnCalls":1,"MaryCalls":0}
```
```py
query='Burglary'
```
```py
res=inference.query(variables=[query],evidence=evidence)
```
```py
print(res)
```
```py
evidence2={"JohnCalls":1,"MaryCalls":1}
```
```py
res2=inference.query(variables=[query],evidence=evidence2)
```
```py
print(res2)
```


## Output :
<img width="347" height="167" alt="image" src="https://github.com/user-attachments/assets/eba463eb-38db-4c13-8802-25f6b7911ede" />
<img width="351" height="170" alt="image" src="https://github.com/user-attachments/assets/ab9efc76-3301-40bc-9984-6e5b8f0f497e" />




## Result :
Thus, Bayesian Inference was successfully determined using Variable Elimination Method

