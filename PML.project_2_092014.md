-----------------------------------------
title: Practical Machine Learning Project
-----------------------------------------

###Downloading the data  

```r
setwd("C:\\Users\\hang\\Desktop\\Coursera_5Top\\PracticalMachineLearning\\Project\\") 
```

```
## Error: cannot change working directory
```

```r
if(!file.exists("data")){
	dir.create("data")
}
###downloading "training" data  
fileURL<-"http://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv" ## replace "https" to "http" then worked!
download.file(fileURL, destfile="./data/training.csv")
dateDownloaded<-date()
dateDownloaded
```

```
## [1] "Sun Sep 21 00:03:56 2014"
```

```r
###downloading "testing" data  
fileURL<-"http://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv" ## replace "https" to "http" then worked!
download.file(fileURL, destfile="./data/testing.csv")
dateDownloaded<-date()
dateDownloaded
```

```
## [1] "Sun Sep 21 00:03:56 2014"
```

###Loading the "training" and "testing" data.     


```r
# The "training" data which is named as "d".
d<-read.csv("./data/training.csv", header=TRUE)
dim(d)
```

```
## [1] 19622   160
```

```r
str(d) # 19622 obs. of 160 vars
```

```
## 'data.frame':	19622 obs. of  160 variables:
##  $ X                       : int  1 2 3 4 5 6 7 8 9 10 ...
##  $ user_name               : Factor w/ 6 levels "adelmo","carlitos",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ raw_timestamp_part_1    : int  1323084231 1323084231 1323084231 1323084232 1323084232 1323084232 1323084232 1323084232 1323084232 1323084232 ...
##  $ raw_timestamp_part_2    : int  788290 808298 820366 120339 196328 304277 368296 440390 484323 484434 ...
##  $ cvtd_timestamp          : Factor w/ 20 levels "02/12/2011 13:32",..: 9 9 9 9 9 9 9 9 9 9 ...
##  $ new_window              : Factor w/ 2 levels "no","yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ num_window              : int  11 11 11 12 12 12 12 12 12 12 ...
##  $ roll_belt               : num  1.41 1.41 1.42 1.48 1.48 1.45 1.42 1.42 1.43 1.45 ...
##  $ pitch_belt              : num  8.07 8.07 8.07 8.05 8.07 8.06 8.09 8.13 8.16 8.17 ...
##  $ yaw_belt                : num  -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 ...
##  $ total_accel_belt        : int  3 3 3 3 3 3 3 3 3 3 ...
##  $ kurtosis_roll_belt      : Factor w/ 397 levels "","-0.016850",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ kurtosis_picth_belt     : Factor w/ 317 levels "","-0.021887",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ kurtosis_yaw_belt       : Factor w/ 2 levels "","#DIV/0!": 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_roll_belt      : Factor w/ 395 levels "","-0.003095",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_roll_belt.1    : Factor w/ 338 levels "","-0.005928",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_yaw_belt       : Factor w/ 2 levels "","#DIV/0!": 1 1 1 1 1 1 1 1 1 1 ...
##  $ max_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_picth_belt          : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_yaw_belt            : Factor w/ 68 levels "","-0.1","-0.2",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ min_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_pitch_belt          : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_yaw_belt            : Factor w/ 68 levels "","-0.1","-0.2",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ amplitude_roll_belt     : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_pitch_belt    : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_yaw_belt      : Factor w/ 4 levels "","#DIV/0!","0.00",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ var_total_accel_belt    : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_roll_belt        : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_pitch_belt          : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_pitch_belt       : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_pitch_belt          : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_yaw_belt            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_yaw_belt         : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_yaw_belt            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ gyros_belt_x            : num  0 0.02 0 0.02 0.02 0.02 0.02 0.02 0.02 0.03 ...
##  $ gyros_belt_y            : num  0 0 0 0 0.02 0 0 0 0 0 ...
##  $ gyros_belt_z            : num  -0.02 -0.02 -0.02 -0.03 -0.02 -0.02 -0.02 -0.02 -0.02 0 ...
##  $ accel_belt_x            : int  -21 -22 -20 -22 -21 -21 -22 -22 -20 -21 ...
##  $ accel_belt_y            : int  4 4 5 3 2 4 3 4 2 4 ...
##  $ accel_belt_z            : int  22 22 23 21 24 21 21 21 24 22 ...
##  $ magnet_belt_x           : int  -3 -7 -2 -6 -6 0 -4 -2 1 -3 ...
##  $ magnet_belt_y           : int  599 608 600 604 600 603 599 603 602 609 ...
##  $ magnet_belt_z           : int  -313 -311 -305 -310 -302 -312 -311 -313 -312 -308 ...
##  $ roll_arm                : num  -128 -128 -128 -128 -128 -128 -128 -128 -128 -128 ...
##  $ pitch_arm               : num  22.5 22.5 22.5 22.1 22.1 22 21.9 21.8 21.7 21.6 ...
##  $ yaw_arm                 : num  -161 -161 -161 -161 -161 -161 -161 -161 -161 -161 ...
##  $ total_accel_arm         : int  34 34 34 34 34 34 34 34 34 34 ...
##  $ var_accel_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_roll_arm         : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_pitch_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_pitch_arm        : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_pitch_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_yaw_arm             : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_yaw_arm          : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_yaw_arm             : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ gyros_arm_x             : num  0 0.02 0.02 0.02 0 0.02 0 0.02 0.02 0.02 ...
##  $ gyros_arm_y             : num  0 -0.02 -0.02 -0.03 -0.03 -0.03 -0.03 -0.02 -0.03 -0.03 ...
##  $ gyros_arm_z             : num  -0.02 -0.02 -0.02 0.02 0 0 0 0 -0.02 -0.02 ...
##  $ accel_arm_x             : int  -288 -290 -289 -289 -289 -289 -289 -289 -288 -288 ...
##  $ accel_arm_y             : int  109 110 110 111 111 111 111 111 109 110 ...
##  $ accel_arm_z             : int  -123 -125 -126 -123 -123 -122 -125 -124 -122 -124 ...
##  $ magnet_arm_x            : int  -368 -369 -368 -372 -374 -369 -373 -372 -369 -376 ...
##  $ magnet_arm_y            : int  337 337 344 344 337 342 336 338 341 334 ...
##  $ magnet_arm_z            : int  516 513 513 512 506 513 509 510 518 516 ...
##  $ kurtosis_roll_arm       : Factor w/ 330 levels "","-0.02438",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ kurtosis_picth_arm      : Factor w/ 328 levels "","-0.00484",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ kurtosis_yaw_arm        : Factor w/ 395 levels "","-0.01548",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_roll_arm       : Factor w/ 331 levels "","-0.00051",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_pitch_arm      : Factor w/ 328 levels "","-0.00184",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_yaw_arm        : Factor w/ 395 levels "","-0.00311",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ max_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_picth_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_yaw_arm             : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_pitch_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_yaw_arm             : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_roll_arm      : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_pitch_arm     : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_yaw_arm       : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ roll_dumbbell           : num  13.1 13.1 12.9 13.4 13.4 ...
##  $ pitch_dumbbell          : num  -70.5 -70.6 -70.3 -70.4 -70.4 ...
##  $ yaw_dumbbell            : num  -84.9 -84.7 -85.1 -84.9 -84.9 ...
##  $ kurtosis_roll_dumbbell  : Factor w/ 398 levels "","-0.0035","-0.0073",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ kurtosis_picth_dumbbell : Factor w/ 401 levels "","-0.0163","-0.0233",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ kurtosis_yaw_dumbbell   : Factor w/ 2 levels "","#DIV/0!": 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_roll_dumbbell  : Factor w/ 401 levels "","-0.0082","-0.0096",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_pitch_dumbbell : Factor w/ 402 levels "","-0.0053","-0.0084",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ skewness_yaw_dumbbell   : Factor w/ 2 levels "","#DIV/0!": 1 1 1 1 1 1 1 1 1 1 ...
##  $ max_roll_dumbbell       : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_picth_dumbbell      : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_yaw_dumbbell        : Factor w/ 73 levels "","-0.1","-0.2",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ min_roll_dumbbell       : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_pitch_dumbbell      : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_yaw_dumbbell        : Factor w/ 73 levels "","-0.1","-0.2",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ amplitude_roll_dumbbell : num  NA NA NA NA NA NA NA NA NA NA ...
##   [list output truncated]
```

```r
summary(d) # the last var "classe" is outcome to be predicted.
```

