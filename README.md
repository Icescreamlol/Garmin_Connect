# Garmin_Connect
Garmin Connect Custom Component for Home Assistant

<img src="https://i.imgur.com/8Jp7hci.jpg" alt="Lovelace" width="300"/>

# Configuration

To be added to the configuration.yaml:
```
sensor: 
  - platform: garmin_connect
    username: XXXXXXXXXXXXXXXX 
    password: YYYYYYYYYYYYYYYY
```    

This will add a sensor called garmin_steps with additional attributes. The available attributes can be found at the end of the readme.
To dispay the attributes as a sensor, sensor templates must be made.

# Example:
```
sensor: 
  - platform: garmin_connect
    username: eddy@merckx.be
    password: iplaybilliards
    
  - platform: template
    sensors:
      garmin_total_kcal:
        value_template: "{{ state_attr('sensor.garmin_steps', 'totalKilocalories') }}"
        unit_of_measurement: 'kcal'

      garmin_restingheartrate:
        value_template: "{{ state_attr('sensor.garmin_steps', 'restingHeartRate') }}"  
        unit_of_measurement:  'bpm'

      garmin_maxheartrate:
        value_template: "{{ state_attr('sensor.garmin_steps', 'maxAvgHeartRate') }}"  
        unit_of_measurement:  'bpm'
        
      garmin_floors:
        value_template: "{{ state_attr('sensor.garmin_steps', 'floorsAscended') }}"  
        unit_of_measurement:  ''
        
      garmin_stress:
        value_template: "{{ state_attr('sensor.garmin_steps', 'averageStressLevel') }}"  
        unit_of_measurement:  ''
```

Lovelace:
```
- icon: mdi:triangle
    cards:
      - id:
        type: vertical-stack
        cards:
        - entities:
          - name: Steps today
            icon: mdi:shoe-print
            entity: sensor.garmin_steps
          - name: Floors
            icon: mdi:stairs
            entity: sensor.garmin_floors
          - name: Calorieën
            icon: mdi:fire
            entity: sensor.garmin_total_kcal
          type: glance
        - entities:
          - name: Stress
            icon: mdi:human-handsup
            entity: sensor.garmin_stress
          - name: Resting HR
            icon: mdi:heart
            entity: sensor.garmin_restingheartrate
          - name: Max HR
            icon: mdi:heart
            entity: sensor.garmin_maxheartrate
          type: glance
```


The following attributes are available:
```
userProfileId
totalKilocalories
activeKilocalories
bmrKilocalories
wellnessKilocalories
burnedKilocalories
consumedKilocalories
remainingKilocalories
totalSteps
netCalorieGoal
totalDistanceMeters
wellnessDistanceMeters
wellnessActiveKilocalories
netRemainingKilocalories
userDailySummaryId
calendarDate
rule
uuid
dailyStepGoal
wellnessStartTimeGmt
wellnessStartTimeLocal
wellnessEndTimeGmt
wellnessEndTimeLocal
durationInMilliseconds
wellnessDescription
highlyActiveSeconds
activeSeconds
sedentarySeconds
sleepingSeconds
includesWellnessData
includesActivityData
includesCalorieConsumedData
privacyProtected
moderateIntensityMinutes
vigorousIntensityMinutes
floorsAscendedInMeters
floorsDescendedInMeters
floorsAscended
floorsDescended
intensityMinutesGoal
userFloorsAscendedGoal
minHeartRate
maxHeartRate
restingHeartRate
lastSevenDaysAvgRestingHeartRate
source
averageStressLevel
maxStressLevel
stressDuration
restStressDuration
activityStressDuration
uncategorizedStressDuration
totalStressDuration
lowStressDuration
mediumStressDuration
highStressDuration
stressPercentage
restStressPercentage
activityStressPercentage
uncategorizedStressPercentage
lowStressPercentage
mediumStressPercentage
highStressPercentage
stressQualifier
measurableAwakeDuration
measurableAsleepDuration
lastSyncTimestampGMT
minAvgHeartRate
maxAvgHeartRate
bodyBatteryChargedValue
bodyBatteryDrainedValue
bodyBatteryHighestValue
bodyBatteryLowestValue
bodyBatteryMostRecentValue
abnormalHeartRateAlertsCount
averageSpo2
lowestSpo2
latestSpo2
latestSpo2ReadingTimeGmt
latestSpo2ReadingTimeLocal
averageMonitoringEnvironmentAltitude
```

Based on the work of Benjamin Blau - https://github.com/benniblau/GarminConnectActivityExport
