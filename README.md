[![Build Status](https://travis-ci.org/Funz/plugin-moret.png)](https://travis-ci.org/Funz/plugin-moret)

# Funz plugin: moret

This plugin is dedicated to launch MORET calculations from Funz.
It supports the following syntax and features:

  * Input
    * file type supported: '*.m5', any other format for resources
    * parameter syntax: 
      * variable syntax: `$(...)`
      * formula syntax: `@{...}`
      * comment char: `*`
    * example input file:
        ```
        MORET_BEGIN
        
        ...
        GEOM
          MODU 0
          TYPE 1 SPHE $(radius~[1,20])
          VOLU Ext0 0 1 1 0.0 0.0 0.0
          ENDM
        ENDG
        
        MATE
          ...
          COMP UMET
            CONC
            U234     4.91895E-04
            U235     $(u5~4.49988E-02)
            U238     2.49865E-03
          ENDC   
        ENDM
        ...
        ENDD
        MORET_END
        ```
      * will identify input:
        * radius, expected to vary inside [1,20]
        * u5, expected to vary inside [0,1] (by default), with default value 4.49988E-02

  * Output
    * file type supported: '*.listing'
    * read `mean_keff`, `sigma_keff`, `dkeff_pertu`, `sigma_dkeff_pertu`
    * example output file:
        ```
        ...
        ##                                             ESTIMATION FINALE DU KEFF                                              ##
        ##                                                                                                                    ##
        ##                                                          KEFF     ECART TYPE    INTERVALLE A +/- 3 SIGMA           ##
        ##                 ETAPE    417  ESTI. + FAIBLE SIGMA     0.99612 +/-  0.00100  :  0.99314 < KEFF < 0.99911           ##
        ...
        ```
        * will return output:
          * mean_keff=0.99612
          * sigma_keff=0.00100


![Analytics](https://ga-beacon.appspot.com/UA-109580-20/plugin-moret)
