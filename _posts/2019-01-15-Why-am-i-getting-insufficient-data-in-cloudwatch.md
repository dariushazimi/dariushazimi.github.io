# Why am I getting insufficient_data alarms in Cloudwatch?

In some cases cloudwatch will show INSUFFICIENT_DATA message.

The is the result of the cloudwatch log not being active for the measured time period or no logs being received. For example, if the log is looking at a 1 minute period and no logs have been submitted, you will get this message.

In addition if a configuration is idle for some period of time, it is normal for there to be "insufficient data" because an unused configuration will be sending no data at all to Cloudwatch.

The INSUFFICIENT_DATA message results from two situations:
 - The alarm has not been in existence for the measurement period (eg an alarm that calculates the total over a 1-hour period needs to have existed for at least 1 hour).

- There is no data within the defined period
If there is at least one data point within the past hour, and the alarm has existed for at least an hour, then the state will be either OK or ALARM.
Therefore, you should treat INSUFFICIENT_DATA the same as OK. The current setting treats INSUFFICIENT_DATA the same as OK