# splunk_queries


| makeresults count=5000  ``` make some number of records ```
| streamstats count ``` create a field for each record effectively having record number ```
| eval _time=_time-(count*86400) ``` alter the time associated with each record to be offset by record number number of days ```
| eval quarter = "CY" . strftime(_time,"%Y") . "Q" . case(tonumber(strftime(_time,"%m"))<=3,"1",tonumber(strftime(_time,"%m"))<=6,"2",tonumber(strftime(_time,"%m"))<=9,"3",tonumber(strftime(_time,"%m"))<=12,"4") ``` create a field, derived from time, representing name of quarter ```
