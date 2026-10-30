# Cloud Lab 2 Submission — Load Balancer and Auto Scaling


- **Student name: Loeng Pheaktra**
- **Student ID: e20220993**
- **Learner Lab user name: LOENG_PHEAKTRA**
- **Date completed: 30/10/2026**

---

## Security groups

![LoadBalancerSecurityGroup](images/01-sg-load-balancer.png)

![LaunchTemplateSecurityGroup](images/02-sg-launch-template.png)

## Target group

![LoadBalancerTargetGroup](images/03-target-group.png)

![Health checks](images/04-health-checks.png)

## Application Load Balancer

![Load balancer list](images/05-load-balancer-list.png)

![Load balancer details](images/06-load-balancer-details.png)

## Launch template

![AutoScalingLaunchTemplate](images/07-launch-template.png)

## Auto Scaling group

![Auto Scaling groups](images/08-asg-list.png)

![Auto Scaling group details](images/09-asg-details.png)

## Load balancing test

![First request](images/10-browser-1.png)

![Second request, different host](images/11-browser-2.png)

## Simulated application failure

![Stopping httpd](images/12-stop-httpd.png)

![Target unhealthy or draining](images/13-target-unhealthy.png)

![New target healthy](images/14-target-replaced.png)

About how many minutes passed between stopping `httpd` and the new instance becoming healthy?
-> about 10min

---

## Questions

1. Why does the page show a different host name when you refresh it?
2. After you stopped `httpd`, the instance was still *running* in EC2, but the target group marked it *unhealthy*. What did the health check test, and why did the instance fail it?
3. Who replaced the failed instance: the load balancer, the target group, or the Auto Scaling group? Explain the role of each one.
4. With desired 2, minimum 2 and maximum 3, how many instances run normally? In what situation could there be 3?
5. The instances' security group allows HTTP from anywhere. How could you change it so that the instances accept HTTP **only** from the load balancer?

## Answer

1. The page shows a different hostname because the load balancer distributes requests between different EC2 instances, and each instance has its own hostname.

2. The health check tested whether the web server (HTTP) was responding. After stopping httpd, the server could no longer respond to HTTP requests, so the target became unhealthy.

3. The Auto Scaling group replaced the failed instance. The load balancer distributes traffic, the target group checks instance health, and the Auto Scaling group launches replacement instances.

4. Normally, 2 instances run. There could be 3 instances when traffic increases or when Auto Scaling launches a replacement before removing an unhealthy instance.

5. Change the instances' security group to allow HTTP (port 80) only from the load balancer's security group instead of allowing traffic from anywhere.

## Clean up

- [x] `MyAutoScalingGroup` deleted and its instances terminated.
- [x] `AutoScalingLaunchTemplate` deleted.
- [x] `MyLoadBalancer` and `LoadBalancerTargetGroup` deleted.
- [x] Both security groups deleted.
