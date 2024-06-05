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
```
<br />

```
## Search with earliest and latest values constraining results to previous quarter using relative time modifiers
index=_internal earliest=-1qtr@qtr latest=@qtr
```


```
## search which calculates difference in seconds between two time-based fields and displays duration in readable time format HH:MM:SS.
| makeresults count=5000 
| streamstats count 
| eval latestTime = _time
| eval earliestTime = latestTime - (random() % 86400 * 2) + 1
| eval duration = tostring(latestTime - earliestTime,"duration")
| eval earliestTime = strftime(earliestTime,"%Y-%m-%d %H:%M:%S"), latestTime = strftime(latestTime,"%Y-%m-%d %H:%M:%S")
```