```
##        X            user_name    raw_timestamp_part_1 raw_timestamp_part_2
##  Min.   :    1   adelmo  :3892   Min.   :1.32e+09     Min.   :   294      
##  1st Qu.: 4906   carlitos:3112   1st Qu.:1.32e+09     1st Qu.:252912      
##  Median : 9812   charles :3536   Median :1.32e+09     Median :496380      
##  Mean   : 9812   eurico  :3070   Mean   :1.32e+09     Mean   :500656      
##  3rd Qu.:14717   jeremy  :3402   3rd Qu.:1.32e+09     3rd Qu.:751891      
##  Max.   :19622   pedro   :2610   Max.   :1.32e+09     Max.   :998801      
##                                                                           
##           cvtd_timestamp  new_window    num_window    roll_belt    
##  28/11/2011 14:14: 1498   no :19216   Min.   :  1   Min.   :-28.9  
##  05/12/2011 11:24: 1497   yes:  406   1st Qu.:222   1st Qu.:  1.1  
##  30/11/2011 17:11: 1440               Median :424   Median :113.0  
##  05/12/2011 11:25: 1425               Mean   :431   Mean   : 64.4  
##  02/12/2011 14:57: 1380               3rd Qu.:644   3rd Qu.:123.0  
##  02/12/2011 13:34: 1375               Max.   :864   Max.   :162.0  
##  (Other)         :11007                                            
##    pitch_belt        yaw_belt      total_accel_belt kurtosis_roll_belt
##  Min.   :-55.80   Min.   :-180.0   Min.   : 0.0              :19216   
##  1st Qu.:  1.76   1st Qu.: -88.3   1st Qu.: 3.0     #DIV/0!  :   10   
##  Median :  5.28   Median : -13.0   Median :17.0     -1.908453:    2   
##  Mean   :  0.31   Mean   : -11.2   Mean   :11.3     -0.016850:    1   
##  3rd Qu.: 14.90   3rd Qu.:  12.9   3rd Qu.:18.0     -0.021024:    1   
##  Max.   : 60.30   Max.   : 179.0   Max.   :29.0     -0.025513:    1   
##                                                     (Other)  :  391   
##  kurtosis_picth_belt kurtosis_yaw_belt skewness_roll_belt
##           :19216            :19216              :19216   
##  #DIV/0!  :   32     #DIV/0!:  406     #DIV/0!  :    9   
##  47.000000:    4                       0.000000 :    4   
##  -0.150950:    3                       0.422463 :    2   
##  -0.684748:    3                       -0.003095:    1   
##  -1.750749:    3                       -0.010002:    1   
##  (Other)  :  361                       (Other)  :  389   
##  skewness_roll_belt.1 skewness_yaw_belt max_roll_belt   max_picth_belt 
##           :19216             :19216     Min.   :-94     Min.   : 3     
##  #DIV/0!  :   32      #DIV/0!:  406     1st Qu.:-88     1st Qu.: 5     
##  0.000000 :    4                        Median : -5     Median :18     
##  -2.156553:    3                        Mean   : -7     Mean   :13     
##  -3.072669:    3                        3rd Qu.: 18     3rd Qu.:19     
##  -6.324555:    3                        Max.   :180     Max.   :30     
##  (Other)  :  361                        NA's   :19216   NA's   :19216  
##   max_yaw_belt   min_roll_belt   min_pitch_belt   min_yaw_belt  
##         :19216   Min.   :-180    Min.   : 0             :19216  
##  -1.1   :   30   1st Qu.: -88    1st Qu.: 3      -1.1   :   30  
##  -1.4   :   29   Median :  -8    Median :16      -1.4   :   29  
##  -1.2   :   26   Mean   : -10    Mean   :11      -1.2   :   26  
##  -0.9   :   24   3rd Qu.:   9    3rd Qu.:17      -0.9   :   24  
##  -1.3   :   22   Max.   : 173    Max.   :23      -1.3   :   22  
##  (Other):  275   NA's   :19216   NA's   :19216   (Other):  275  
##  amplitude_roll_belt amplitude_pitch_belt amplitude_yaw_belt
##  Min.   :  0         Min.   : 0                  :19216     
##  1st Qu.:  0         1st Qu.: 1           #DIV/0!:   10     
##  Median :  1         Median : 1           0.00   :   12     
##  Mean   :  4         Mean   : 2           0.0000 :  384     
##  3rd Qu.:  2         3rd Qu.: 2                             
##  Max.   :360         Max.   :12                             
##  NA's   :19216       NA's   :19216                          
##  var_total_accel_belt avg_roll_belt   stddev_roll_belt var_roll_belt  
##  Min.   : 0           Min.   :-27     Min.   : 0       Min.   :  0    
##  1st Qu.: 0           1st Qu.:  1     1st Qu.: 0       1st Qu.:  0    
##  Median : 0           Median :116     Median : 0       Median :  0    
##  Mean   : 1           Mean   : 68     Mean   : 1       Mean   :  8    
##  3rd Qu.: 0           3rd Qu.:123     3rd Qu.: 1       3rd Qu.:  0    
##  Max.   :16           Max.   :157     Max.   :14       Max.   :201    
##  NA's   :19216        NA's   :19216   NA's   :19216    NA's   :19216  
##  avg_pitch_belt  stddev_pitch_belt var_pitch_belt   avg_yaw_belt  
##  Min.   :-51     Min.   :0         Min.   : 0      Min.   :-138   
##  1st Qu.:  2     1st Qu.:0         1st Qu.: 0      1st Qu.: -88   
##  Median :  5     Median :0         Median : 0      Median :  -7   
##  Mean   :  1     Mean   :1         Mean   : 1      Mean   :  -9   
##  3rd Qu.: 16     3rd Qu.:1         3rd Qu.: 0      3rd Qu.:  14   
##  Max.   : 60     Max.   :4         Max.   :16      Max.   : 174   
##  NA's   :19216   NA's   :19216     NA's   :19216   NA's   :19216  
##  stddev_yaw_belt  var_yaw_belt    gyros_belt_x      gyros_belt_y    
##  Min.   :  0     Min.   :    0   Min.   :-1.0400   Min.   :-0.6400  
##  1st Qu.:  0     1st Qu.:    0   1st Qu.:-0.0300   1st Qu.: 0.0000  
##  Median :  0     Median :    0   Median : 0.0300   Median : 0.0200  
##  Mean   :  1     Mean   :  107   Mean   :-0.0056   Mean   : 0.0396  
##  3rd Qu.:  1     3rd Qu.:    0   3rd Qu.: 0.1100   3rd Qu.: 0.1100  
##  Max.   :177     Max.   :31183   Max.   : 2.2200   Max.   : 0.6400  
##  NA's   :19216   NA's   :19216                                      
##   gyros_belt_z     accel_belt_x      accel_belt_y    accel_belt_z   
##  Min.   :-1.460   Min.   :-120.00   Min.   :-69.0   Min.   :-275.0  
##  1st Qu.:-0.200   1st Qu.: -21.00   1st Qu.:  3.0   1st Qu.:-162.0  
##  Median :-0.100   Median : -15.00   Median : 35.0   Median :-152.0  
##  Mean   :-0.130   Mean   :  -5.59   Mean   : 30.1   Mean   : -72.6  
##  3rd Qu.:-0.020   3rd Qu.:  -5.00   3rd Qu.: 61.0   3rd Qu.:  27.0  
##  Max.   : 1.620   Max.   :  85.00   Max.   :164.0   Max.   : 105.0  
##                                                                     
##  magnet_belt_x   magnet_belt_y magnet_belt_z     roll_arm     
##  Min.   :-52.0   Min.   :354   Min.   :-623   Min.   :-180.0  
##  1st Qu.:  9.0   1st Qu.:581   1st Qu.:-375   1st Qu.: -31.8  
##  Median : 35.0   Median :601   Median :-320   Median :   0.0  
##  Mean   : 55.6   Mean   :594   Mean   :-346   Mean   :  17.8  
##  3rd Qu.: 59.0   3rd Qu.:610   3rd Qu.:-306   3rd Qu.:  77.3  
##  Max.   :485.0   Max.   :673   Max.   : 293   Max.   : 180.0  
##                                                               
##    pitch_arm         yaw_arm        total_accel_arm var_accel_arm  
##  Min.   :-88.80   Min.   :-180.00   Min.   : 1.0    Min.   :  0    
##  1st Qu.:-25.90   1st Qu.: -43.10   1st Qu.:17.0    1st Qu.:  9    
##  Median :  0.00   Median :   0.00   Median :27.0    Median : 41    
##  Mean   : -4.61   Mean   :  -0.62   Mean   :25.5    Mean   : 53    
##  3rd Qu.: 11.20   3rd Qu.:  45.88   3rd Qu.:33.0    3rd Qu.: 76    
##  Max.   : 88.50   Max.   : 180.00   Max.   :66.0    Max.   :332    
##                                                     NA's   :19216  
##   avg_roll_arm   stddev_roll_arm  var_roll_arm   avg_pitch_arm  
##  Min.   :-167    Min.   :  0     Min.   :    0   Min.   :-82    
##  1st Qu.: -38    1st Qu.:  1     1st Qu.:    2   1st Qu.:-23    
##  Median :   0    Median :  6     Median :   33   Median :  0    
##  Mean   :  13    Mean   : 11     Mean   :  417   Mean   : -5    
##  3rd Qu.:  76    3rd Qu.: 15     3rd Qu.:  223   3rd Qu.:  8    
##  Max.   : 163    Max.   :162     Max.   :26232   Max.   : 76    
##  NA's   :19216   NA's   :19216   NA's   :19216   NA's   :19216  
##  stddev_pitch_arm var_pitch_arm    avg_yaw_arm    stddev_yaw_arm 
##  Min.   : 0       Min.   :   0    Min.   :-173    Min.   :  0    
##  1st Qu.: 2       1st Qu.:   3    1st Qu.: -29    1st Qu.:  3    
##  Median : 8       Median :  66    Median :   0    Median : 17    
##  Mean   :10       Mean   : 196    Mean   :   2    Mean   : 22    
##  3rd Qu.:16       3rd Qu.: 267    3rd Qu.:  38    3rd Qu.: 36    
##  Max.   :43       Max.   :1885    Max.   : 152    Max.   :177    
##  NA's   :19216    NA's   :19216   NA's   :19216   NA's   :19216  
##   var_yaw_arm     gyros_arm_x      gyros_arm_y      gyros_arm_z   
##  Min.   :    0   Min.   :-6.370   Min.   :-3.440   Min.   :-2.33  
##  1st Qu.:    7   1st Qu.:-1.330   1st Qu.:-0.800   1st Qu.:-0.07  
##  Median :  278   Median : 0.080   Median :-0.240   Median : 0.23  
##  Mean   : 1056   Mean   : 0.043   Mean   :-0.257   Mean   : 0.27  
##  3rd Qu.: 1295   3rd Qu.: 1.570   3rd Qu.: 0.140   3rd Qu.: 0.72  
##  Max.   :31345   Max.   : 4.870   Max.   : 2.840   Max.   : 3.02  
##  NA's   :19216                                                    
##   accel_arm_x      accel_arm_y      accel_arm_z      magnet_arm_x 
##  Min.   :-404.0   Min.   :-318.0   Min.   :-636.0   Min.   :-584  
##  1st Qu.:-242.0   1st Qu.: -54.0   1st Qu.:-143.0   1st Qu.:-300  
##  Median : -44.0   Median :  14.0   Median : -47.0   Median : 289  
##  Mean   : -60.2   Mean   :  32.6   Mean   : -71.2   Mean   : 192  
##  3rd Qu.:  84.0   3rd Qu.: 139.0   3rd Qu.:  23.0   3rd Qu.: 637  
##  Max.   : 437.0   Max.   : 308.0   Max.   : 292.0   Max.   : 782  
##                                                                   
##   magnet_arm_y   magnet_arm_z  kurtosis_roll_arm kurtosis_picth_arm
##  Min.   :-392   Min.   :-597           :19216            :19216    
##  1st Qu.:  -9   1st Qu.: 131   #DIV/0! :   78    #DIV/0! :   80    
##  Median : 202   Median : 444   -0.02438:    1    -0.00484:    1    
##  Mean   : 157   Mean   : 306   -0.04190:    1    -0.01311:    1    
##  3rd Qu.: 323   3rd Qu.: 545   -0.05051:    1    -0.02967:    1    
##  Max.   : 583   Max.   : 694   -0.05695:    1    -0.07394:    1    
##                                (Other) :  324    (Other) :  322    
##  kurtosis_yaw_arm skewness_roll_arm skewness_pitch_arm skewness_yaw_arm
##          :19216           :19216            :19216             :19216  
##  #DIV/0! :   11   #DIV/0! :   77    #DIV/0! :   80     #DIV/0! :   11  
##  0.55844 :    2   -0.00051:    1    -0.00184:    1     -1.62032:    2  
##  0.65132 :    2   -0.00696:    1    -0.01185:    1     0.55053 :    2  
##  -0.01548:    1   -0.01884:    1    -0.01247:    1     -0.00311:    1  
##  -0.01749:    1   -0.03359:    1    -0.02063:    1     -0.00562:    1  
##  (Other) :  389   (Other) :  325    (Other) :  322     (Other) :  389  
##   max_roll_arm   max_picth_arm    max_yaw_arm     min_roll_arm  
##  Min.   :-73     Min.   :-173    Min.   : 4      Min.   :-89    
##  1st Qu.:  0     1st Qu.:  -2    1st Qu.:29      1st Qu.:-42    
##  Median :  5     Median :  23    Median :34      Median :-22    
##  Mean   : 11     Mean   :  36    Mean   :35      Mean   :-21    
##  3rd Qu.: 27     3rd Qu.:  96    3rd Qu.:41      3rd Qu.:  0    
##  Max.   : 86     Max.   : 180    Max.   :65      Max.   : 66    
##  NA's   :19216   NA's   :19216   NA's   :19216   NA's   :19216  
##  min_pitch_arm    min_yaw_arm    amplitude_roll_arm amplitude_pitch_arm
##  Min.   :-180    Min.   : 1      Min.   :  0        Min.   :  0        
##  1st Qu.: -73    1st Qu.: 8      1st Qu.:  5        1st Qu.: 10        
##  Median : -34    Median :13      Median : 28        Median : 55        
##  Mean   : -34    Mean   :15      Mean   : 32        Mean   : 70        
##  3rd Qu.:   0    3rd Qu.:19      3rd Qu.: 51        3rd Qu.:115        
##  Max.   : 152    Max.   :38      Max.   :120        Max.   :360        
##  NA's   :19216   NA's   :19216   NA's   :19216      NA's   :19216      
##  amplitude_yaw_arm roll_dumbbell    pitch_dumbbell    yaw_dumbbell    
##  Min.   : 0        Min.   :-153.7   Min.   :-149.6   Min.   :-150.87  
##  1st Qu.:13        1st Qu.: -18.5   1st Qu.: -40.9   1st Qu.: -77.64  
##  Median :22        Median :  48.2   Median : -21.0   Median :  -3.32  
##  Mean   :21        Mean   :  23.8   Mean   : -10.8   Mean   :   1.67  
##  3rd Qu.:29        3rd Qu.:  67.6   3rd Qu.:  17.5   3rd Qu.:  79.64  
##  Max.   :52        Max.   : 153.6   Max.   : 149.4   Max.   : 154.95  
##  NA's   :19216                                                        
##  kurtosis_roll_dumbbell kurtosis_picth_dumbbell kurtosis_yaw_dumbbell
##         :19216                 :19216                  :19216        
##  #DIV/0!:    5          -0.5464:    2           #DIV/0!:  406        
##  -0.2583:    2          -0.9334:    2                                
##  -0.3705:    2          -2.0833:    2                                
##  -0.5855:    2          -2.0851:    2                                
##  -2.0851:    2          -2.0889:    2                                
##  (Other):  393          (Other):  396                                
##  skewness_roll_dumbbell skewness_pitch_dumbbell skewness_yaw_dumbbell
##         :19216                 :19216                  :19216        
##  #DIV/0!:    4          -0.2328:    2           #DIV/0!:  406        
##  -0.9324:    2          -0.3521:    2                                
##  0.1110 :    2          -0.7036:    2                                
##  1.0312 :    2          0.1090 :    2                                
##  -0.0082:    1          1.0326 :    2                                
##  (Other):  395          (Other):  396                                
##  max_roll_dumbbell max_picth_dumbbell max_yaw_dumbbell min_roll_dumbbell
##  Min.   :-70       Min.   :-113              :19216    Min.   :-150     
##  1st Qu.:-27       1st Qu.: -67       -0.6   :   20    1st Qu.: -60     
##  Median : 15       Median :  40       0.2    :   19    Median : -44     
##  Mean   : 14       Mean   :  33       -0.8   :   18    Mean   : -41     
##  3rd Qu.: 51       3rd Qu.: 133       -0.3   :   16    3rd Qu.: -25     
##  Max.   :137       Max.   : 155       -0.2   :   15    Max.   :  73     
##  NA's   :19216     NA's   :19216      (Other):  318    NA's   :19216    
##  min_pitch_dumbbell min_yaw_dumbbell amplitude_roll_dumbbell
##  Min.   :-147              :19216    Min.   :  0            
##  1st Qu.: -92       -0.6   :   20    1st Qu.: 15            
##  Median : -66       0.2    :   19    Median : 35            
##  Mean   : -33       -0.8   :   18    Mean   : 55            
##  3rd Qu.:  21       -0.3   :   16    3rd Qu.: 81            
##  Max.   : 121       -0.2   :   15    Max.   :256            
##  NA's   :19216      (Other):  318    NA's   :19216          
##  amplitude_pitch_dumbbell amplitude_yaw_dumbbell total_accel_dumbbell
##  Min.   :  0                     :19216          Min.   : 0.0        
##  1st Qu.: 17              #DIV/0!:    5          1st Qu.: 4.0        
##  Median : 42              0.00   :  401          Median :10.0        
##  Mean   : 66                                     Mean   :13.7        
##  3rd Qu.:100                                     3rd Qu.:19.0        
##  Max.   :274                                     Max.   :58.0        
##  NA's   :19216                                                       
##  var_accel_dumbbell avg_roll_dumbbell stddev_roll_dumbbell
##  Min.   :  0        Min.   :-129      Min.   :  0         
##  1st Qu.:  0        1st Qu.: -12      1st Qu.:  5         
##  Median :  1        Median :  48      Median : 12         
##  Mean   :  4        Mean   :  24      Mean   : 21         
##  3rd Qu.:  3        3rd Qu.:  64      3rd Qu.: 26         
##  Max.   :230        Max.   : 126      Max.   :124         
##  NA's   :19216      NA's   :19216     NA's   :19216       
##  var_roll_dumbbell avg_pitch_dumbbell stddev_pitch_dumbbell
##  Min.   :    0     Min.   :-71        Min.   : 0           
##  1st Qu.:   22     1st Qu.:-42        1st Qu.: 3           
##  Median :  149     Median :-20        Median : 8           
##  Mean   : 1020     Mean   :-12        Mean   :13           
##  3rd Qu.:  695     3rd Qu.: 13        3rd Qu.:19           
##  Max.   :15321     Max.   : 94        Max.   :83           
##  NA's   :19216     NA's   :19216      NA's   :19216        
##  var_pitch_dumbbell avg_yaw_dumbbell stddev_yaw_dumbbell var_yaw_dumbbell
##  Min.   :   0       Min.   :-118     Min.   :  0         Min.   :    0   
##  1st Qu.:  12       1st Qu.: -77     1st Qu.:  4         1st Qu.:   15   
##  Median :  65       Median :  -5     Median : 10         Median :  105   
##  Mean   : 350       Mean   :   0     Mean   : 17         Mean   :  590   
##  3rd Qu.: 370       3rd Qu.:  71     3rd Qu.: 25         3rd Qu.:  609   
##  Max.   :6836       Max.   : 135     Max.   :107         Max.   :11468   
##  NA's   :19216      NA's   :19216    NA's   :19216       NA's   :19216   
##  gyros_dumbbell_x  gyros_dumbbell_y gyros_dumbbell_z accel_dumbbell_x
##  Min.   :-204.00   Min.   :-2.10    Min.   : -2.4    Min.   :-419.0  
##  1st Qu.:  -0.03   1st Qu.:-0.14    1st Qu.: -0.3    1st Qu.: -50.0  
##  Median :   0.13   Median : 0.03    Median : -0.1    Median :  -8.0  
##  Mean   :   0.16   Mean   : 0.05    Mean   : -0.1    Mean   : -28.6  
##  3rd Qu.:   0.35   3rd Qu.: 0.21    3rd Qu.:  0.0    3rd Qu.:  11.0  
##  Max.   :   2.22   Max.   :52.00    Max.   :317.0    Max.   : 235.0  
##                                                                      
##  accel_dumbbell_y accel_dumbbell_z magnet_dumbbell_x magnet_dumbbell_y
##  Min.   :-189.0   Min.   :-334.0   Min.   :-643      Min.   :-3600    
##  1st Qu.:  -8.0   1st Qu.:-142.0   1st Qu.:-535      1st Qu.:  231    
##  Median :  41.5   Median :  -1.0   Median :-479      Median :  311    
##  Mean   :  52.6   Mean   : -38.3   Mean   :-328      Mean   :  221    
##  3rd Qu.: 111.0   3rd Qu.:  38.0   3rd Qu.:-304      3rd Qu.:  390    
##  Max.   : 315.0   Max.   : 318.0   Max.   : 592      Max.   :  633    
##                                                                       
##  magnet_dumbbell_z  roll_forearm     pitch_forearm     yaw_forearm    
##  Min.   :-262.0    Min.   :-180.00   Min.   :-72.50   Min.   :-180.0  
##  1st Qu.: -45.0    1st Qu.:  -0.74   1st Qu.:  0.00   1st Qu.: -68.6  
##  Median :  13.0    Median :  21.70   Median :  9.24   Median :   0.0  
##  Mean   :  46.1    Mean   :  33.83   Mean   : 10.71   Mean   :  19.2  
##  3rd Qu.:  95.0    3rd Qu.: 140.00   3rd Qu.: 28.40   3rd Qu.: 110.0  
##  Max.   : 452.0    Max.   : 180.00   Max.   : 89.80   Max.   : 180.0  
##                                                                       
##  kurtosis_roll_forearm kurtosis_picth_forearm kurtosis_yaw_forearm
##         :19216                :19216                 :19216       
##  #DIV/0!:   84         #DIV/0!:   85          #DIV/0!:  406       
##  -0.8079:    2         -0.0073:    1                              
##  -0.9169:    2         -0.0442:    1                              
##  -0.0227:    1         -0.0489:    1                              
##  -0.0359:    1         -0.0523:    1                              
##  (Other):  316         (Other):  317                              
##  skewness_roll_forearm skewness_pitch_forearm skewness_yaw_forearm
##         :19216                :19216                 :19216       
##  #DIV/0!:   83         #DIV/0!:   85          #DIV/0!:  406       
##  -0.1912:    2         0.0000 :    4                              
##  -0.4126:    2         -0.6992:    2                              
##  -0.0004:    1         -0.0113:    1                              
##  -0.0013:    1         -0.0131:    1                              
##  (Other):  317         (Other):  313                              
##  max_roll_forearm max_picth_forearm max_yaw_forearm min_roll_forearm
##  Min.   :-67      Min.   :-151             :19216   Min.   :-72     
##  1st Qu.:  0      1st Qu.:   0      #DIV/0!:   84   1st Qu.: -6     
##  Median : 27      Median : 113      -1.2   :   32   Median :  0     
##  Mean   : 24      Mean   :  81      -1.3   :   31   Mean   :  0     
##  3rd Qu.: 46      3rd Qu.: 175      -1.4   :   24   3rd Qu.: 12     
##  Max.   : 90      Max.   : 180      -1.5   :   24   Max.   : 62     
##  NA's   :19216    NA's   :19216     (Other):  211   NA's   :19216   
##  min_pitch_forearm min_yaw_forearm amplitude_roll_forearm
##  Min.   :-180             :19216   Min.   :  0           
##  1st Qu.:-175      #DIV/0!:   84   1st Qu.:  1           
##  Median : -61      -1.2   :   32   Median : 18           
##  Mean   : -58      -1.3   :   31   Mean   : 25           
##  3rd Qu.:   0      -1.4   :   24   3rd Qu.: 40           
##  Max.   : 167      -1.5   :   24   Max.   :126           
##  NA's   :19216     (Other):  211   NA's   :19216         
##  amplitude_pitch_forearm amplitude_yaw_forearm total_accel_forearm
##  Min.   :  0                    :19216         Min.   :  0.0      
##  1st Qu.:  2             #DIV/0!:   84         1st Qu.: 29.0      
##  Median : 84             0.00   :  322         Median : 36.0      
##  Mean   :139                                   Mean   : 34.7      
##  3rd Qu.:350                                   3rd Qu.: 41.0      
##  Max.   :360                                   Max.   :108.0      
##  NA's   :19216                                                    
##  var_accel_forearm avg_roll_forearm stddev_roll_forearm var_roll_forearm
##  Min.   :  0       Min.   :-177     Min.   :  0         Min.   :    0   
##  1st Qu.:  7       1st Qu.:  -1     1st Qu.:  0         1st Qu.:    0   
##  Median : 21       Median :  11     Median :  8         Median :   64   
##  Mean   : 34       Mean   :  33     Mean   : 42         Mean   : 5274   
##  3rd Qu.: 51       3rd Qu.: 107     3rd Qu.: 85         3rd Qu.: 7289   
##  Max.   :173       Max.   : 177     Max.   :179         Max.   :32102   
##  NA's   :19216     NA's   :19216    NA's   :19216       NA's   :19216   
##  avg_pitch_forearm stddev_pitch_forearm var_pitch_forearm avg_yaw_forearm
##  Min.   :-68       Min.   : 0           Min.   :   0      Min.   :-155   
##  1st Qu.:  0       1st Qu.: 0           1st Qu.:   0      1st Qu.: -26   
##  Median : 12       Median : 6           Median :  30      Median :   0   
##  Mean   : 12       Mean   : 8           Mean   : 140      Mean   :  18   
##  3rd Qu.: 28       3rd Qu.:13           3rd Qu.: 166      3rd Qu.:  86   
##  Max.   : 72       Max.   :48           Max.   :2280      Max.   : 169   
##  NA's   :19216     NA's   :19216        NA's   :19216     NA's   :19216  
##  stddev_yaw_forearm var_yaw_forearm gyros_forearm_x   gyros_forearm_y 
##  Min.   :  0        Min.   :    0   Min.   :-22.000   Min.   : -7.02  
##  1st Qu.:  1        1st Qu.:    0   1st Qu.: -0.220   1st Qu.: -1.46  
##  Median : 25        Median :  612   Median :  0.050   Median :  0.03  
##  Mean   : 45        Mean   : 4640   Mean   :  0.158   Mean   :  0.08  
##  3rd Qu.: 86        3rd Qu.: 7368   3rd Qu.:  0.560   3rd Qu.:  1.62  
##  Max.   :198        Max.   :39009   Max.   :  3.970   Max.   :311.00  
##  NA's   :19216      NA's   :19216                                     
##  gyros_forearm_z  accel_forearm_x  accel_forearm_y accel_forearm_z 
##  Min.   : -8.09   Min.   :-498.0   Min.   :-632    Min.   :-446.0  
##  1st Qu.: -0.18   1st Qu.:-178.0   1st Qu.:  57    1st Qu.:-182.0  
##  Median :  0.08   Median : -57.0   Median : 201    Median : -39.0  
##  Mean   :  0.15   Mean   : -61.7   Mean   : 164    Mean   : -55.3  
##  3rd Qu.:  0.49   3rd Qu.:  76.0   3rd Qu.: 312    3rd Qu.:  26.0  
##  Max.   :231.00   Max.   : 477.0   Max.   : 923    Max.   : 291.0  
##                                                                    
##  magnet_forearm_x magnet_forearm_y magnet_forearm_z classe  
##  Min.   :-1280    Min.   :-896     Min.   :-973     A:5580  
##  1st Qu.: -616    1st Qu.:   2     1st Qu.: 191     B:3797  
##  Median : -378    Median : 591     Median : 511     C:3422  
##  Mean   : -313    Mean   : 380     Mean   : 394     D:3216  
##  3rd Qu.:  -73    3rd Qu.: 737     3rd Qu.: 653     E:3607  
##  Max.   :  672    Max.   :1480     Max.   :1090             
## 
```

