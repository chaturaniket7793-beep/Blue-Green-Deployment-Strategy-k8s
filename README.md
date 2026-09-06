# Blue-Green-Deployment-Strategy-k8s
# AWS Blue-Green Deployment using EC2 and Application Load Balancer

## Project Overview

This project demonstrates a working **Blue-Green Deployment Strategy** on AWS using:

* Amazon EC2
* Application Load Balancer (ALB)
* Target Groups
* Ubuntu Server
* Nginx
* Git
* GitHub

The objective is to deploy two versions of a web application and switch production traffic between them with minimal downtime.

## Architecture

```text
                         Internet
                            |
                            v
                Application Load Balancer
                            |
                  ---------------------
                  |                   |
                  v                   v
           Blue Target Group   Green Target Group
                  |                   |
                  v                   v
            Blue EC2 Server     Green EC2 Server
             Version 1.0          Version 2.0
```

## Blue Environment

* **Server Name:** blue-server
* **Application Version:** 1.0
* **Status:** Live Production

## Green Environment

* **Server Name:** green-server
* **Application Version:** 2.0
* **Status:** New Deployment

## Deployment Process

1. Create Blue EC2 instance.
2. Install Nginx on the Blue server.
3. Deploy Version 1.0 application.
4. Create Green EC2 instance.
5. Install Nginx on the Green server.
6. Deploy Version 2.0 application.
7. Create a Blue Target Group.
8. Create a Green Target Group.
9. Register the Blue EC2 instance with the Blue Target Group.
10. Register the Green EC2 instance with the Green Target Group.
11. Create an Application Load Balancer.
12. Configure the ALB listener to forward traffic to the Blue Target Group.
13. Verify that Version 1.0 is accessible through the ALB.
14. Test the Green environment independently.
15. Switch the ALB listener from the Blue Target Group to the Green Target Group.
16. Verify that production traffic is now served by Version 2.0.
17. Perform rollback to Blue if required.

## Blue to Green Switch

### Initially

Production traffic is routed to the Blue environment:

```text
              ALB
               |
               v
             BLUE
          Version 1.0
```

### After Deployment

The ALB listener is changed to route production traffic to Green:

```text
              ALB
               |
               v
            GREEN
          Version 2.0
```

## Rollback

If the Green deployment has a problem, production traffic can quickly be switched back to the Blue Target Group.

```text
              ALB
               |
               v
             BLUE
          Version 1.0
```

This provides a fast rollback mechanism without requiring the previous application version to be redeployed.

## Key Benefits

* Minimal production downtime
* Safe application releases
* Easy testing of the new version before production traffic is switched
* Fast rollback capability
* Reduced deployment risk
* Separate environments for the current and new application versions

## Technologies Used

* **AWS EC2**
* **AWS Application Load Balancer**
* **AWS Target Groups**
* **Ubuntu Server**
* **Nginx**
* **Git**
* **GitHub**

## Deployment Flow

```text
Create Blue EC2
       |
       v
Install Nginx
       |
       v
Deploy Version 1.0
       |
       v
Create Green EC2
       |
       v
Install Nginx
       |
       v
Deploy Version 2.0
       |
       v
Create Target Groups
       |
       v
Create Application Load Balancer
       |
       v
Route Traffic to Blue
       |
       v
Test Green
       |
       v
Switch Traffic to Green
       |
       v
Monitor Application
       |
       +------> If failure ------> Rollback to Blue
```

## Author

**Aniket Chatur**
