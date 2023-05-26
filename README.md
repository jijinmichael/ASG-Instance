# Attaching an Instance which is already created to an ASG

To attach an existing instance to an Auto Scaling group, you need to follow these general steps:

1. Create an AMI of the desired Instance. 
2. Create a Launch Configuration.
   Please note choose the newly created AMI 
3. Create an Auto Scaling Group with the above LC. 
   Under the Group size - optional 
   
   Desired capacity = 0
   Minimum capacity = 0
   Maximum capacity = 0
   
4. Then go the Instance section, select the Instance >> Instance Settings >> Attach to Auto Scaling

After that go to the Auto Scaling Groups >> Activity >> Activity History you will see a log as below.

![WhatsApp Image 2023-05-24 at 18 02 04 (1)](https://github.com/jijinmichael/ASG-Instance/assets/134680540/73ae1e1b-022a-40d2-80b1-9ddb39af4e83)
