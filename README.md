# CHEME7770-PS-2

DataDictionary contains four functions that are used to calculate the metabolic flux distributions for the four cases

1.	Aerobic conditions with regulatory constraints (function maximize_cellmass_aerobic_regulated_data_dictionary)

2.	Aerobic conditions without regulatory constraints (function maximize_cellmass_aerobic_unregulated_data_dictionary)

3.	Anaerobic conditions with regulatory constraint (function maximize_cellmass_anaerobic_regulated_data_dictionary)

4.	Anaerobic conditions without regulatory constraints (function maximize_cellmass_anaerobic_unregulated_data_dictionary)

Each of these functions can be called separately in Solve.jl
The resulting arrays of the LP problem have been stored in the four folders in src labeled Aerobic regulated results, Anaerobic regulated results, Aerobic unregulated results, Anaerobic unregulated results.

Changes were made to the exchange_array for all four fluxes based on the information in Palsson et al., 2009, Reconstruction and Use of Microbial Metabolic Networks: the Core Escherichia coli Metabolic Model as an Educational Guide .
Glucose uptake rate = 10 mmol/gDW/h (so lower bound of M_glc_D_b was set to 
-10)
Rxns in involving pyruvate kinase and the production of glutamate are activated.

Without regulatory constraints:
For the unregulated results, changes were made in the exchange_array.
Phosphate was seen to have a large effect on flux and so its lower bound was set to an optimal value of -2.

For the anaerobic case, flux is sensitive to the EtOH produced by E. coli, so its upper bound was set to the low value of 0.15 (also E.coli is a poor producer of EtOH).


With regulatory constraints:
The Boolean rules given by Tables 16 and 17 in  Palsson et al. were used. The changes made in the unregulated case exchange_array also carry over here.

Aerobic conditions:

The following assumptions were made:
There is o2[e], nh4[e] , phosphate pi[e] and glucose glc-D[e] present in the cell. So these compounds are in the ‘on’ state i.e. have the value 1 in the Boolean code.
Since the cell is growing, Biomass_Ecoli_core was set to 1.
Based on these, the Boolean values for table 17 were calculated and these were then used to calculate which of the reactions on table 16 are ‘on’ or ‘off’. The remaining reactions in the code were set to be ‘on’.

Anaerobic conditions:
Other than o2[e], nh4[e] , pi[e] and glc-D[e], lactate lac-D, acetate ac and formate (for) and etoh are secreted by the cell in order to balance the reactions (so that the NADPH produced has a way to be used to form the above mentioned byproducts).  
(ref. Palsson et al. pg 35)
Their value in the Boolean is set to 1.

Also their upper bounds in the exchange_array were set to a positive value. (also done for the unregulated case)



Discussion of results:

The flux values obtained as the objective_value match those in Palsson et al. pg 35

0.81 h-1  for aerobic conditions both with and without regulatory constraints and
0.21 h-1 for anaerobic conditions both with and without regulatory constraints.

The same growth rates were obtained for both with and without regulatory constraints since the reactions that are inactivated by including the regulatory constraints are not involved in the optimal flux distribution for growth on glucose. Thus the growth rate is not affected. (ref. Palsson et al. pg 35)

The growth rate is lesser in the absence of oxygen which is expected since many metabolic pathways are switched off.



