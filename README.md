# Krisuvik to Norway

## Description of Situation

The icelandic volcano Krìsuvik is currently erupting, but so far not emitting volcanic ash. 
Depending on new fissures in the volcano, ash emissions can occur at any time. Therefore, MET Norway
is running the eemep volcanic ash transport model 4 times a day simulating an ash emission starting at
00:00, 06:00, 12:00 and 18:00 (all times UTC). The models are started as followed

```
# 00 meteo, 06 eruption
30 8 * * * ERUPT=06:00 add_volcanos.sh
# 06 meteo, 12 eruption
30 14 * * * ERUPT=12:00 add_volcanos.sh
# 12 meteo, 18 eruption
30 20 * * * ERUPT=18:00 add_volcanos.sh
# 18 meteo, 00 eruption
30 2 * * * ERUPT=00:00 add_volcanos.sh
```

The jobs are queued after this timestep and usually results arrive between 20 min and 3 hours after
the start. Delays appear, both for technical reasons, but also due to other volcanos running on higher priority.

Results are added to the directory at https://thredds.met.no/thredds/catalog/metusers/heikok/ash/krisuvik/catalog.html
The important files are  `eemep_hourInst_*.nc` where `*` is a timestamp when the model actually started.

## Task

Notify duty-meteorologists as soon as new results are available. The notification should included a message about
when and where Norwegian land is hit by an ash-column exceeding 0.2g/m2 during the eemep-run.

For simplicity, notifications should be initially implemented as configurable email.

## Constraints

The code will be deployed on an open-stack cloud computer using ubuntu 20.04. 
Deployment instructions need to be simple and clear.

## Further information

  * Icelandic volcanos: https://icelandicvolcanos.is/?volcano=KRY
  * Reports from recent exercises: https://volcanicashtest.met.no/
  * Job-control code of the eemep model: https://github.com/metno/snap/tree/master/utils/SnapPy
