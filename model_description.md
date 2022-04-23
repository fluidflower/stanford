_Please stick to the headings and their order. Don't modify the words in bold. Your input is required at each occurrence of "e.g." and "..."._<br>
_You may use https://tex-image-link-generator.herokuapp.com/ to render math formulas in Markdown, see the examples below._

## Physics

### PDEs

[//]: <> (_E.g._ One mass balance per component water and CO2.)
We use black oil formulation to simulate CO2 injection, where oil phase represent brine phase, gas phase represent CO2 phase. Gas component represents CO2 components

![\frac{\partial }{\partial t}(\phi b_o S_o) + \nabla \cdot \left(b_o \boldsymbol{u}_o \right) = q_o,
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%0A++++%5Cfrac%7B%5Cpartial+%7D%7B%5Cpartial+t%7D%28%5Cphi+b_o+S_o%29+%2B+%5Cnabla+%5Ccdot+%5Cleft%28b_o+%5Cboldsymbol%7Bu%7D_o+%5Cright%29+%3D+q_o%2C%0A)

![\frac{\partial }{\partial t}(\phi b_w S_w) + \nabla \cdot \left(b_w \boldsymbol{u}_w \right) = q_w,](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cfrac%7B%5Cpartial+%7D%7B%5Cpartial+t%7D%28%5Cphi+b_w+S_w%29+%2B+%5Cnabla+%5Ccdot+%5Cleft%28b_w+%5Cboldsymbol%7Bu%7D_w+%5Cright%29+%3D+q_w%2C)

![    \frac{\partial }{\partial t}\left(\phi (b_g S_g + R_s b_o S_o)\right) + \nabla \cdot \left(b_g \boldsymbol{u}_g + R_s b_o\boldsymbol{u}_o\right) = q_g + R_s q_o.](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+++++%5Cfrac%7B%5Cpartial+%7D%7B%5Cpartial+t%7D%5Cleft%28%5Cphi+%28b_g+S_g+%2B+R_s+b_o+S_o%29%5Cright%29+%2B+%5Cnabla+%5Ccdot+%5Cleft%28b_g+%5Cboldsymbol%7Bu%7D_g+%2B+R_s+b_o%5Cboldsymbol%7Bu%7D_o%5Cright%29+%3D+q_g+%2B+R_s+q_o.)

### Constitutive relations

#### Fluid-matrix interaction

* **Capillary pressure:** _E.g._ Brooks-Corey
  ![p_c(S_{l}) = p_\text{entry}S_{le}^{-1/\lambda}](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+p_c%28S_%7Bl%7D%29+%3D+p_%5Ctext%7Bentry%7DS_%7Ble%7D%5E%7B-1%2F%5Clambda%7D%0A)

* **Relative permeability:** 
We have tried on
  - Quadratic relative permeability

#### Phase composition: Applied equations of state

* **CO2 in liquid phase:** 
  * Our method to calculate the gas solubility 
    - Estimate c_max factor at 20 degree C and 1 atm [R.F Weiss, Marine Chemestry, 1974]
    - Formula to calculate Rs_max [T.H Sandve et al., Trindheim CCS Conf., 2021] 

* **Water in gas phase:** ...

#### Density

* **Liquid phase:** 
mu_w=0.8e-3 Pa s
mu_c=15.0e-6 Pa s

* **Gas phase:** 

rho_c0=1.7 kg/m^3 c_c=1e-5 Pa^-1

#### Solubility limit

We assumed a solubulity of 1.5 kg/m<sup>3</sup>, though we varied this parameters._

### Temperature

We assumed a 20 °C temperature._

### Domain volume

We assumed 0.084 m<sup>3</sup>._

### Spatial parameters

_Please provide the relevant facies parameters as a csv file._<br>
_E.g._ The parameters ![p_\text{entry}, \lambda, S_{lr}, S_{gr}](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+p_%5Ctext%7Bentry%7D%2C+%5Clambda%2C+S_%7Blr%7D%2C+S_%7Bgr%7D%0A) for the different facies are given in [spatial_parameters.csv](spatial_parameters.csv).<br>
_Obviously, the number and type of parameters for your model might differ from the ones in the provided template._

## Numerics

### Coupling of flow and transport, temporal and spatial discretization

[//]: <> (_E.g._ Fully coupled, fully implicit, cell-centered FV with TPFA.)

Fully Implicit Schemes incorporating, flow and transport problem and the well problems.
The scheme use is TPFA with a PPU upwinding.
We have generated both Prism Grid (Extruded Triangulation) and Pepi Grid but are currently presenting results from the Prism Grid.
 
### Linearization and Solvers

[//]: <>  (_E.g._ Newton with line search, AMG-preconditioned BiCGSTAB for the linear systems.)
Direct linear solver. Specially we are using SUPERLU right now



### Primary Variables

[//]: <> (_E.g._ Dependent on local phase composition:)

We are using pseudo black oil formulation to simulate the CO2-Water-Brine system, where *p* represents fluid pressure, *Sw* represents water saturation, *Sg* represents CO2 gas saturation
* Free CO2 gas exists:
  [p, Sw, Sg]
* No Free CO2 gas:
  [p, Sw, Rs]: where Rs represents the dissolved gas/brine ratio


### Computational Grid

Both computational grid with 6094 prism cells and 21392 prism cells are used

### Performance

| Indicator                            |  Average |      Min |      Max |
|:-------------------------------------|---------:|---------:|---------:|
| time step size [s]                   |     2.28 |          |     4.32 | 
| # nonlinear iterations per time step |    1.074 |        2 |       25 |
| # linear iterations per solve        |        1 |        1 |        1 |
