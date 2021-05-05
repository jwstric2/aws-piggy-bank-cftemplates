h1. Description

Sets a default retention time on all cloudwatch log groups per a defined cron event.  This is based largely on code with some modifcations at https://www.linkedin.com/pulse/enforcing-cloudwatch-log-expiration-shabbir-bata.

While cloudwatch is relatively cheap; never expiring log groups will accumlate storage and analyze cost across the logs (insights).  As of May, th 2021 the costs are below:

```
Store (Archival)	$0.03 per GB
Analyze (Logs Insights queries)	$0.005 per GB of data scanned
```

Taking just storage, lets say you are pushing 10 gigs of logs in a month.  Thats 0.30 a month for storage.  At the end of 12 months you will be paying 3.60.  While a drop in the bucket, these cost will continue to climb at the same linear rate over time.  


h2. Variables

ExpireEventsAfter -> The retention time to set on the cloudwatch log groups.  Allowed values are 7, 14, 30, 60, 120, and 180.  Default of 14 days
LambdaRate -> The time to run the lambda to check and set the retention times.  Allowed value are `cron(0 0 * * ? *)`, `cron(0 0 ? * SUN *)`, and `cron(0 0 1 * ? *)`. Default of `cron(0 0 * * ? *)`

h1. Other

h2. Bypass retention set

Add the following tag key/value to the loggroup to skip modifying retentions for certain log groups.

```
Key: SkipModifyRetention
Value: True
```

h1. Credits

https://www.linkedin.com/pulse/enforcing-cloudwatch-log-expiration-shabbir-bata
