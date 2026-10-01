# Thermostat Control with WHF integration

-sensor.indoor_temp_avg = downstairs average temp
-sensor.entry_temp_avg = upstairs average temp
-deadband = 5
-If tgap <= deadband, force fan_only
-If tgap > deadband, choose cool or heat based on upstairs temp vs XYE set point
-If upstairs temp exactly equals the set point, do nothing

# Reactive and preemptive lockout 
if WHF is actually on OR WHF conditions are favorable:
    set AC = off
else:
    run normal heat / cool / fan only logic

WHF favorable =
  outside temperature is at least 4°F cooler than upstairs/downstairs max
  AND outside temperature is below XYE set point
  AND indoor temperature is above XYE set point

WHF is considered favorable when:
warmest indoor temp > XYE set point + 1°F
outdoor temp < XYE set point
outdoor temp is at least 4°F cooler than the warmest indoor temp
Example:
Upstairs: 78°F
Downstairs: 73°F
XYE set point: 74°F
Outside: 68°F
Result:
WHF favorable = true

Add eventually:
AND outdoor AQI is acceptable
AND outdoor humidity is not excessive
AND at least one window is open
AND it is not raining heavily


