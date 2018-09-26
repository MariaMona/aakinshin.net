---
layout: post
title: "MSBuild task solution load time for ReSharperHost"
date: '2018-09-26'
lang: en
type: note
tags:
- Rider
- perf
output: md_document
---

<!--more-->

## Setup

**Hardware/Software:**
Mac mini, Intel Core i7-3615QM CPU 2.30GHz (Ivy Bridge).
Windows 10.0.15063.1155, macOS High Sierra 10.13.4, ubuntu 16.04.

Experiment: run `pwc.cmd`, open `ReSharperHost.Generated.sln` on warmed caches (238 projects)

Configurations:


|MSBuild              | SourceRevision|HostRider    |
|:--------------------|--------------:|:------------|
|15.8.20180925.124351 |        5716848|2018.2781.71 |
|15.1.20180831.144626 |        5716848|2018.2781.71 |

## Plot

<div class="mx-auto"><img class="mx-auto d-block" width="600" src="/img/notes/msbuild-load-resharperhost/plot-1.png" /></div>

## Mean Summary


|OS      |MSBuild              | MeanTotal|
|:-------|:--------------------|---------:|
|linux   |15.1.20180831.144626 |  17.00467|
|linux   |15.8.20180925.124351 |  38.03000|
|mac     |15.1.20180831.144626 |  28.97400|
|mac     |15.8.20180925.124351 |  39.23750|
|windows |15.1.20180831.144626 |  11.40067|
|windows |15.8.20180925.124351 |  17.15000|

## Raw data


|MSBuild              | SourceRevision|HostRider    |OS      | Iteration| Total| Binding| PreEvaluation| BuildEvaluation|
|:--------------------|--------------:|:------------|:-------|---------:|-----:|-------:|-------------:|---------------:|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         0| 30.91|    3.37|         17.56|            0.70|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         1| 34.71|    3.46|         18.42|            1.03|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         2| 30.48|    3.03|         16.61|            0.82|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         3| 31.55|    3.25|         17.98|            0.67|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         4| 34.38|    3.25|         20.10|            0.69|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         5| 51.42|    5.24|         24.80|            1.05|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         6| 48.14|    5.09|         23.33|            0.92|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         7| 37.63|    4.14|         21.20|            0.71|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         8| 31.18|    2.92|         15.82|            0.62|
|15.8.20180925.124351 |        5716848|2018.2781.71 |linux   |         9| 49.90|    4.61|         28.20|            1.09|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         0| 35.09|    2.75|         23.45|            0.52|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         1| 40.25|    2.85|         27.95|            0.63|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         2| 40.20|    2.70|         28.34|            0.58|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         3| 42.01|    2.80|         28.78|            0.56|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         4| 37.90|    2.66|         25.69|            0.52|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         5| 38.39|    2.71|         25.45|            0.52|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         6| 40.50|    2.75|         28.87|            0.56|
|15.8.20180925.124351 |        5716848|2018.2781.71 |mac     |         7| 39.56|    2.60|         27.43|            0.55|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         0| 32.69|    2.37|         30.67|            0.68|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         1| 26.29|    2.18|         24.48|            0.65|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         2| 29.25|    2.42|         27.52|            0.67|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         3| 29.11|    2.32|         27.23|            0.73|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         4| 28.78|    2.32|         26.97|            0.65|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         5| 29.33|    2.25|         27.32|            0.69|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         6| 30.13|    2.36|         28.39|            0.65|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         7| 29.65|    2.22|         27.80|            0.72|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         8| 29.18|    2.33|         27.48|            0.63|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |         9| 29.50|    2.26|         27.22|            0.66|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |        10| 27.11|    2.17|         25.47|            0.66|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |        11| 29.04|    2.34|         27.28|            0.75|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |        12| 29.81|    2.26|         27.95|            0.67|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |        13| 28.37|    2.31|         26.49|            0.71|
|15.1.20180831.144626 |        5716848|2018.2781.71 |mac     |        14| 26.37|    2.25|         24.75|            0.62|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         0| 15.05|    2.85|          8.70|            0.54|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         1| 18.73|    3.82|         10.77|            0.62|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         2| 18.42|    3.82|         10.70|            0.58|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         3| 15.93|    2.57|          9.56|            0.52|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         4| 19.56|    3.92|          9.89|            0.64|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         5| 19.12|    3.31|         10.86|            0.55|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         6| 18.19|    3.44|         10.80|            0.57|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         7| 14.20|    2.99|          7.85|            0.50|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         8| 14.47|    2.78|          8.26|            0.49|
|15.8.20180925.124351 |        5716848|2018.2781.71 |windows |         9| 17.83|    3.58|         10.98|            0.84|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         0| 15.89|    1.96|         14.63|            0.69|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         1| 16.31|    2.08|         14.93|            0.60|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         2| 15.73|    1.92|         14.57|            0.61|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         3| 16.18|    1.98|         14.85|            0.62|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         4| 16.09|    2.07|         14.86|            0.58|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         5| 24.46|    2.95|         22.37|            0.92|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         6| 21.70|    2.37|         19.88|            0.77|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         7| 15.60|    2.11|         14.35|            0.54|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         8| 15.84|    1.88|         14.61|            0.66|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |         9| 16.16|    1.94|         14.88|            0.59|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |        10| 16.37|    2.02|         14.94|            0.59|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |        11| 16.11|    2.01|         14.76|            0.59|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |        12| 16.45|    2.01|         14.99|            0.58|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |        13| 16.03|    2.07|         14.65|            0.61|
|15.1.20180831.144626 |        5716848|2018.2781.71 |linux   |        14| 16.15|    1.99|         14.84|            0.57|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         0|  7.72|    1.86|          6.52|            0.46|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         1| 12.34|    2.69|         10.73|            0.75|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         2| 12.06|    1.83|          9.94|            0.77|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         3| 10.62|    2.35|          9.11|            0.66|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         4| 13.23|    2.28|         11.43|            0.63|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         5|  9.41|    2.10|          8.09|            0.52|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         6| 10.33|    2.30|          8.71|            0.52|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         7| 12.26|    2.42|         10.65|            0.53|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         8| 12.29|    2.13|         10.62|            0.56|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |         9| 13.50|    2.51|         11.36|            0.65|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |        10| 12.80|    2.71|         10.84|            0.75|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |        11| 10.33|    2.23|          8.63|            0.54|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |        12|  9.22|    2.00|          7.75|            0.60|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |        13| 12.66|    2.59|         10.75|            0.70|
|15.1.20180831.144626 |        5716848|2018.2781.71 |windows |        14| 12.24|    2.51|         10.40|            0.51|