```r
# The "testing" data which is named as "d2".
d2<-read.csv("./data/testing.csv", header=TRUE)
dim(d2)
```

```
## [1]  20 160
```

```r
str(d2) # 20 obs. of 160 vars
```

```
## 'data.frame':	20 obs. of  160 variables:
##  $ X                       : int  1 2 3 4 5 6 7 8 9 10 ...
##  $ user_name               : Factor w/ 6 levels "adelmo","carlitos",..: 6 5 5 1 4 5 5 5 2 3 ...
##  $ raw_timestamp_part_1    : int  1323095002 1322673067 1322673075 1322832789 1322489635 1322673149 1322673128 1322673076 1323084240 1322837822 ...
##  $ raw_timestamp_part_2    : int  868349 778725 342967 560311 814776 510661 766645 54671 916313 384285 ...
##  $ cvtd_timestamp          : Factor w/ 11 levels "02/12/2011 13:33",..: 5 10 10 1 6 11 11 10 3 2 ...
##  $ new_window              : Factor w/ 1 level "no": 1 1 1 1 1 1 1 1 1 1 ...
##  $ num_window              : int  74 431 439 194 235 504 485 440 323 664 ...
##  $ roll_belt               : num  123 1.02 0.87 125 1.35 -5.92 1.2 0.43 0.93 114 ...
##  $ pitch_belt              : num  27 4.87 1.82 -41.6 3.33 1.59 4.44 4.15 6.72 22.4 ...
##  $ yaw_belt                : num  -4.75 -88.9 -88.5 162 -88.6 -87.7 -87.3 -88.5 -93.7 -13.1 ...
##  $ total_accel_belt        : int  20 4 5 17 3 4 4 4 4 18 ...
##  $ kurtosis_roll_belt      : logi  NA NA NA NA NA NA ...
##  $ kurtosis_picth_belt     : logi  NA NA NA NA NA NA ...
##  $ kurtosis_yaw_belt       : logi  NA NA NA NA NA NA ...
##  $ skewness_roll_belt      : logi  NA NA NA NA NA NA ...
##  $ skewness_roll_belt.1    : logi  NA NA NA NA NA NA ...
##  $ skewness_yaw_belt       : logi  NA NA NA NA NA NA ...
##  $ max_roll_belt           : logi  NA NA NA NA NA NA ...
##  $ max_picth_belt          : logi  NA NA NA NA NA NA ...
##  $ max_yaw_belt            : logi  NA NA NA NA NA NA ...
##  $ min_roll_belt           : logi  NA NA NA NA NA NA ...
##  $ min_pitch_belt          : logi  NA NA NA NA NA NA ...
##  $ min_yaw_belt            : logi  NA NA NA NA NA NA ...
##  $ amplitude_roll_belt     : logi  NA NA NA NA NA NA ...
##  $ amplitude_pitch_belt    : logi  NA NA NA NA NA NA ...
##  $ amplitude_yaw_belt      : logi  NA NA NA NA NA NA ...
##  $ var_total_accel_belt    : logi  NA NA NA NA NA NA ...
##  $ avg_roll_belt           : logi  NA NA NA NA NA NA ...
##  $ stddev_roll_belt        : logi  NA NA NA NA NA NA ...
##  $ var_roll_belt           : logi  NA NA NA NA NA NA ...
##  $ avg_pitch_belt          : logi  NA NA NA NA NA NA ...
##  $ stddev_pitch_belt       : logi  NA NA NA NA NA NA ...
##  $ var_pitch_belt          : logi  NA NA NA NA NA NA ...
##  $ avg_yaw_belt            : logi  NA NA NA NA NA NA ...
##  $ stddev_yaw_belt         : logi  NA NA NA NA NA NA ...
##  $ var_yaw_belt            : logi  NA NA NA NA NA NA ...
##  $ gyros_belt_x            : num  -0.5 -0.06 0.05 0.11 0.03 0.1 -0.06 -0.18 0.1 0.14 ...
##  $ gyros_belt_y            : num  -0.02 -0.02 0.02 0.11 0.02 0.05 0 -0.02 0 0.11 ...
##  $ gyros_belt_z            : num  -0.46 -0.07 0.03 -0.16 0 -0.13 0 -0.03 -0.02 -0.16 ...
##  $ accel_belt_x            : int  -38 -13 1 46 -8 -11 -14 -10 -15 -25 ...
##  $ accel_belt_y            : int  69 11 -1 45 4 -16 2 -2 1 63 ...
##  $ accel_belt_z            : int  -179 39 49 -156 27 38 35 42 32 -158 ...
##  $ magnet_belt_x           : int  -13 43 29 169 33 31 50 39 -6 10 ...
##  $ magnet_belt_y           : int  581 636 631 608 566 638 622 635 600 601 ...
##  $ magnet_belt_z           : int  -382 -309 -312 -304 -418 -291 -315 -305 -302 -330 ...
##  $ roll_arm                : num  40.7 0 0 -109 76.1 0 0 0 -137 -82.4 ...
##  $ pitch_arm               : num  -27.8 0 0 55 2.76 0 0 0 11.2 -63.8 ...
##  $ yaw_arm                 : num  178 0 0 -142 102 0 0 0 -167 -75.3 ...
##  $ total_accel_arm         : int  10 38 44 25 29 14 15 22 34 32 ...
##  $ var_accel_arm           : logi  NA NA NA NA NA NA ...
##  $ avg_roll_arm            : logi  NA NA NA NA NA NA ...
##  $ stddev_roll_arm         : logi  NA NA NA NA NA NA ...
##  $ var_roll_arm            : logi  NA NA NA NA NA NA ...
##  $ avg_pitch_arm           : logi  NA NA NA NA NA NA ...
##  $ stddev_pitch_arm        : logi  NA NA NA NA NA NA ...
##  $ var_pitch_arm           : logi  NA NA NA NA NA NA ...
##  $ avg_yaw_arm             : logi  NA NA NA NA NA NA ...
##  $ stddev_yaw_arm          : logi  NA NA NA NA NA NA ...
##  $ var_yaw_arm             : logi  NA NA NA NA NA NA ...
##  $ gyros_arm_x             : num  -1.65 -1.17 2.1 0.22 -1.96 0.02 2.36 -3.71 0.03 0.26 ...
##  $ gyros_arm_y             : num  0.48 0.85 -1.36 -0.51 0.79 0.05 -1.01 1.85 -0.02 -0.5 ...
##  $ gyros_arm_z             : num  -0.18 -0.43 1.13 0.92 -0.54 -0.07 0.89 -0.69 -0.02 0.79 ...
##  $ accel_arm_x             : int  16 -290 -341 -238 -197 -26 99 -98 -287 -301 ...
##  $ accel_arm_y             : int  38 215 245 -57 200 130 79 175 111 -42 ...
##  $ accel_arm_z             : int  93 -90 -87 6 -30 -19 -67 -78 -122 -80 ...
##  $ magnet_arm_x            : int  -326 -325 -264 -173 -170 396 702 535 -367 -420 ...
##  $ magnet_arm_y            : int  385 447 474 257 275 176 15 215 335 294 ...
##  $ magnet_arm_z            : int  481 434 413 633 617 516 217 385 520 493 ...
##  $ kurtosis_roll_arm       : logi  NA NA NA NA NA NA ...
##  $ kurtosis_picth_arm      : logi  NA NA NA NA NA NA ...
##  $ kurtosis_yaw_arm        : logi  NA NA NA NA NA NA ...
##  $ skewness_roll_arm       : logi  NA NA NA NA NA NA ...
##  $ skewness_pitch_arm      : logi  NA NA NA NA NA NA ...
##  $ skewness_yaw_arm        : logi  NA NA NA NA NA NA ...
##  $ max_roll_arm            : logi  NA NA NA NA NA NA ...
##  $ max_picth_arm           : logi  NA NA NA NA NA NA ...
##  $ max_yaw_arm             : logi  NA NA NA NA NA NA ...
##  $ min_roll_arm            : logi  NA NA NA NA NA NA ...
##  $ min_pitch_arm           : logi  NA NA NA NA NA NA ...
##  $ min_yaw_arm             : logi  NA NA NA NA NA NA ...
##  $ amplitude_roll_arm      : logi  NA NA NA NA NA NA ...
##  $ amplitude_pitch_arm     : logi  NA NA NA NA NA NA ...
##  $ amplitude_yaw_arm       : logi  NA NA NA NA NA NA ...
##  $ roll_dumbbell           : num  -17.7 54.5 57.1 43.1 -101.4 ...
##  $ pitch_dumbbell          : num  25 -53.7 -51.4 -30 -53.4 ...
##  $ yaw_dumbbell            : num  126.2 -75.5 -75.2 -103.3 -14.2 ...
##  $ kurtosis_roll_dumbbell  : logi  NA NA NA NA NA NA ...
##  $ kurtosis_picth_dumbbell : logi  NA NA NA NA NA NA ...
##  $ kurtosis_yaw_dumbbell   : logi  NA NA NA NA NA NA ...
##  $ skewness_roll_dumbbell  : logi  NA NA NA NA NA NA ...
##  $ skewness_pitch_dumbbell : logi  NA NA NA NA NA NA ...
##  $ skewness_yaw_dumbbell   : logi  NA NA NA NA NA NA ...
##  $ max_roll_dumbbell       : logi  NA NA NA NA NA NA ...
##  $ max_picth_dumbbell      : logi  NA NA NA NA NA NA ...
##  $ max_yaw_dumbbell        : logi  NA NA NA NA NA NA ...
##  $ min_roll_dumbbell       : logi  NA NA NA NA NA NA ...
##  $ min_pitch_dumbbell      : logi  NA NA NA NA NA NA ...
##  $ min_yaw_dumbbell        : logi  NA NA NA NA NA NA ...
##  $ amplitude_roll_dumbbell : logi  NA NA NA NA NA NA ...
##   [list output truncated]
```

