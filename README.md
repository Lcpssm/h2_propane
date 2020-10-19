semiconductor sensor measurements of H2 and Propane

All data available here: https://cloud.mail.ru/public/DSYb/4rDP3QPh5

# 1. Raw data: config & data files

Each observation is represented by of pair of files: 

* **measurement file** `.dat` - e.g.:  `16.03.2019-18.37.32.dat`

|  | Time | T_set1 | T_set2 | T_set_3 | T_set4 | N_cycle | Phase | T1 | R1 | T2 | R2 | T3 | R3 | T4 | R4 | 
| :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- |
| 0 | 0.26 | 100.0 | 150.0 | 150.0 | 150.0 | 1 | 3 | 6.796659 | 1017631.0 | 16.99999 | 3738238.0 | 13.96551 | 364169200.0 | 16.15645 | 138198600.0 |
| 1 | 0.37 | 100.0 | 150.0 | 150.0 | 150.0 | 1 | 3 | 9.633535 | 918182.3 | 21.88888 | 3400904.0 | 19.02298 | 247933100.0 | 20.91836 | 86560560.0 |

- `Time`: time in seconds from start of the experiment (sampling rate ~0.1sec);
- `T_set*`: temperature (Celsius) set by the heater control program, `*` - sensor number (1-4)
- `N_cycle`: the number of measurement period (each cycle ~60sec long; consists of phases 3-4-5-6)
- `Phases`: heater operating modes:
    - 3 - stable-bottom; 
    - 4 - heating;
    - 5 - stable-top;
    - 6 - cooling;
- `T*`: observed temperature (Celsius) `*` - sensor number (1-4);
- `R*`: observed sensor resistance `*` - sensor number (1-4);


* **config file** `.xlsx` - e.g.: `16.03.2019-18.37.32.xlsx`

|  | time | gas | conc ppm |
| :- | :- | :- | :- |
| 0 | 0 | air | 0 |
| 1 | 3600 | H2 | 1600 |
| 2 | 7200 | air | 0 |
| 3 | 10800 | propane | 1600 |

- `time`: time in seconds from start of the experiment 
>    Example: 
>    * 0 row: `0 air 0` -  urban air (any addition gas concentration = 0ppm) was oberved during 0-3600sec from experiment starting
>    * 1 row: `3600 H2 1600` - H2 at concentration 1600ppm was observed at 3600-7200sec
>    * 2 row: `7200 air 0` - air was observed at 7200-10800sec
>    * 3 row: `10800 propane 1600` - propane at concentration 1600ppm was oberved after 10800sec
 
    
- `gas`: observed gas;
- `conc ppm`: gas concentration parts per million.

## 2. Prepared data: R & T observations

Because our main goal - gas classification, we have prepared files where each cycle\period is presented as a separate samples.

You could find files in root folder `./cropped_data`. This folder consists of folders `air, h2, propane` with measurement files for corresponding gas. There are pairs of files (R & T) for each experiment session (config file row number):

Example:
> 2 of numerous files in `./cropped_data/h2/`:
>
> `16.03.2019_R1_1600_num2.csv` & `16.03.2019_T1_1600_num2.csv`
>
> filenames have information about:
> - `23.03.2019` - experiment date;
> - `R` - measurement type (`R` - resistance; `T` - temperatire (Celsius));
> - `1` - sensor number;
> - `1600` - gas concentration;
> - `num2` - row number at **config file** for these measurements subset (here = 2)

The structure of typical observation file (here `16.03.2019_R1_1600_num2.csv`):

|  | 0 | 1 | 2 | 3 | ... | 547 | 548 | 549 | 550 |
| :- | :- | :- | :- | :- | :- | :- | :- | :- | :- |
| 0 | 1600 | 17780.8 | 17669.34 | 17909.73 | ... | 12127.51 | 12351.3 | 12496.23 | 12587.69 |
| 1 | 1600 | 12458.27 | 12427.96 | 12451.9 | ... | 10438.04 | 10489.96 | 10574.12 | 10580.16 |
| 2 | 1600 | 10470.03 | 10603.79 | 10604.77 | ... | 9784.31 | 9763.056 | 9759.589 | 9591.474 |

* first column\row - just dummy indexes;
* **column index** `0` - **gas concentration** (here 1600ppm, as expected from filename);
* each row has **resistance** (temperature, if `T` at filename) values at **column indexes** `1-550` for current cycle\period;

## 3. References
>  *Efitorov A., Andreev M., Krivetskiy V. Metal oxide gas sensors response processing by statistical shape analysis and machine learning algorithm for industrial safety applications. Advances in Neural Computation, Machine Learning, and Cognitive Research IV. V.925 pp.228–233. Springer International Publishing Cham, 2021. https://doi.org/10.1007/978-3-030-60577-3*
