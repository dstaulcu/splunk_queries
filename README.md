# Splunk Queries
This is a compilation of Splunk queries that I've collected and used over time.  I'll add to this list as I find more.

```
## Calendar Quarter
| makeresults count=5000 
| streamstats count 
| eval _time=_time-(count*86400)
| eval calendar_quarter = "CY" . strftime(_time,"%Y") . "Q" . case(tonumber(strftime(_time,"%m"))<=3,"1",tonumber(strftime(_time,"%m"))<=6,"2",tonumber(strftime(_time,"%m"))<=9,"3",tonumber(strftime(_time,"%m"))<=12,"4")
```
<br />

```
## Search with earliest value specified as string
index=_internal earliest="01/01/2024:00:00:00"
| head 1
```
<br />