```r
summary(d2) # the last var "classe" is outcome to be predicted.
```

```
##        X            user_name raw_timestamp_part_1 raw_timestamp_part_2
##  Min.   : 1.00   adelmo  :1   Min.   :1.32e+09     Min.   : 36553      
##  1st Qu.: 5.75   carlitos:3   1st Qu.:1.32e+09     1st Qu.:268655      
##  Median :10.50   charles :1   Median :1.32e+09     Median :530706      
##  Mean   :10.50   eurico  :4   Mean   :1.32e+09     Mean   :512167      
##  3rd Qu.:15.25   jeremy  :8   3rd Qu.:1.32e+09     3rd Qu.:787738      
##  Max.   :20.00   pedro   :3   Max.   :1.32e+09     Max.   :920315      
##                                                                        
##           cvtd_timestamp new_window   num_window    roll_belt     
##  30/11/2011 17:11:4      no:20      Min.   : 48   Min.   : -5.92  
##  05/12/2011 11:24:3                 1st Qu.:250   1st Qu.:  0.91  
##  30/11/2011 17:12:3                 Median :384   Median :  1.11  
##  05/12/2011 14:23:2                 Mean   :380   Mean   : 31.31  
##  28/11/2011 14:14:2                 3rd Qu.:467   3rd Qu.: 32.51  
##  02/12/2011 13:33:1                 Max.   :859   Max.   :129.00  
##  (Other)         :5                                               
##    pitch_belt        yaw_belt     total_accel_belt kurtosis_roll_belt
##  Min.   :-41.60   Min.   :-93.7   Min.   : 2.00    Mode:logical      
##  1st Qu.:  3.01   1st Qu.:-88.6   1st Qu.: 3.00    NA's:20           
##  Median :  4.66   Median :-87.8   Median : 4.00                      
##  Mean   :  5.82   Mean   :-59.3   Mean   : 7.55                      
##  3rd Qu.:  6.13   3rd Qu.:-63.5   3rd Qu.: 8.00                      
##  Max.   : 27.80   Max.   :162.0   Max.   :21.00                      
##                                                                      
##  kurtosis_picth_belt kurtosis_yaw_belt skewness_roll_belt
##  Mode:logical        Mode:logical      Mode:logical      
##  NA's:20             NA's:20           NA's:20           
##                                                          
##                                                          
##                                                          
##                                                          
##                                                          
##  skewness_roll_belt.1 skewness_yaw_belt max_roll_belt  max_picth_belt
##  Mode:logical         Mode:logical      Mode:logical   Mode:logical  
##  NA's:20              NA's:20           NA's:20        NA's:20       
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##  max_yaw_belt   min_roll_belt  min_pitch_belt min_yaw_belt  
##  Mode:logical   Mode:logical   Mode:logical   Mode:logical  
##  NA's:20        NA's:20        NA's:20        NA's:20       
##                                                             
##                                                             
##                                                             
##                                                             
##                                                             
##  amplitude_roll_belt amplitude_pitch_belt amplitude_yaw_belt
##  Mode:logical        Mode:logical         Mode:logical      
##  NA's:20             NA's:20              NA's:20           
##                                                             
##                                                             
##                                                             
##                                                             
##                                                             
##  var_total_accel_belt avg_roll_belt  stddev_roll_belt var_roll_belt 
##  Mode:logical         Mode:logical   Mode:logical     Mode:logical  
##  NA's:20              NA's:20        NA's:20          NA's:20       
##                                                                     
##                                                                     
##                                                                     
##                                                                     
##                                                                     
##  avg_pitch_belt stddev_pitch_belt var_pitch_belt avg_yaw_belt  
##  Mode:logical   Mode:logical      Mode:logical   Mode:logical  
##  NA's:20        NA's:20           NA's:20        NA's:20       
##                                                                
##                                                                
##                                                                
##                                                                
##                                                                
##  stddev_yaw_belt var_yaw_belt    gyros_belt_x     gyros_belt_y   
##  Mode:logical    Mode:logical   Min.   :-0.500   Min.   :-0.050  
##  NA's:20         NA's:20        1st Qu.:-0.070   1st Qu.:-0.005  
##                                 Median : 0.020   Median : 0.000  
##                                 Mean   :-0.045   Mean   : 0.010  
##                                 3rd Qu.: 0.070   3rd Qu.: 0.020  
##                                 Max.   : 0.240   Max.   : 0.110  
##                                                                  
##   gyros_belt_z     accel_belt_x     accel_belt_y    accel_belt_z   
##  Min.   :-0.480   Min.   :-48.00   Min.   :-16.0   Min.   :-187.0  
##  1st Qu.:-0.138   1st Qu.:-19.00   1st Qu.:  2.0   1st Qu.: -24.0  
##  Median :-0.025   Median :-13.00   Median :  4.5   Median :  27.0  
##  Mean   :-0.101   Mean   :-13.50   Mean   : 18.4   Mean   : -17.6  
##  3rd Qu.: 0.000   3rd Qu.: -8.75   3rd Qu.: 25.5   3rd Qu.:  38.2  
##  Max.   : 0.050   Max.   : 46.00   Max.   : 72.0   Max.   :  49.0  
##                                                                    
##  magnet_belt_x   magnet_belt_y magnet_belt_z     roll_arm     
##  Min.   :-13.0   Min.   :566   Min.   :-426   Min.   :-137.0  
##  1st Qu.:  5.5   1st Qu.:578   1st Qu.:-398   1st Qu.:   0.0  
##  Median : 33.5   Median :600   Median :-314   Median :   0.0  
##  Mean   : 35.1   Mean   :602   Mean   :-347   Mean   :  16.4  
##  3rd Qu.: 46.2   3rd Qu.:631   3rd Qu.:-305   3rd Qu.:  71.5  
##  Max.   :169.0   Max.   :638   Max.   :-291   Max.   : 152.0  
##                                                               
##    pitch_arm         yaw_arm       total_accel_arm var_accel_arm 
##  Min.   :-63.80   Min.   :-167.0   Min.   : 3.0    Mode:logical  
##  1st Qu.: -9.19   1st Qu.: -60.1   1st Qu.:20.2    NA's:20       
##  Median :  0.00   Median :   0.0   Median :29.5                  
##  Mean   : -3.95   Mean   :  -2.8   Mean   :26.4                  
##  3rd Qu.:  3.46   3rd Qu.:  25.5   3rd Qu.:33.2                  
##  Max.   : 55.00   Max.   : 178.0   Max.   :44.0                  
##                                                                  
##  avg_roll_arm   stddev_roll_arm var_roll_arm   avg_pitch_arm 
##  Mode:logical   Mode:logical    Mode:logical   Mode:logical  
##  NA's:20        NA's:20         NA's:20        NA's:20       
##                                                              
##                                                              
##                                                              
##                                                              
##                                                              
##  stddev_pitch_arm var_pitch_arm  avg_yaw_arm    stddev_yaw_arm
##  Mode:logical     Mode:logical   Mode:logical   Mode:logical  
##  NA's:20          NA's:20        NA's:20        NA's:20       
##                                                               
##                                                               
##                                                               
##                                                               
##                                                               
##  var_yaw_arm     gyros_arm_x      gyros_arm_y      gyros_arm_z    
##  Mode:logical   Min.   :-3.710   Min.   :-2.090   Min.   :-0.690  
##  NA's:20        1st Qu.:-0.645   1st Qu.:-0.635   1st Qu.:-0.180  
##                 Median : 0.020   Median :-0.040   Median :-0.025  
##                 Mean   : 0.077   Mean   :-0.160   Mean   : 0.120  
##                 3rd Qu.: 1.248   3rd Qu.: 0.217   3rd Qu.: 0.565  
##                 Max.   : 3.660   Max.   : 1.850   Max.   : 1.130  
##                                                                   
##   accel_arm_x      accel_arm_y     accel_arm_z      magnet_arm_x 
##  Min.   :-341.0   Min.   :-65.0   Min.   :-404.0   Min.   :-428  
##  1st Qu.:-277.0   1st Qu.: 52.2   1st Qu.:-128.5   1st Qu.:-374  
##  Median :-194.5   Median :112.0   Median : -83.5   Median :-265  
##  Mean   :-134.6   Mean   :103.1   Mean   : -87.8   Mean   : -39  
##  3rd Qu.:   5.5   3rd Qu.:168.2   3rd Qu.: -27.2   3rd Qu.: 250  
##  Max.   : 106.0   Max.   :245.0   Max.   :  93.0   Max.   : 750  
##                                                                  
##   magnet_arm_y   magnet_arm_z  kurtosis_roll_arm kurtosis_picth_arm
##  Min.   :-307   Min.   :-499   Mode:logical      Mode:logical      
##  1st Qu.: 205   1st Qu.: 403   NA's:20           NA's:20           
##  Median : 291   Median : 476                                       
##  Mean   : 239   Mean   : 370                                       
##  3rd Qu.: 359   3rd Qu.: 517                                       
##  Max.   : 474   Max.   : 633                                       
##                                                                    
##  kurtosis_yaw_arm skewness_roll_arm skewness_pitch_arm skewness_yaw_arm
##  Mode:logical     Mode:logical      Mode:logical       Mode:logical    
##  NA's:20          NA's:20           NA's:20            NA's:20         
##                                                                        
##                                                                        
##                                                                        
##                                                                        
##                                                                        
##  max_roll_arm   max_picth_arm  max_yaw_arm    min_roll_arm  
##  Mode:logical   Mode:logical   Mode:logical   Mode:logical  
##  NA's:20        NA's:20        NA's:20        NA's:20       
##                                                             
##                                                             
##                                                             
##                                                             
##                                                             
##  min_pitch_arm  min_yaw_arm    amplitude_roll_arm amplitude_pitch_arm
##  Mode:logical   Mode:logical   Mode:logical       Mode:logical       
##  NA's:20        NA's:20        NA's:20            NA's:20            
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##  amplitude_yaw_arm roll_dumbbell     pitch_dumbbell   yaw_dumbbell    
##  Mode:logical      Min.   :-111.12   Min.   :-55.0   Min.   :-103.32  
##  NA's:20           1st Qu.:   7.49   1st Qu.:-51.9   1st Qu.: -75.28  
##                    Median :  50.40   Median :-40.8   Median :  -8.29  
##                    Mean   :  33.76   Mean   :-19.5   Mean   :  -0.94  
##                    3rd Qu.:  58.13   3rd Qu.: 16.1   3rd Qu.:  55.83  
##                    Max.   : 123.98   Max.   : 96.9   Max.   : 132.23  
##                                                                       
##  kurtosis_roll_dumbbell kurtosis_picth_dumbbell kurtosis_yaw_dumbbell
##  Mode:logical           Mode:logical            Mode:logical         
##  NA's:20                NA's:20                 NA's:20              
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##  skewness_roll_dumbbell skewness_pitch_dumbbell skewness_yaw_dumbbell
##  Mode:logical           Mode:logical            Mode:logical         
##  NA's:20                NA's:20                 NA's:20              
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##                                                                      
##  max_roll_dumbbell max_picth_dumbbell max_yaw_dumbbell min_roll_dumbbell
##  Mode:logical      Mode:logical       Mode:logical     Mode:logical     
##  NA's:20           NA's:20            NA's:20          NA's:20          
##                                                                         
##                                                                         
##                                                                         
##                                                                         
##                                                                         
##  min_pitch_dumbbell min_yaw_dumbbell amplitude_roll_dumbbell
##  Mode:logical       Mode:logical     Mode:logical           
##  NA's:20            NA's:20          NA's:20                
##                                                             
##                                                             
##                                                             
##                                                             
##                                                             
##  amplitude_pitch_dumbbell amplitude_yaw_dumbbell total_accel_dumbbell
##  Mode:logical             Mode:logical           Min.   : 1.0        
##  NA's:20                  NA's:20                1st Qu.: 7.0        
##                                                  Median :15.5        
##                                                  Mean   :17.2        
##                                                  3rd Qu.:29.0        
##                                                  Max.   :31.0        
##                                                                      
##  var_accel_dumbbell avg_roll_dumbbell stddev_roll_dumbbell
##  Mode:logical       Mode:logical      Mode:logical        
##  NA's:20            NA's:20           NA's:20             
##                                                           
##                                                           
##                                                           
##                                                           
##                                                           
##  var_roll_dumbbell avg_pitch_dumbbell stddev_pitch_dumbbell
##  Mode:logical      Mode:logical       Mode:logical         
##  NA's:20           NA's:20            NA's:20              
##                                                            
##                                                            
##                                                            
##                                                            
##                                                            
##  var_pitch_dumbbell avg_yaw_dumbbell stddev_yaw_dumbbell var_yaw_dumbbell
##  Mode:logical       Mode:logical     Mode:logical        Mode:logical    
##  NA's:20            NA's:20          NA's:20             NA's:20         
##                                                                          
##                                                                          
##                                                                          
##                                                                          
##                                                                          
##  gyros_dumbbell_x gyros_dumbbell_y  gyros_dumbbell_z accel_dumbbell_x
##  Min.   :-1.030   Min.   :-1.1100   Min.   :-1.180   Min.   :-159.0  
##  1st Qu.: 0.160   1st Qu.:-0.2100   1st Qu.:-0.485   1st Qu.:-140.2  
##  Median : 0.360   Median : 0.0150   Median :-0.280   Median : -19.0  
##  Mean   : 0.269   Mean   : 0.0605   Mean   :-0.266   Mean   : -47.6  
##  3rd Qu.: 0.463   3rd Qu.: 0.1450   3rd Qu.:-0.165   3rd Qu.:  15.8  
##  Max.   : 1.060   Max.   : 1.9100   Max.   : 1.100   Max.   : 185.0  
##                                                                      
##  accel_dumbbell_y accel_dumbbell_z magnet_dumbbell_x magnet_dumbbell_y
##  Min.   :-30.00   Min.   :-221.0   Min.   :-576      Min.   :-558     
##  1st Qu.:  5.75   1st Qu.:-192.2   1st Qu.:-528      1st Qu.: 260     
##  Median : 71.50   Median :  -3.0   Median :-508      Median : 316     
##  Mean   : 70.55   Mean   : -60.0   Mean   :-304      Mean   : 189     
##  3rd Qu.:151.25   3rd Qu.:  76.5   3rd Qu.:-317      3rd Qu.: 348     
##  Max.   :166.00   Max.   : 100.0   Max.   : 523      Max.   : 403     
##                                                                       
##  magnet_dumbbell_z  roll_forearm    pitch_forearm     yaw_forearm     
##  Min.   :-164.0    Min.   :-176.0   Min.   :-63.50   Min.   :-168.00  
##  1st Qu.: -33.0    1st Qu.: -40.2   1st Qu.:-11.46   1st Qu.: -93.38  
##  Median :  49.5    Median :  94.2   Median :  8.83   Median : -19.25  
##  Mean   :  71.4    Mean   :  38.7   Mean   :  7.10   Mean   :   2.19  
##  3rd Qu.:  96.2    3rd Qu.: 143.2   3rd Qu.: 28.50   3rd Qu.: 104.50  
##  Max.   : 368.0    Max.   : 176.0   Max.   : 59.30   Max.   : 159.00  
##                                                                       
##  kurtosis_roll_forearm kurtosis_picth_forearm kurtosis_yaw_forearm
##  Mode:logical          Mode:logical           Mode:logical        
##  NA's:20               NA's:20                NA's:20             
##                                                                   
##                                                                   
##                                                                   
##                                                                   
##                                                                   
##  skewness_roll_forearm skewness_pitch_forearm skewness_yaw_forearm
##  Mode:logical          Mode:logical           Mode:logical        
##  NA's:20               NA's:20                NA's:20             
##                                                                   
##                                                                   
##                                                                   
##                                                                   
##                                                                   
##  max_roll_forearm max_picth_forearm max_yaw_forearm min_roll_forearm
##  Mode:logical     Mode:logical      Mode:logical    Mode:logical    
##  NA's:20          NA's:20           NA's:20         NA's:20         
##                                                                     
##                                                                     
##                                                                     
##                                                                     
##                                                                     
##  min_pitch_forearm min_yaw_forearm amplitude_roll_forearm
##  Mode:logical      Mode:logical    Mode:logical          
##  NA's:20           NA's:20         NA's:20               
##                                                          
##                                                          
##                                                          
##                                                          
##                                                          
##  amplitude_pitch_forearm amplitude_yaw_forearm total_accel_forearm
##  Mode:logical            Mode:logical          Min.   :21.0       
##  NA's:20                 NA's:20               1st Qu.:24.0       
##                                                Median :32.5       
##                                                Mean   :32.0       
##                                                3rd Qu.:36.8       
##                                                Max.   :47.0       
##                                                                   
##  var_accel_forearm avg_roll_forearm stddev_roll_forearm var_roll_forearm
##  Mode:logical      Mode:logical     Mode:logical        Mode:logical    
##  NA's:20           NA's:20          NA's:20             NA's:20         
##                                                                         
##                                                                         
##                                                                         
##                                                                         
##                                                                         
##  avg_pitch_forearm stddev_pitch_forearm var_pitch_forearm avg_yaw_forearm
##  Mode:logical      Mode:logical         Mode:logical      Mode:logical   
##  NA's:20           NA's:20              NA's:20           NA's:20        
##                                                                          
##                                                                          
##                                                                          
##                                                                          
##                                                                          
##  stddev_yaw_forearm var_yaw_forearm gyros_forearm_x  gyros_forearm_y 
##  Mode:logical       Mode:logical    Min.   :-1.060   Min.   :-5.970  
##  NA's:20            NA's:20         1st Qu.:-0.585   1st Qu.:-1.288  
##                                     Median : 0.020   Median : 0.035  
##                                     Mean   :-0.020   Mean   :-0.042  
##                                     3rd Qu.: 0.292   3rd Qu.: 2.047  
##                                     Max.   : 1.380   Max.   : 4.260  
##                                                                      
##  gyros_forearm_z   accel_forearm_x  accel_forearm_y  accel_forearm_z 
##  Min.   :-1.2600   Min.   :-212.0   Min.   :-331.0   Min.   :-282.0  
##  1st Qu.:-0.0975   1st Qu.:-114.8   1st Qu.:   8.5   1st Qu.:-199.0  
##  Median : 0.2300   Median :  86.0   Median : 138.0   Median :-148.5  
##  Mean   : 0.2610   Mean   :  38.8   Mean   : 125.3   Mean   : -93.7  
##  3rd Qu.: 0.7625   3rd Qu.: 166.2   3rd Qu.: 268.0   3rd Qu.: -31.0  
##  Max.   : 1.8000   Max.   : 232.0   Max.   : 406.0   Max.   : 179.0  
##                                                                      
##  magnet_forearm_x magnet_forearm_y magnet_forearm_z   problem_id   
##  Min.   :-714.0   Min.   :-787     Min.   :-32      Min.   : 1.00  
##  1st Qu.:-427.2   1st Qu.:-329     1st Qu.:275      1st Qu.: 5.75  
##  Median :-189.5   Median : 487     Median :492      Median :10.50  
##  Mean   :-159.2   Mean   : 192     Mean   :460      Mean   :10.50  
##  3rd Qu.:  41.5   3rd Qu.: 721     3rd Qu.:662      3rd Qu.:15.25  
##  Max.   : 532.0   Max.   : 800     Max.   :884      Max.   :20.00  
## 
```

