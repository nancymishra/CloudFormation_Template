# Notify when any resource is deleted from AWS Account (Cloudformation Template)
# Workflow: 
![image](https://user-images.githubusercontent.com/62890188/127000534-fccad471-a645-434a-86b1-3ac225ca0f27.png)

AWS Config will record every configuration change in the region it is enabled for. Then using the Cloudwatch rule we can specifically record the deletion of resources present in the AWS Config region. Whenever any resource is deleted in the region, information will be sent to the Cloudwatch rule. Further, the rule will send this information to the target which is the SNS topic. The topic is subscribed by the AWS account holder to get notifications for any resource deletion. So, the SNS will send the notification to the subscription endpoint (Email ID) whenever any resource would be deleted from the AWS Config region

# Steps to achieve the task:
1. Enable AWS Config for the region you will be using for your resources. Create a bucket to store all the config information. 

![image](https://user-images.githubusercontent.com/62890188/127000694-e458da26-b774-4f4a-9204-e781d90998da.png)

2. Make a template to create a Cloudformation stack.We need to create the following from the stack:
•	SNS topic and subscription to topic 
•	Cloudwatch rule for aws config which has the SNS topic as target
•	SNSTopicPolicy

 ![image](https://user-images.githubusercontent.com/62890188/127000766-d76fd1c5-6243-47e0-91ed-3cc22119bcb8.png)
![image](https://user-images.githubusercontent.com/62890188/127000783-a52913f6-b49f-416f-9612-d5ae0e354e33.png)
![image](https://user-images.githubusercontent.com/62890188/127000797-4220a4f1-353e-4bba-8ce3-7bd2921d6323.png) 

This is the structure for the Stack 
3. Create the Stack from the template 

 ![image](https://user-images.githubusercontent.com/62890188/127000840-624f3650-cb76-4e3c-bb33-f08362b8e94b.png)

4. Verify the created resources:
•	SNS Topic

 ![image](https://user-images.githubusercontent.com/62890188/127000873-3cdf258c-1c5f-4924-83ac-40e916a75a76.png)

•	Subscription to topic

 ![image](https://user-images.githubusercontent.com/62890188/127000888-dbb4b5cd-b890-44a2-b074-0ee42f9996ae.png)

•	Cloudwatch rule

 ![image](https://user-images.githubusercontent.com/62890188/127000900-01565805-c0b7-4f82-9841-d6f270fa356f.png)

•	The target is SNS Topic 

 ![image](https://user-images.githubusercontent.com/62890188/127000922-2385073d-e7d7-48aa-a102-e285c57b1c6c.png)

5. An email would be sent to the email ID mentioned as the subscription endpoint for the SNS topic. Confirm the subscription to start receiving notifications

 ![image](https://user-images.githubusercontent.com/62890188/127000951-01d8cba7-be28-46dd-83a8-b72f06419acd.png)

6. Now, to verify the complete process, delete any resource from your AWS account.

 ![image](https://user-images.githubusercontent.com/62890188/127000969-bc7ada10-4673-4c1e-aa79-dc8e043e06f2.png)

Terminate this instance and you will receive a notification email on your Email ID about this change in your AWS Config region on your Account. 

 ![image](https://user-images.githubusercontent.com/62890188/127001000-c2665e77-2643-4434-8ed4-5f06972db32a.png)

Similarly we can try deleting other resources like S3 bucket, or EBS volume, IAM policy, etc. We will be notified for every resource deletion. 

![image](https://user-images.githubusercontent.com/62890188/127001019-d4c43913-4368-4d53-9d69-e72322059090.png)
![image](https://user-images.githubusercontent.com/62890188/127001053-dac6e11b-f833-4dd0-b6eb-cab88cb786c6.png)
![image](https://user-images.githubusercontent.com/62890188/127001067-099386a4-6ef3-4fea-b489-158028b1f0b8.png)

