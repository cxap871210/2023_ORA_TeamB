# Multi-Commodity Distribution Under Uncertainty in Disaster Response Phase

## ORA Term Project (2023 Fall)
Team B (Supply Chain Resilience)</br></br>
T12303106 David Benedi </br>
R11725028 陳柄瑞  </br>
R12725060 Welbey Prasadirta 陳祖譽  </br>

## Table of Contents
1. [Background and Motivation](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#table-of-contents) </br>
  1.1. [Motivation](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#motivation) </br> 
  1.2. [Background](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#background) </br>
  1.3. [Problem Definition](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#problem-definition) </br>
2. [Methodology](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#methodology)  
3. [Data Collection and Analysis Result](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#data-collection-and-analysis-result) </br>
  3.1. [Data Collection](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#data-collection) </br>
  3.2. [Analysis](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#analysis)  </br>
  3.3. [Results and Managerial Implications](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#results-and-managerial-implications) </br>
4. [Conclusion](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#conclusion) 
5. [Reference](https://github.com/cxap871210/2023_ORA_TeamB?tab=readme-ov-file#reference)  

## Background and Motivation
### Motivation
### Background
### Problem Definition

## Methodology
### Inventory Routing Problem (Gurobi Optimizer)

### Model Objective 
<p align="justify">to identify the most effective vehicle routes for distributing vital commodities from a Distribution Center (DC) to various Local Relief Centers (RCs) and between these RCs. The goal is to actively meet each Relief Center (RC) demand while minimizing the completion time (longest) of vehicle assignments, all within the context of stochastic traffic conditions caused by earthquake impacts. The model will account for each RC's pre-existing inventory sourced from local donations.</p>

### Model Assumptions
-	Multiple vehicles can fulfill RC demand level (Split Delivery).
-	We can divide RC demand into multiple deliveries instead of being shipped as one complete package. 
-	Vehicles have the permission to make multiple visits to various facilities to perform loading and unloading activities (Multiple Destination).
-	Loading and unloading times are assumed to be negligible.
-	The locations of all facilities, including a DC and five RCs, are known.
-	DC maintains an unlimited supply of commodities and has no demand for them.
-	Each RC has a known initial inventory level and demand for each commodity.
-	DC and RCs operate without a maximum limit on their inventory capacity.
-	The number of vehicles in the network is known, and each vehicle has the same capacity and can carry any commodity.
-	Vehicles heading to a DC do not need to carry commodities.

### Notation and Definitions 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Sets** 
 - _H_: set of vehicles, indexed by _h_.
 - _PI_: set of journey number, indexed by π ∈ {1,2,…,θ}.
 - _N_: set of nodes, indexed by _a, b, c_.
 - _G_: set of types of commodities, indexed by _g_.
 - _I<sub>gb</sub>_: initial inventory level of commodity _g_ at RC _b_.
 - _Q<sub>gb</sub>_: demand of commodity _g_ at RC _b_.
 - _volume<sub>g_</sub>: volume of one unit of commodity _g_.
 - _carryingvolume_: total carrying volume of each vehicle.
 -	_t<sub>ab<sub>_: the travel time required from node _a_ to node _b_. </br></br>
**Decision Variables** </br>
 + _X<sup>hπ</sup><sub>ab</sub>_: if it is 1, it means that vehicle _h_ travels from node _a_ to node _b_ during its πth journey; otherwise, it is 0.
 + _Y<sup>hπ</sup><sub>gab</sub>_: the quantity of commodity _g_ transported by vehicle _h_ traveling from node _a_ to node _b_ during its πth journey.

### Model Formulation
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Objective Function** 
 - minimize _T_ </br></br>
**Constraints** </br></br>
 - Constraint 1: a given vehicle will only use one link to move in each journey. </br>
∑<sub>a∈N</sub> ∑<sub>b∈N</sub> _X<sup>hπ</sup><sub>ab</sub>_ ≤ 1 ∀h ∈ H, π ∈ PI. </br></br>
 - Constraint 2: allowing vehicle journeys to be connected, i.e., the end of the previous journey is the starting point of the next. </br>
∑<sub>a∈N</sub> _X<sup>h(π-1)</sup><sub>ab</sub>_ ≤ ∑<sub>c∈N</sub> _X<sup>hπ</sup><sub>bc</sub>_ ∀b ∈ N, h ∈ H, π ∈ {2,3,…,θ}. </br></br>
 - Constraint 3: guaranteeing that the commodities shipped to the DC are zero. </br>
_Y<sup>hπ</sup><sub>ga1</sub>_ = 0 ∀h ϵ H, π ϵ PI, g ϵ G, a ϵ N. </br></br>
 - Constraint 4: ensuring that the final inventory level of all nodes must be greater than or equal to their demand. </br>
_I<sub>gb</sub>_ + ∑<sub>h∈H</sub> ∑<sub>π∈PI</sub> ∑<sub>a∈N</sub> _Y<sup>hπ</sup><sub>gab</sub>_ - ∑<sub>h∈H</sub> ∑<sub>π∈PI</sub> ∑<sub>c∈N</sub> _Y<sup>hπ</sup><sub>gbc</sub>_ ≥ _Q<sub>gb</sub>_ ∀g ϵ G, b ϵ N. </br></br>
 - Constraint 5: vehicle capacity. </br>
∑<sub>g∈G</sub> _Y<sup>hπ</sup><sub>gab</sub>_ ≤ _carryingvolume_ x _X<sup>hπ</sup><sub>ab</sub>_ ∀h ∈ H, π ∈ PI, a ∈ N, b ∈ N. </br></br>
 - Constraint 6: maximizing total times in each journey. </br>
_T_ ≥  ∑<sub>π∈PI</sub> ∑<sub>a∈N</sub> ∑<sub>b∈N</sub> _X<sup>hπ</sup><sub>ab</sub>_ × _t<sub>ab<sub>_ ∀h ϵ H. </br></br>
 - Constraint 7: decision variable constraints. </br>
_X<sup>hπ</sup><sub>ab</sub>_ ϵ {0,1} ∀a ϵ N, b ϵ N, h ϵ H, π ϵ PI. </br> 
_Y<sup>hπ</sup><sub>gab</sub>_ ≥ 0 ∀g ϵ G, a ϵ N, b ϵ N, h ϵ H, π ϵ PI. </br> 
_t<sub>ab<sub>_ ≥ 0 ∀a ϵ N, b ϵ N. </br>


## Data Collection and Analysis Result
### Data Collection
### Analysis
### Results and Managerial Implications

## Conclusion
## Reference