### Cleaning & Exploring Data  
I noticed that there are many variables that contain a large number of NAs, several variables have value "DIV/0!". To review the data in details, I used Hmisc package and options() function.  

```r
# NA details
library(Hmisc) 
```

```
## Loading required package: grid
## Loading required package: lattice
## Loading required package: survival
## Loading required package: splines
## Loading required package: Formula
## 
## Attaching package: 'Hmisc'
## 
## The following objects are masked from 'package:base':
## 
##     format.pval, round.POSIXt, trunc.POSIXt, units
```

```r
options(na.action="na.keep", na.detail.response=TRUE)
# review the dataframe "d".
a<-describe(d)
a[1:20]
```

```
## d 
## 
##  20  Variables      19622  Observations
## ---------------------------------------------------------------------------
## X 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##   19622       0   19622    9812   982.1  1963.1  4906.2  9811.5 14716.8 
##     .90     .95 
## 17659.9 18641.0 
## 
## lowest :     1     2     3     4     5
## highest: 19618 19619 19620 19621 19622 
## ---------------------------------------------------------------------------
## user_name 
##       n missing  unique 
##   19622       0       6 
## 
##           adelmo carlitos charles eurico jeremy pedro
## Frequency   3892     3112    3536   3070   3402  2610
## %             20       16      18     16     17    13
## ---------------------------------------------------------------------------
## raw_timestamp_part_1 
##         n   missing    unique      Mean       .05       .10       .25 
##     19622         0       837 1.323e+09 1.322e+09 1.322e+09 1.323e+09 
##       .50       .75       .90       .95 
## 1.323e+09 1.323e+09 1.323e+09 1.323e+09 
## 
## lowest : 1322489605 1322489606 1322489607 1322489608 1322489609
## highest: 1323095077 1323095078 1323095079 1323095080 1323095081 
## ---------------------------------------------------------------------------
## raw_timestamp_part_2 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##   19622       0   16783  500656   48389  100343  252912  496380  751891 
##     .90     .95 
##  900367  950649 
## 
## lowest :    294    301    307    309    312
## highest: 998716 998741 998749 998750 998801 
## ---------------------------------------------------------------------------
## cvtd_timestamp 
##       n missing  unique 
##   19622       0      20 
## 
## lowest : 02/12/2011 13:32 02/12/2011 13:33 02/12/2011 13:34 02/12/2011 13:35 02/12/2011 14:56
## highest: 28/11/2011 14:14 28/11/2011 14:15 30/11/2011 17:10 30/11/2011 17:11 30/11/2011 17:12 
## ---------------------------------------------------------------------------
## new_window 
##       n missing  unique 
##   19622       0       2 
## 
## no (19216, 98%), yes (406, 2%) 
## ---------------------------------------------------------------------------
## num_window 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##   19622       0     858   430.6      44      88     222     424     644 
##     .90     .95 
##     780     821 
## 
## lowest :   1   2   3   4   5, highest: 860 861 862 863 864 
## ---------------------------------------------------------------------------
## roll_belt 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##   19622       0    1330   64.41   -0.20    0.53    1.10  113.00  123.00 
##     .90     .95 
##  129.00  139.00 
## 
## lowest : -28.9 -28.8 -28.6 -28.4 -28.3
## highest: 158.0 159.0 160.0 161.0 162.0 
## ---------------------------------------------------------------------------
## pitch_belt 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##   19622       0    1840  0.3053  -43.60  -42.10    1.76    5.28   14.90 
##     .90     .95 
##   25.40   26.20 
## 
## lowest : -55.8 -54.9 -54.7 -54.4 -53.9
## highest:  59.9  60.0  60.1  60.2  60.3 
## ---------------------------------------------------------------------------
## yaw_belt 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##   19622       0    1957  -11.21   -93.5   -92.9   -88.3   -13.0    12.9 
##     .90     .95 
##   165.0   168.0 
## 
## lowest : -180 -179 -178 -177 -176, highest:  175  176  177  178  179 
## ---------------------------------------------------------------------------
## total_accel_belt 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##   19622       0      29   11.31       2       3       3      17      18 
##     .90     .95 
##      20      21 
## 
## lowest :  0  1  2  3  4, highest: 25 26 27 28 29 
## ---------------------------------------------------------------------------
## kurtosis_roll_belt 
##       n missing  unique 
##   19622       0     397 
## 
## lowest :           -0.016850 -0.021024 -0.025513 -0.033935
## highest: 5.587755  5.681869  6.545935  7.004355  7.515290  
## ---------------------------------------------------------------------------
## kurtosis_picth_belt 
##       n missing  unique 
##   19622       0     317 
## 
## lowest :           -0.021887 -0.060755 -0.099173 -0.108371
## highest: 8.953960  9.042959  9.296951  9.804491  9.896970  
## ---------------------------------------------------------------------------
## kurtosis_yaw_belt 
##       n missing  unique 
##   19622       0       2 
## 
##  (19216, 98%), #DIV/0! (406, 2%) 
## ---------------------------------------------------------------------------
## skewness_roll_belt 
##       n missing  unique 
##   19622       0     395 
## 
## lowest :           -0.003095 -0.010002 -0.014020 -0.015465
## highest: 2.058296  2.097857  2.674649  2.713152  3.595369  
## ---------------------------------------------------------------------------
## skewness_roll_belt.1 
##       n missing  unique 
##   19622       0     338 
## 
## lowest :           -0.005928 -0.005960 -0.008391 -0.017954
## highest: 6.164414  6.708204  6.782330  6.855655  7.348469  
## ---------------------------------------------------------------------------
## skewness_yaw_belt 
##       n missing  unique 
##   19622       0       2 
## 
##  (19216, 98%), #DIV/0! (406, 2%) 
## ---------------------------------------------------------------------------
## max_roll_belt 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##     406   19216     195  -6.667  -93.07  -92.30  -88.00   -5.10   18.50 
##     .90     .95 
##  165.50  169.00 
## 
## lowest : -94.3 -94.1 -93.9 -93.8 -93.6
## highest: 172.0 173.0 174.0 177.0 180.0 
## ---------------------------------------------------------------------------
## max_picth_belt 
##       n missing  unique    Mean     .05     .10     .25     .50     .75 
##     406   19216      22   12.92       3       3       5      18      19 
##     .90     .95 
##      21      26 
## 
## lowest :  3  4  5  6  7, highest: 25 26 27 28 30 
## ---------------------------------------------------------------------------
## max_yaw_belt 
##       n missing  unique 
##   19622       0      68 
## 
## lowest :      -0.1 -0.2 -0.3 -0.4, highest: 5.6  5.7  6.5  7.0  7.5  
## ---------------------------------------------------------------------------
```

