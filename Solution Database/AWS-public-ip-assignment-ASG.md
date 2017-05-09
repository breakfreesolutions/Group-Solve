### Problem: I need to whitelist a set of public IP addresses which will be assigned to NGINX instances which are configured in an auto-scaling group. 

### Solutions

1. (Original Solution) use Lamba to monitor cloudtrail for new instances of NGINX being spun up by the ASG and then kick of a script which assigns the IP address once the instance has succesfull come online. 
1. (
