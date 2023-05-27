### Reboot an instance which is created by Auto Scaling Group

When an instance is manually rebooted within the ASG, the ASG may still view the instance as unhealthy since services were interrupted. Similar to the automatic procedure outlined above, the ASG may be prompted by this to end the current instance and start a new one.

Here's what typically happens:

1. *Reboot*: When you initiate a reboot for an instance, the operating system gracefully shuts down and restarts, which may take a few minutes. During this time, the instance becomes temporarily unavailable.
2. *Replacement*: The Auto Scaling Group identifies that the instance is no longer in a healthy state (as it was temporarily unavailable) and terminates it.
3. *New instance creation*: The Auto Scaling Group immediately launches a new instance to replace the terminated one. The new instance is created using the same launch configuration or template specified in the Auto Scaling Group.

To avoid disruptions caused by reboots, you can take the following measures:

### 1. Detach and Reboot
### 2. Standby and Reboot

### Detach and Reboot

Detaching an instance refers to removing it from an Auto Scaling group. When you detach an instance, it is no longer managed by the Auto Scaling group, and it continues to run independently. Detaching can be useful in scenarios where you want to take manual control over an instance or perform specific actions that are not handled by the Auto Scaling group.

An ASG won't automatically replace a restarted instance if you detach an instance from it and subsequently reattach it. In this case, the following is usually what occurs:

1.Detachment: When you detach an instance from an ASG, the ASG no longer manages that instance. The instance is essentially removed from the ASG's control and becomes a standalone instance.

2.Reboot: Once you initiate a reboot for the detached instance, it goes through the usual reboot process. The operating system gracefully shuts down and restarts.

3.Replacement: Since the instance is no longer part of the ASG, the ASG does not actively monitor it or replace it. Therefore, no automatic replacement occurs when the instance is rebooted. The detached instance will remain as an individual, separate instance.

Please note that while detaching, please uncheck Replace Instance option and please make sure that the minimum group size value must be equal to 0(Zero).

To do this, go to ASG >> Instance Management >> Select the Instance >> Action >> Detach.

![image](https://github.com/jijinmichael/ASG-Instance-Management/assets/134680540/d84f8af8-6c18-4fa7-8778-b0420d2a62ab)

You can see an activity history as follows.
![WhatsApp Image 2023-05-24 at 18 03 48 (1)](https://github.com/jijinmichael/ASG-Instance-Management/assets/134680540/5d9a8eb1-3459-44bc-8e94-eb805262b753)

### Standby and Reboot

Placing an instance in standby means that it is temporarily removed from the Auto Scaling group's active capacity but remains associated with the group. The instance is not terminated but is prevented from receiving traffic or participating in scaling activities. Standby instances can be a part of the Auto Scaling group again when needed, without launching new instances.

Standby instances are useful in situations such as performing maintenance on instances, troubleshooting, or applying updates. By putting an instance in standby, you can ensure that it doesn't receive traffic during such activities while still keeping it as a part of the group for future use.

When you make an instance standby from an Auto Scaling Group (ASG) and then reboot it, the following actions typically occur:

1. Standby state: When you mark an instance as standby in an ASG, the instance is removed from the load balancer or target group that the ASG is associated with. The instance is no longer considered in the ASG's scaling activities. However, the instance remains registered with the ASG and retains its instance ID.

2. Reboot: Rebooting the instance while it's in standby state is similar to a regular reboot. The instance is restarted, and any processes or services running on the instance are temporarily halted and then resumed once the reboot is complete. The instance retains its IP address, storage volumes, and other configuration settings.

Like detach, to make the instance standby, please uncheck Replace Instance option.
![image](https://github.com/jijinmichael/ASG-Instance-Management/assets/134680540/0a651a32-3a0c-44b1-9db3-25f86edecf53)

You can see an activity history as follows.
![WhatsApp Image 2023-05-24 at 18 06 59 (1)](https://github.com/jijinmichael/ASG-Instance-Management/assets/134680540/9400f4f6-e6e5-4bb2-8548-271f25e98fa5)

To summarize, detaching an instance permanently removes it from the Auto Scaling group, while placing an instance in standby temporarily removes it from the group but retains its association for easy reactivation.