```r
# can review more contents of a.
```

To remove the variables with a large number of NAs, I first created a function to identify the indices for the variables with NAs. 
The variables containing NAs, "#DIV/0!" and empty cells should be removed. In addition, the first 6 column variables which are not dirrectly corresponding to the exercise manner would also be removed. Total 54 of variables were remained in the data frame.    

```r
d_na.rm<-d
d_na.rm<-d_na.rm[,-c(1:6, 12:16, 17:19, 21, 22, 24, 25, 26, 27, 28:30, 31:36, 50:59, 
		69:74, 75:80, 81:83, 87, 90, 92,93, 94, 96, 97, 99, 100, 101, 103:112, 
		125, 126, 128, 129, 131, 132, 133, 	134, 135, 136, 137, 138, 139,141:150, 89, 127, 130, 20, 23, 88, 91, 95, 98)]   
dim(d_na.rm) 
```

```
## [1] 19622    54
```


###Splitting the Data  

```r
library(caret)
```

```
## Loading required package: ggplot2
## 
## Attaching package: 'caret'
## 
## The following object is masked from 'package:survival':
## 
##     cluster
```

```r
set.seed(33833)
inTrain<-createDataPartition(d_na.rm$classe, p=3/4, list=FALSE) 
training<-d_na.rm[inTrain,]
testing<-d_na.rm[-inTrain,]
```

