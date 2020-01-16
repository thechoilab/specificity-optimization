# RT Protocols to Test

**B)** and **C)** are based on the **TSO Revision 1 Protocol** with the following modifications:

## B) Hot Start (No Ice)

Same as the original protocol, but keep everything at **55°C**. First, anneal primer and keep at **55°C**. Then, make dNTP/enzyme mix, warm at **55°C**, then add to primer tube.

## C) Touchdown RT reaction

Replace **Primer Annealing** with the following:

### **Primer Annealing:**

#### 5X Hyb Buffer Recipe

| Reagent           |
| ----------------- |
| 1.5 M NaCl        |
| 50 mM Tris pH 7.5 |
| 10 mM EDTA        |

1. Make a primer/template mix for each sample as detailed below:

   | Reagent          | Volume (uL)   |
   | ---------------- | ------------- |
   | total RNA        | 10 ug (14 uL) |
   | 5X Hyb buffer    | 3.75 uL       |
   | 1 ug primer pool | 1 uL          |
   | **Total**        | 18.75 uL      |

2. In thermo-cycler, heat to **90°C** then cool to **55°C** over 30 min.
3. Prepare the dNTP Enzyme mix as described, warming to **55°C** before adding to template/primer mix. Proceed with rest of reaction as described.

## D) Rocketscript Protocol

1. Add the following reagents:

| Reagent                | Volume (uL)   |
| ---------------------- | ------------- |
| 5X Rocketscript buffer | 3.75 uL       |
| 1st strand primer pool | 1 uL          |
| total RNA              | 10 ug (14 uL) |
| **Total**              | 18.75 uL      |

2. Place samples in thermo-cycler and run the following cycle: **70°C 1 min, 60°C hold**
3. Make the enzyme dNTP mix for each sample as detailed below:
4. 

| Reagent (final concentration per protocol in parentheses)    | Volume (uL) |
| ------------------------------------------------------------ | ----------- |
| 5X Rocketscript buffer                                       | 4           |
| 25 mM dNTP mix (25 mM of each dNTP; final conc = 1 mM mcSCRB-seq protocol, 0.5 mM Dwyer protocol, 1 mM Smart3Seq protocol, 0.5 mM Thermo protocol -> try 1 mM for now) | 1.6         |
| TSO 50 uM stock (2 uM mcSCRB-seq, 1 uM Smart3Seq protocol -> try 1 uM for now) | 1.6         |
| 200 U/uL RocketScript Reverse Transcriptase (2 U/uL mcSCRB-Seq, 10 U/uL Thermo protocol -> try 10 U/uL for now) | 1.5         |
| ddH2O                                                        | 11.3        |
| **Total**                                                    | **20**      |

1. Follow same cycling protocol/conditions for Maxima RT, except allow reaction to proceed at **60°C** for 90 min.

