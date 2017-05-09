### Problem: I need to whitelist a set of public IP addresses which will be assigned to NGINX instances which are configured in an auto-scaling group. 

### Solutions

1. Lambda (Original Solution) Use Lamba to monitor cloudtrail for new instances of NGINX being spun up by the ASG and then kick of a script which assigns the IP address once the instance has succesfull come online. 
1. User-Data (GroupSolve Solution) Use user-data to execute a script on the new NGINX instances which looks to see which public IP address from the whitelisted pool is available and to assign that to the new instance. 

The group's feelings where that the user-data solution was simpler and would likely work at a mroe reliable and quicker pace then a Lambda funiction looking for log data. It would also be cheaper and the configuraiton would be tightly coupled to the autoscaling configuration and EC2 instances. 