###Plotting Predictors    
I used 'car' package to make scatter plot on outcome variable "classe" with multiple pairs of predictors. Here shows an example, the plot shows relationship of "classe" with a few predictors on "belt" which suggested some potentials for good predictors.    

```r
library(car)
scatterplotMatrix(~classe+roll_belt+pitch_belt+yaw_belt+total_accel_belt, span=0.7, data=training) 
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 

```r
dev.copy(png, file="belt.scatterplot.pairs_1.png")
```

```
## png 
##   3
```

```r
dev.off()
```

```
## pdf 
##   2
```

###PreProcess using the caret package  
After cleaning the data, there are 54 variables remained. However, some of those variables may be correlated. I used principle componenent analysis to preProcess the data. The results showed that 26 componenets can capture 95% of the variance.  

```r
preProc<-preProcess(training[,-54], method="pca") #26 components to capture 95% of the variance.
preProc
```

```
## 
## Call:
## preProcess.default(x = training[, -54], method = "pca")
## 
## Created from 14718 samples and 53 variables
## Pre-processing: principal component signal extraction, scaled, centered 
## 
## PCA needed 26 components to capture 95 percent of the variance
```

```r
trainPC<-predict(preProc, training[,-54]) 
```

###To train the model using the pre-processed training data.  
The varImp() function shows the most important predictors in the fitted model.    
I chose the random-forest approach which uses bootstrapping re-sampling, and at each split, bootstrpping variables to grow multiple trees to vote, therefore increases the accuracy.   

```r
set.seed(125) 
modelFit<-train(training$classe~., method="rf", data=trainPC)
```

```
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
```

```
## Loading required package: randomForest
## randomForest 4.6-10
## Type rfNews() to see new features/changes/bug fixes.
## 
## Attaching package: 'randomForest'
## 
## The following object is masked from 'package:Hmisc':
## 
##     combine
```

```r
varImp(modelFit)
```

```
## rf variable importance
## 
##   only 20 most important variables shown (out of 26)
## 
##      Overall
## PC8    100.0
## PC15    85.4
## PC1     81.5
## PC13    72.0
## PC12    71.1
## PC3     70.7
## PC5     65.6
## PC9     62.3
## PC2     53.3
## PC6     51.2
## PC16    41.0
## PC10    37.1
## PC18    35.3
## PC7     35.0
## PC4     34.4
## PC17    34.1
## PC14    33.2
## PC21    28.2
## PC23    27.8
## PC22    26.8
```

###Cross validation.
For cross-validation, pre-processing the splitted testing data using the same parameters and method used on the training data. Then make a prediction on the pre-processed testing data and compute the expected out of sample errors. The result shows that the accuracy is 98.2% which is high.

```r
testPC<-predict(preProc, testing[,-54]) 
confusionMatrix(testing$classe, predict(modelFit, testPC)) 
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 1386    6    2    1    0
##          B   10  930    8    0    1
##          C    3   12  834    6    0
##          D    0    0   29  775    0
##          E    0    2    5    3  891
## 
## Overall Statistics
##                                         
##                Accuracy : 0.982         
##                  95% CI : (0.978, 0.986)
##     No Information Rate : 0.285         
##     P-Value [Acc > NIR] : <2e-16        
##                                         
##                   Kappa : 0.977         
##  Mcnemar's Test P-Value : NA            
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity             0.991    0.979    0.950    0.987    0.999
## Specificity             0.997    0.995    0.995    0.993    0.998
## Pos Pred Value          0.994    0.980    0.975    0.964    0.989
## Neg Pred Value          0.996    0.995    0.989    0.998    1.000
## Prevalence              0.285    0.194    0.179    0.160    0.182
## Detection Rate          0.283    0.190    0.170    0.158    0.182
## Detection Prevalence    0.284    0.194    0.174    0.164    0.184
## Balanced Accuracy       0.994    0.987    0.972    0.990    0.998
```

###Fit the model without PCA pre-process.
I also fit the model using the random-forest approach on the training data without PCA preprocess to compare the two approached with or without PCA.  
The result shows that without PCA preprocess, the accuracy is 99.7%, only slightly increases. This suggested that PCA approach can capture the majority of the variance and is effective in this study.  

```r
modelFit2<-train(training$classe~., method="rf", ntree=20, data=training)
```

```
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
## Warning: argument is not numeric or logical: returning NA
```

```r
varImp(modelFit2)
```

```
## rf variable importance
## 
##   only 20 most important variables shown (out of 53)
## 
##                      Overall
## num_window            100.00
## roll_belt              66.89
## pitch_forearm          41.10
## yaw_belt               35.09
## magnet_dumbbell_z      33.72
## roll_forearm           31.83
## magnet_dumbbell_y      31.50
## pitch_belt             27.22
## roll_dumbbell          14.57
## accel_forearm_x        13.13
## magnet_forearm_z       11.04
## magnet_belt_y          10.93
## accel_dumbbell_y       10.90
## magnet_dumbbell_x       9.44
## accel_dumbbell_z        9.24
## total_accel_dumbbell    9.22
## accel_belt_z            8.54
## magnet_belt_x           8.35
## magnet_belt_z           8.02
## accel_dumbbell_x        6.41
```

```r
confusionMatrix(testing$classe, predict(modelFit2, testing)) 
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 1394    1    0    0    0
##          B    4  945    0    0    0
##          C    0    6  849    0    0
##          D    0    0    1  803    0
##          E    0    0    1    2  898
## 
## Overall Statistics
##                                         
##                Accuracy : 0.997         
##                  95% CI : (0.995, 0.998)
##     No Information Rate : 0.285         
##     P-Value [Acc > NIR] : <2e-16        
##                                         
##                   Kappa : 0.996         
##  Mcnemar's Test P-Value : NA            
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity             0.997    0.993    0.998    0.998    1.000
## Specificity             1.000    0.999    0.999    1.000    0.999
## Pos Pred Value          0.999    0.996    0.993    0.999    0.997
## Neg Pred Value          0.999    0.998    1.000    1.000    1.000
## Prevalence              0.285    0.194    0.174    0.164    0.183
## Detection Rate          0.284    0.193    0.173    0.164    0.183
## Detection Prevalence    0.284    0.194    0.174    0.164    0.184
## Balanced Accuracy       0.998    0.996    0.998    0.999    1.000
```

```r
predict(modelFit2, d2_na.rm)
```

```
## Error: object 'd2_na.rm' not found
```

###To predict newdata, the testing data (named "d2") from the assignment.  
To clean the new testing data, I changed the variable name to exactly the same as the training data, which only replace "problem_id" with "classe".  
And change the type of variable "classe" into factor variable with 5 levels. Furthermore, remove the variables in the same way as in the training data.  
Make a prediction using the two trained models used in above,"modelFit" and "modelFit2" which agrees with each other.  


```r
names(d2[,-160])==names(d[,-160]) # all TRUE
```

```
##   [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
##  [30] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
##  [59] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
##  [88] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
## [117] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
## [146] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
```

```r
names(d2)=names(d) 

d2_na.rm<-d2
d2_na.rm<-d2_na.rm[,-c(1:6, 12:16, 17:19, 21, 22, 24, 25, 26, 27, 28:30, 31:36, 50:59, 
		69:74, 75:80, 81:83, 87, 90, 92,93, 94, 96, 97, 99, 100, 101, 103:112, 
		125, 126, 128, 129, 131, 132, 133, 	134, 135, 136, 137, 138, 139,141:150, 89, 127, 130, 20, 23, 88, 91, 95, 98)]   
d2_na.rm$classe<-rep(c("A","B","C","D","E"),4)
d2_na.rm$classe<-as.factor(d2_na.rm$classe)

test2PC<-predict(preProc, d2_na.rm[,-54])	
predict(modelFit, test2PC)
```

```
##  [1] B A B A A E D B A A B C B A E E A B B B
## Levels: A B C D E
```

```r
predict(modelFit2, d2_na.rm)
```

```
##  [1] B A B A A E D B A A B C B A E E A B B B
## Levels: A B C D E
```





