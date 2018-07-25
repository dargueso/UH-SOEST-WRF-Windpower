# UH-SOEST-WRF-Windpower
Modified version of WRF to write out wind energy variables at specific above-the-ground levels and its statistics


---------------------------------------------
WRFV3.8 Modified for wind energy applications
8/09/2016 Daniel Argüeso @ University of Hawaii
email: dab8@hawaii.edu


Weather Research and Forecasting Model v3.8 was developed by National Center for
Atmospheric Research (NCAR) which is operated by the University Corporation for
Atmospheric Research (UCAR). Please read their instructions for general
information about the model.

This is a personal project and therefore it is provided AS IS and any warranties are disclaimed.


---------------------------------------------

This modified version of WRFV3.8 is available at:

https://github.com/dargueso/UH-SOEST-WRF-Windpower


---------------------------------------------
---------------------------------------------

The purpose of this modifications is to provide variables that are relevant for wind
power resources studies. These variables are provided at specific levels above
the ground indicated by the user (z-levels).

In addition to instantaneous values of the variables at the time of the output,
a set of statistics calculated at time-step frequency are also provided, such as
maximum, standard deviation and mean since the last output.

Variables have ZL appended to their name indicated that they refer to
levels above the ground (this is a feature in the original WRFV3.8). Using the sample namelist, they are written to an auxliary
wrf output file called wrfzl_d0?_[DATE].

Available variables are:   
  
|Variable           |  description                                                                        |  Units |
|-------------------|-------------------------------------------------------------------------------------|--------|
|U_ZLMAX:           |  Height level data, U COMPONENT OF MAXIMUM WIND SPEED IN DIAGNOSTIC OUTPUT INTERVAL |  m s-1|
|V_ZLMAX:           |  Height level data, V COMPONENT OF MAXIMUM WIND SPEED IN DIAGNOSTIC OUTPUT INTERVAL |  m s-1|
|SPDUV_ZLMAX        |  Height level data, MAXIMUM WIND SPEED IN DIAGNOSTIC OUTPUT INTERVAL                |  m s-1|
|TSPDUV_ZLMAX       |  Height level data, TIME OF MAXIMUM WIND SPEED IN DIAGNOSTIC OUTPUT INTERVAL        |  minute|
|WPD_ZLMAX          |  Height level data, MAXIMUM WIND POWER DENSITY IN DIAGNOSTIC OUTPUT INTERVAL        |  W m-2|
|TWPD_ZLMAX         |  Height level data, TIME OF MAXIMUM WIND POWER DENSITY IN DIAGNOSTIC OUTPUT INTERVAL|  minute|
|U_ZLSTD            |  Height level data, STANDARD DEV. U IN DIAGNOSTIC OUTPUT INTERVAL                   |  m s-1|
|V_ZLSTD            |  Height level data, STANDARD DEV. U IN DIAGNOSTIC OUTPUT INTERVAL                   |  m s-1|
|SPDUV_ZLSTD        |  Height level data, STANDARD DEV. WIND SPEED IN DIAGNOSTIC OUTPUT INTERVAL          |  m s-1|
|WPD_ZLSTD          |  Height level data, STANDARD DEV. WIND POWER DENSITY IN DIAGNOSTIC OUTPUT INTERVAL  |  W m-2|
|U_ZLMEAN           |  Height level data, MEAN U IN DIAGNOSTIC OUTPUT INTERVAL                            |  m s-1|
|V_ZLMEAN           |  Height level data, MEAN U IN DIAGNOSTIC OUTPUT INTERVAL                            |  m s-1|
|SPDUV_ZLMEAN       |  Height level data, MEAN WIND SPEED IN DIAGNOSTIC OUTPUT INTERVAL                   |  m s-1|
|WPD_ZLMEAN         |  Height level data, MEAN WIND POWER DENSITY IN DIAGNOSTIC OUTPUT INTERVAL           |  W m-2|


A few variables were removed from the output at z-levels that were in the original WRFV3.8 (RH_ZL, GHT_ZL, S_ZL, Q_ZL)

Computation of wind power density (WPD) was added to the code and is defined as:

WPD = 0.5 * rho * ((U\**2+V\**2)**(0.5))**3

Output levels are selected in the &diags section of the namelist.input. For example:

&diags  
z_lev_diags                         = 1,  
num_z_levels                        = 4,  
z_levels                            = -80,-100,-120,-150,  
/

See WRF official documentation for further details.

A sample namelist.input is provided in WRFV3.8/run/namelist.input_sample_windenergyvars
