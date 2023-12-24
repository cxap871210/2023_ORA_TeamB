# Multi-Commodity Distribution Under Uncertainty in Disaster Response Phase

## ORA Term Project (2023 Fall)
Team B (Supply Chain Resilience)</br></br>
T12303106 David Benedi </br>
R11725028 陳柄瑞  </br>
R12725060 陳祖譽 Welbey Prasadirta  </br>

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

- **Humanitarian Impact**: In the aftermath of earthquakes, there is a surge in demand for life-supporting commodities like food, water, medical supplies, and survival equipment. The efficient distribution of these supplies is crucial to mitigate the suffering of affected populations and potentially save lives​.
- **Prevention of Social Upset and Mistrust**: Ineffective and slow delivery of essential commodities can lead to high anxiety levels among the population, mistrust in government authorities, and even social conflict. These can exacerbate the already dire situation in disaster-stricken areas, making commodity distribution optimization even more crucial​.
- **Addressing the Challenge of Uncertainty**: Post-disaster environments are highly uncertain, and characterized by disrupted transportation networks. The decision-making process in these scenarios is complex and challenging, necessitating systematic and coordinated planning and response strategies​.
- **Historical Precedence and Ongoing Risk**: over the years, the world has witnessed numerous large-scale natural disasters resulting in significant loss of life, displacement of populations, and extensive damage to infrastructure and economies. Regions like Taiwan, which are geographically prone to typhoons, floods, earthquakes, and tsunamis, face a continuous threat. Efficient disaster response strategies are vital for these areas to minimize the impact of such catastrophic events​.
- **Global Significance**: Earthquakes and other natural disasters are world phenomena and are not limited to any specific region. The model and methodologies developed in this research have international applicability and can provide valuable insights and frameworks for disaster response globally.
  
### Background

<p align="justify">The background of the problem involves understanding the complexities of disaster response, particularly in distributing various commodities to affected areas. Challenges include dealing with damaged infrastructure and logistical constraints. The importance of material requirement planning and capacity planning in this context lies in their ability to streamline the distribution process, ensuring timely and adequate supply of necessary goods to disaster-stricken areas. </p>

### Problem Definition

<p align="justify">The problem is defined as the need for a robust model to optimize the distribution of multiple commodities in the disaster response phase. The study proposes a solution that takes into account the uncertainties and constraints typical of post-disaster scenarios. This involves developing a stochastic programming model that aims to minimize the total time associated with the allocation of resources and capacities for fulfilling the demand in a disrupted supply chain network. </p>

## Methodology
### Inventory Routing Problem (Gurobi Optimizer)

### Model Objective 
<p align="justify">To identify the most effective vehicle routes for distributing vital commodities from a Distribution Center (DC) to various Local Relief Centers (RCs) and between these RCs. The goal is to actively meet each Relief Center (RC) demand while minimizing the completion time (longest) of vehicle assignments, all within the context of stochastic traffic conditions caused by earthquake impacts. The model will account for each RC's pre-existing inventory sourced from local donations.</p>

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

| Nodes                    | Initial Inventory of Blood Packages | Initial Inventory of Medication | Demand of  Blood Packages | Demand of Medication |
|--------------------------|--------------------------------------|--------------------------------|---------------------------|----------------------|
| DC                       | Unlimited Supplies                   | Unlimited Supplies             | No Demand                 | No Demand            |
| 1<sup>st</sup> RC        | 30                                   | 20                             | 60                        | 40                   |
| 2<sup>nd</sup> RC        | 20                                   | 30                             | 50                        | 50                   |
| 3<sup>rd</sup> RC        | 50                                   | 20                             | 90                        | 30                   |
| 4<sup>th</sup> RC        | 30                                   | 30                             | 50                        | 40                   |
| 5<sup>th</sup> RC        | 40                                   | 20                             | 70                        | 40                   |
</br>

-  Three trucks, each with a maximum of 20 journey numbers, each with a maximum of 250 carrying volumes. </br>
-  Blood Package, each blood package will fill 5 trucks carrying volume.</br>
-  Medication go bag, each medication go bag will fill 10 trucks carrying volume. </br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Decision Variables** 
 + $X^{hπ}_{ab}$: if it is 1, it means that vehicle _h_ travels from node _a_ to node _b_ during its πth journey; otherwise, it is 0.
 + $Y^{hπ}_{gab}$: the quantity of commodity _g_ transported by vehicle _h_ traveling from node _a_ to node _b_ during its πth journey.

