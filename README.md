# IAM-Cloud-Project
## Table of Contents

1. [Day 1: Setting Up the Environment](#day-1-setting-up-the-environment)
2. [Day 2: Configuring IAM](#day-2-configuring-iam)
3. [Day 3: Integrating with Lambda and API Gateway](#day-3-integrating-with-lambda-and-api-gateway)
...
## Day 1: Setting Up the Environment

### Introduction

Today marked the beginning of my journey with the Cloud Resume Challenge. The primary focus was to get acquainted with AWS Identity and Access Management (IAM) and set up the foundational elements.

### Goals Achieved 🎯

1. **IAM User ![CR-IAG_App User Success](https://github.com/alexmerelus/IAM-Cloud-Project/assets/138509128/7e7cb4fe-1d95-4382-b779-c8a2bf7ec72d)
Setup**: Successfully set up an IAM user with programmatic access. 
    
2. **IAM Policy Creation in JSON Format**: Created a custom policy for accessing specific AWS services.
![JSON Policy Filled](https://github.com/alexmerelus/IAM-Cloud-Project/assets/138509128/907f2056-6300-4353-a54e-813a14d619ac)


3. **Created S3 Bucket for static website**: Ensured S3 Bucket was created to host resume on AWS S3 with CloudFront
    ![S3 Bucket Succes](https://github.com/alexmerelus/IAM-Cloud-Project/assets/138509128/76f38c37-0afe-483e-8d2b-2eed3226aa62)


4. **Initial AWS CLI Setup**: Initialized AWS CLI to later sync AWS S3.
  ![CLI file test](https://github.com/alexmerelus/IAM-Cloud-Project/assets/138509128/413b1cf3-8398-4c44-a412-1add4418aed5)



### Challenges Faced 🤔

While the day was productive, I faced a few challenges:
- Understanding the difference between AWS managed policies and customer managed policies.
- Ensuring that the IAM user had the least privilege necessary for the tasks.

### Learnings 📘

- **Principle of Least Privilege**: Learned about the importance of granting only the permissions necessary to perform a task.
- **IAM Best Practices**: Got familiar with AWS recommendations for securing IAM resources.

### Next Steps 🐾

- Dive deeper into more advanced IAM configurations.
- Start integrating AWS services using the permissions set up today.

---


...

## Day 2: Configuring IAM🌐

---

#### **Introduction** 📜

On the second day of the Cloud Resume Challenge, my focus shifted to a deeper exploration of AWS's IAM (Identity and Access Management) and setting up the crucial backend components for the serverless application.

---

#### **IAM - The Heart of AWS Security** 🔐

IAM allows me to manage access to AWS services and resources securely. Today, I used it to create and manage AWS users and groups, and used permissions to allow and deny their access to AWS resources.

**Policy Simulator** 🕹️:
The AWS Policy Simulator is a tool to help you understand, test, and validate the effects of your access control policies. I was able to use this to simulate and validate the IAM policies, ensuring they grant permissions as intended.

![Policy Simulator Success](https://github.com/alexmerelus/IAM-Cloud-Project/assets/138509128/fdda4262-2f44-41d5-bd7d-65f56e6ddd2f)


---

#### **Setting Up the Backend** 💻

The backend of our application is crucial as it's responsible for the logic that increments and displays the visit count.

**Lambda Integration with API Gateway** 🚪:
Lambda lets me run code without provisioning or managing servers. I integrated Lambda with API Gateway to trigger my function each time the API endpoint is hit. This allows me to execute the visit counter logic.

![Lambda Function code](https://github.com/alexmerelus/IAM-Cloud-Project/assets/138509128/6f8f6e94-ad01-4e9e-868d-31992a7a76a6)


**CloudResumelAG-EC2Role Setup** 🛠️:
Roles in AWS allow services to interact with resources without the use of security credentials. I set up the `CloudResumelAG-EC2Role` to grant specific permissions to our resources, ensuring the application components can communicate effectively.

![CR-IAG_EC2Role Review ](https://github.com/alexmerelus/IAM-Cloud-Project/assets/138509128/128b39f6-b6cc-418b-b86e-cfaffe2bc480)


---

#### **Conclusion** 🌟

Day 2 was all about setting a strong foundation for the application's security and backend logic. Through IAM, I made sure I secured environment, and with Lambda and API Gateway, I'm now ready to handle and display the website's visits.

Stay tuned for more updates as I continue our journey into the Cloud Resume Challenge!

---

Looking forward to Day 3, for frontend integration and more! 🚀🔍

---

🔗 [Back to Table of Contents](#IAM-Cloud-Project)

...

## Day 3: Integrating with Lambda and API Gateway

**"Decoding the IAM Project: A Deep Dive into AWS Cloud Resume's Visitor Counter"**

🌥️ Today, I'm peeling back the layers of the IAM project I've been working on for my AWS cloud resume. If you've been curious about how Im trying to display a visit count on the index page of my website, but it looks like this is going to be more complex that neccessary so im going to pivot to a different feature that still takes advantage of the Lambda and Api gateway. 

### 1. **Integration with DynamoDB**:
The first feature was the DynamoDB - Amazon's managed NoSQL database service. Specifically, I wanted to set up a table named 'ResumeVisitCounter' for this. This was designed to be a visit tracker for my resume site so that every time someone checks out my site, this function makes sure it's noted.

### 3. **How it 'supposed' to work?**:
Every time the function’s called upon, it should make a change in the DynamoDB table. The 'SiteName' gets updated and the 'ResumeSite' value is changed and each change increase the 'VisitCount' by one, counting every person who visits. So after adding to the count, the function fetches the new count and generates a response to show the new number, in the form of a 200 status code and a JSON response.

- Every time someone lands on my resume page, this function gets a notified by the API Gateway.
- Keeping the numbers in DynamoDB allows me to save the progress over time.

😑😑😑  **Pivoting**:
This felt like a great idea at the time but the way JSON and DynamoDB's number data type is setup, they dont recognize decimal types the same and it led to a serialization error when trying to convert a decimal directly to JSON. Basically like trying to fit a square peg into a round hole. A decimal object, straight from the database to JSON format wasnt possible.

Alternate options,

- **Option 1**: Ditch Lambda for a Python script on EC2. (Paying for extra services)
- **Option 2**: Pair up API Gateway and DynamoDB SDK. Get API Gateway to act as the mediator, transforming the Decimal before the JSON sees it. (Too Complex)
- **Option 4**: Move the counter to the front-end with JavaScript. (Not my expertise)
- **Option 5**: Create a different feature altogether that still uses Lambda and DynamoDB...

I chose option 5 and its currently in the works. Stay tuned. 👨‍💻

...
