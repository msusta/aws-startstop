# Start-stop service
This service was created to automatically stop the development resources during nights and weekends so you don't have to pay for their use.

There's a regular schedule for triggering a Lambda script that checks all the resources for `Nightly` tag key. The value is UTC offset which allows you to set when people using them are in work.

## Deployment
## Configuration
For now only statically defined start and stop hours. Start at 7 and stop at 18. Can be changed by rewriting the script.
## Usage
Tag the supported resource with key `Nightly`. Use the required timezone offset as value. For example:

|Key|Value|Timezone|Running time (UTC)|
|---|---|---|---|
|Nightly|0|UTC|7-18|
|Nightly|+1|CET|8-19|
|Nightly|-6|ETZ|1-12|

If there are multiple teams using the resource, you can use multiple offsets separated by comma. If there's at least one offset that matches the running hours of resource during the check, it's left running.

|Key|Value|Timezone|Running time (UTC)|
|---|---|---|---|
|Nightly|0,+1|UTC and CET|7-19|

## Supported services
* EC2 (outside ASG)

## Planned development
- CloudFormation deployment
- support more services (RDS, ASG...)
- configuration in DynamoDB
- be stateful (don't start what wasn't running)
- tests