### Model Formulation
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Objective Function** 
 - minimize _T_ </br></br>
**Constraints** </br></br>
 - Constraint 1: a given vehicle will only use one link to move in each journey. </br>
∑<sub>a∈N</sub> ∑<sub>b∈N</sub> $X^{hπ}_{ab}$ ≤ 1 ∀h ∈ H, π ∈ PI. </br>
<p align="justify"> The mathematical model ensures that each vehicle in the fleet uses exactly one link to move from one node to another in each journey.
This implies that in each journey π, vehicle h will travel from node a to node b using one designated path, ensuring that the routing of vehicles
is properly defined and does not allow for any vehicle to travel on multiple paths simultaneously. </p>

 - Constraint 2: allowing vehicle journeys to be connected, i.e., the end of the previous journey is the starting point of the next. \\
   $\sum_{a \in N} X^{h \pi}_{ab} \leq \sum_{c \in N} X^{h \pi}_{bc} \forall$
<p align="justify"> The mathematical model refers to the sequential connection of vehicle journeys. It ensures that the end of one journey must be the starting point for the subsequent journey. This is modeled by stating that for any node 
b, the amount of commodity g picked up by vehicle h in the previous journey (π−1) should be smaller and equal to the amount of commodity g delivered to the same node b by the same vehicle h in the next journey π.
This constraint ensures the continuity of vehicle routing and that the flow of commodities is accounted for accurately in the mathematical optimization problem.</p>

 - Constraint 3: guaranteeing that the commodities shipped to the DC are zero. </br>
$Y^{hπ}_{ga1}$ = 0 ∀h ϵ H, π ϵ PI, g ϵ G, a ϵ N. </br>
<p align="justify"> The mathematical model ensures that the amount of commodities shipped to the DC is zero. This is a critical aspect of the model because it implies that vehicles are not allowed to transport commodities back to the DC. This constraint effectively maintains the flow of commodities in one direction - from the distribution centers to the points of need, rather than allowing for backflow to the centers or non-operational points, thereby ensuring that relief efforts are directed outward from supply points to where they are needed.</p>

 - Constraint 4: ensuring that the final inventory level of all nodes must be greater than or equal to their demand. </br>
_I<sub>gb</sub>_ + ∑<sub>h∈H</sub> ∑<sub>π∈PI</sub> ∑<sub>a∈N</sub> $Y^{hπ}_{gab}$ - ∑<sub>h∈H</sub> ∑<sub>π∈PI</sub> ∑<sub>c∈N</sub> $Y^{hπ}_{gab}$ ≥ _Q<sub>gb</sub>_ ∀g ϵ G, b ϵ N. </br>
<p align="justify"> The mathematical model ensures that the final inventory level of all nodes must be greater than or equal to their demand. Sometimes it is more optimal to pick up commodities from RC rather than go back and pick them up from DC.
This constraint wants to ensure that at the end of the model, all the RC's demands are fulfilled. All the RC demands are guaranteed fulfilled because the DC supply is unlimited.</p>

 - Constraint 5: vehicle capacity. </br>
∑<sub>g∈G</sub> $Y^{hπ}_{gab}$ ≤ _carryingvolume_ x  $X^{hπ}_{ab}$ ∀h ∈ H, π ∈ PI, a ∈ N, b ∈ N. </br>
<p align="justify"> The mathematical model sets a limit on the amount of commodity g that can be picked up from node a and delivered to node b by vehicle h in journey π. 
This constraint ensures that the vehicle capacities are not exceeded and that the flow of commodities is by the planned routing and vehicle assignments. </p>

 - Constraint 6: maximizing total times in each journey. </br>
_T_ ≥  ∑<sub>π∈PI</sub> ∑<sub>a∈N</sub> ∑<sub>b∈N</sub>  $X^{hπ}_{ab}$ × _t<sub>ab<sub>_ ∀h ϵ H. </br>
<p align="justify">Every vehicle in each journey has its different traveling time according to the path they are taking. The constraint will help the model to choose the maximum travelling times in each journey to be totaled at the end of the model.</p>

 - Constraint 7: decision variable constraints. </br>
$X^{hπ}_{ab}$ ϵ {0,1} ∀a ϵ N, b ϵ N, h ϵ H, π ϵ PI. </br> 
$Y^{hπ}_{gab}$ ≥ 0 ∀g ϵ G, a ϵ N, b ϵ N, h ϵ H, π ϵ PI. </br> 
_t<sub>ab<sub>_ ≥ 0 ∀a ϵ N, b ϵ N. </br>


