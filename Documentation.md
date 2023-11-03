## Purpose

This blitz focuses on addressing the challenge of effectively managing traffic spikes during US holidays within the context of the URL Shortener application. It explores the economic benefits of utilizing auto-scaling and resource-efficient strategies to ensure high availability and responsiveness during peak traffic periods, while optimizing costs and resource utilization.


## Initial Step: Re-deploy the URL-Shortener Application on Elastic Beanstalk

We manually configured the AWS Elastic Beanstalk environment with T.2 micro to deploy the url-shortener application. 

<img width="746" alt="Screen Shot 2023-10-31 at 4 46 49 PM" src="https://github.com/SaraGurungLABS01/Blitz-3/assets/140760966/eb78c68b-ec52-42ba-ba8d-f98f8e50f3c9">


<img width="1742" alt="Screen Shot 2023-10-31 at 4 47 28 PM" src="https://github.com/SaraGurungLABS01/Blitz-3/assets/140760966/53378503-b6cc-4613-bf91-5a593b49282b">


## Summary on Infrastructure Configuration

# Overview of Application Deployment

This overview provides a high-level summary of the tools, components, installations, and plugins used in the application deployment.

## Tools and Components

- **GitHub**: GitHub is a web-based platform for version control and collaboration. It was used to host the project repository, enabling code management and collaboration among team members.

- **Amazon EC2**: Amazon Elastic Compute Cloud (EC2) is a cloud computing service that provides resizable virtual machines for hosting applications. In this project, EC2 instances were used to host the web application and Jenkins.

- **Jenkins**: Jenkins is an open-source automation server used for building, deploying, and automating software development pipelines. In this project:
  - Jenkins was installed on an Amazon EC2 instance, enabling automation of the CI/CD process.
  - The "Pipeline Keep Running Step" plugin was added to Jenkins, enhancing pipeline automation by allowing specific steps to continue until specific conditions are met.

- **Nginx**: Nginx is a web server and reverse proxy server. It was configured to act as a reverse proxy for the web application, handling incoming HTTP requests and forwarding them to the application server.


## Issue:

During the US holidays, the URL Shortener faces a critical challenge as it experiences unexpected traffic spikes, with request rates ranging from 900 to 1,000 requests per second. This surge in traffic poses a severe performance bottleneck, given that the URL Shortener can efficiently handle a maximum of 700 requests per second on a single T2 micro instance. The issue is further compounded by the fact that there are 12 government-recognized holidays in a year. To maintain a high-quality user experience and ensure the availability of the service during these peak periods, a comprehensive solution is required to effectively address and mitigate the performance limitations and scaling constraints of the URL Shortener infrastructure.

**Initial Blitz with 700 requests**

Initially, the Quality Assuarance Engineer blitzed our instance with 700 requests

**700 requests per second:**

![Screenshot 2023-10-31 161804](https://github.com/SaraGurungLABS01/Blitz-3/assets/140760966/05ee562f-1cc8-4ec8-a5ab-f5309ec716ef)

**Result:** No Error

![after 700](https://github.com/SaraGurungLABS01/Blitz-3/assets/140760966/f6d364b0-9dc3-4702-8ffa-76733743e1c4)


**Blitz with 1000 requests**

QA Engineer blitzed our instance with 1000 requests. The goal is to to check if our application  can handle 1000 requests per second.

**1000 requests per second**

![1000 request](https://github.com/SaraGurungLABS01/Blitz-3/assets/140760966/672bd1ce-f0e2-48e3-94d7-a1c06286463b)


**Result:** Error- our application was not able to handle the traffic

![after 1000](https://github.com/SaraGurungLABS01/Blitz-3/assets/140760966/46f79f98-6c93-4258-be06-cbc89ed413ca)


## Resolution

To address the challenge of handling traffic spikes during US holidays, where request rates can surge to 900-1,000 requests per second, a scalable and cost-efficient approach is essential. Given that the URL Shortener can efficiently handle up to 700 requests per second on a single T2 micro instance, it's imperative to find a solution that ensures high availability without incurring unnecessary costs.

**Auto-Scaling for Traffic Spikes**: To effectively manage the varying traffic load, auto-scaling is a practical solution. Auto-Scaling Groups (ASG) can be configured to automatically adjust the number of instances based on traffic demand. When traffic exceeds the 700 requests per second threshold, the ASG will seamlessly launch additional instances to handle the increased load. This dynamic scaling ensures that the application can efficiently accommodate traffic spikes during the limited 12 government-recognized holidays without overprovisioning resources during the rest of the year.

**Elasticity with Cost Efficiency**: Auto-scaling not only ensures elasticity but also cost efficiency. Rather than running continuously powerful instances that may be underutilized during non-peak periods, auto-scaling allocates resources based on actual demand. This approach results in cost savings as you only pay for the resources you use when you need them, making it an economically sound choice.

In conclusion, the approach of auto-scaling provides an effective solution for handling unexpected traffic spikes during US holidays while maintaining cost-efficiency throughout the year. This solution ensures the URL Shortener remains responsive and available during peak periods, providing a high-quality user experience.


## Question

**Economic Benefits of Using Auto-Scaling and an ALB vs. a Stronger Instance (c5.4xlarge)**

During US holidays, the URL Shortener experiences unexpected traffic spikes, with request rates ranging from 900 to 1,000 requests per second. To handle this surge in traffic, what are the economic benefits of using auto-scaling in conjunction with an Application Load Balancer (ALB) compared to relying on a single, more powerful instance like a c5.4xlarge with increased bandwidth?


Using auto-scaling and an Application Load Balancer (ALB) offers significant economic benefits compared to relying on a single, more powerful instance like a c5.4xlarge. Auto-scaling and ALB provide a cost-efficient solution by dynamically adjusting resource allocation based on actual demand. This ensures that you only pay for the resources you use, avoiding unnecessary fixed costs associated with continuously running a high-capacity instance. Additionally, auto-scaling offers resource optimization, preventing underutilization during non-peak periods, and enhancing availability through redundancy. In contrast, a stronger instance, while providing high performance and bandwidth, incurs continuous fixed costs, leads to resource underutilization, and has scalability limitations, making it less economically efficient, especially for handling variable traffic loads.

## Diagram

![Blitz3 drawio](https://github.com/SaraGurungLABS01/Blitz-3/assets/140760966/e85e019c-dd58-4705-a6ad-5f9bb8e47e5d)