## Data Collection and Analysis Result
### Data Collection
### Analysis
We apply the Sample Average Approximation method to analyze this problem. The SAA method for solving stochastic optimization problems involves generating a set of samples from the probability distribution representing uncertainties, such as the impact of earthquakes on road travel times. In our analysis, we generate 30 samples from a road damage probability density function proposed in the reference paper. The road damage probability density function is as follows:  
$$p_i(x) = \frac{1}{\sqrt{2 \pi} \beta x}e^{\left[ -\frac{1}{2}(\frac{\ln x - \ln m}{\beta})^2 \right]}  ,0 \leq x \leq \infty.$$
$p_i$ represents the probability of road $i$ being damaged after an earthquake with PGD value $x$. Knowing $p_i$, we can compute the traveling time of road $i$ after being damaged by a sample draw of $\beta_i \thicksim (10-10p_i, \ 10p)$. We define that
$$t^{damaged}_i(x) = t^{original}_i \times[1+\beta_i(p_i)]$$ 
where $t^{original}_i$ is the original traveling time of road $i$ and $t^{damaged}_i$ is the traveling time of road $i$ after being damaged. For each sample, a random model is constructed by calculating the traveling time of each road according to the above definition to describe the optimization problem under that specific scenario. The optimization problem is then solved for each sample, yielding corresponding optimal solutions. The average of these optimal solutions across all samples is computed to approximate the final solution. The performance of this solution, considering uncertainties, is evaluated. If a more precise result is desired, the process is iterated by increasing the number of samples. Overall, the SAA method provides a way to approximate solutions for optimization problems in the presence of uncertainty by simulating multiple scenarios and averaging the results.

### Results and Managerial Implications
<p align="justify"> The average completion time (longest) of vehicle assignment is 19.934, and the standard deviation is 0.217. Then the 95% confidence interval of the objective value is $[19.859, 20.009]$. The confidence interval signifies the uncertainty surrounding the estimated average for the completion time (longest) of vehicle assignment. The calculated average from the Sample Average Approximation (SAA) method, based on 30 computations, is 19.934. This average is viewed as an expectation of the vehicle travel metrics. The width of the confidence interval, established at a 95% confidence level, reflects the statistical uncertainty associated with this estimation. In practical terms, there is a 95% probability that the true average lies within this interval if similar experiments were conducted. This statistical range aids in comprehending the reliability of the average estimation, especially in the context of road damage caused by earthquakes and the resulting variability in travel times. </p>

## Conclusion
<p align="justify">In conclusion, the application of the Sample Average Approximation (SAA) method to address the impact of earthquake-induced road damage on the shortest distance and travel time estimation proved insightful. Through 30 iterations, the method produced a set of optimal solutions, yielding an average estimate of 19.934 for the vehicle travel metrics. The calculated confidence interval [19.859, 20.009] at a 95% confidence level encapsulates the statistical uncertainty associated with this average. This interval provides a valuable range, indicating that there is a 95% probability that the true average falls within it. Consequently, in the face of uncertain conditions introduced by the seismic event, this statistical approach offers a robust understanding of the reliability of the estimated shortest distance and travel time metrics. </p>

<p align="justify">The study still has a few potential limitations and areas for improvement. Firstly, the sample size of 30 computations might be considered relatively small. Increasing the sample size could enhance the accuracy of the average estimation and reduce the width of the confidence interval. Secondly, there is only 1 DC and 5 RC in our problem, which is also relatively small. However, considering that the problem has to be solved multiple times to complete the SAA process, we are not able to increase the DC and RC numbers due to time limitations. We attempted to increase the numbers, but it took too long to obtain the optimal solution with the restriction of computing power. Additionally, the model's simplicity in addressing the impact of earthquake-induced road damage may oversimplify the varying degrees of damage. Further research could explore more complex seismic impact models to better reflect diverse road damage scenarios. In summary, addressing these aspects could further enhance the reliability and practical utility of the study, allowing it to more effectively address the impact of earthquake-induced road damage on traffic flow. </p>

## Reference
Chang, K.-H., T.-Y. Hsiung, T.-Y. Chang. 2022. Multi-commodity distribution under uncertainty in disaster response phase: Model, solution method, and an empirical study. *European Journal of Operational Research* 303(2) 857–876.
