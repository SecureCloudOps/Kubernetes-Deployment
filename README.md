
# Set Up Kubernetes Deployment


**Author:** Mohamed Mohamed  
**Email:** mohamed0395@gmail.com

---

## Set Up Kubernetes Deployment

![Image](https://imgur.com/88ThsPz.png)

---

## Introducing Today's Project!

In this project, I will clone a backend application from GitHub, build a Docker image of the backend, and push it to an Amazon ECR repository. I will also troubleshoot installation and configuration errors to enhance my problem-solving skills. This is important because it provides hands-on experience in containerization, cloud-based image storage, and debugging, which are essential skills for cloud and DevOps roles.

### Tools and concepts

![Image](https://imgur.com/pJnLmz9.png)

I used **Amazon EKS, Git, Docker, and Amazon ECR** to deploy a containerized backend application. Key steps include:  
1. **Cloning the backend repository** from GitHub using Git.  
2. **Building a Docker image** to package the application and its dependencies.  
3. **Pushing the image to Amazon ECR** for centralized storage.  
4. **Deploying the image on an Amazon EKS cluster** to enable scalable and reliable execution.  
These tools and steps ensured efficient **container orchestration, version control, and automated deployment** within AWS infrastructure.

### Project reflection

This project took me approximately **1 hour** to complete. The most challenging part was **resolving Docker permissions and ensuring smooth deployment to Amazon EKS**, as it required troubleshooting authentication and network configurations. My favorite part was **building and pushing the container image to Amazon ECR**, as it demonstrated how containerized applications can be efficiently stored and deployed in a scalable environment.

Something new that I learned from this experience was **how to integrate Amazon EKS with Amazon ECR for seamless container deployment**. I also gained hands-on experience with **troubleshooting Docker permission issues** and managing containerized applications using **Kubernetes**. This project deepened my understanding of **cloud-based CI/CD workflows**, making deployments more scalable and efficient.

---

## What I'm deploying

To set up today's project, I launched a Kubernetes cluster. Steps I took to do this included installing `eksctl`, which simplifies EKS cluster creation, and setting up an IAM role to grant necessary AWS permissions. I then used `eksctl` to provision an EKS cluster, allowing AWS to automatically configure networking resources. Finally, I verified the cluster setup and ensured that worker nodes were registered successfully.

### I'm deploying an app's backend

Next, I retrieved the backend that I plan to deploy. An app's backend handles data processing and logic, ensuring proper functionality. I retrieved the backend code by first installing Git on my EC2 instance. Then, I cloned the `nextwork-flask-backend` repository from GitHub using the `git clone` command. This copied all necessary backend files, including `app.py`, `Dockerfile`, and `requirements.txt`, onto my EC2 instance, preparing it for deployment.

![Image](https://imgur.com/6jItNB6.png)

---

## Building a container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because a container image packages the application with all its dependencies, ensuring consistency across different environments. Using a **Dockerfile**, the image is built with all necessary configurations, making it portable and scalable. This allows Kubernetes to deploy multiple instances of the backend efficiently, ensuring reliability in development, testing, and production environments.

When I tried to build a Docker image of the backend, I ran into a permissions error because the **ec2-user** does not have the required privileges to access the Docker daemon. Docker requires root-level permissions to execute commands like `docker build`. Since **ec2-user** is a non-root user, it was denied access to the Docker socket (`/var/run/docker.sock`). To fix this, I need to either **run the command with `sudo`** or **add `ec2-user` to the Docker group** for persistent access.

To solve the permissions error, I added **ec2-user** to the **Docker group** using the command:  
```sh
sudo usermod -a -G docker ec2-user
```
The **Docker group** allows non-root users to run Docker commands without needing `sudo`. The `usermod` command updates the user's groups, and the `-a -G` flags ensure that **ec2-user** retains existing group memberships while being added to the Docker group. After running this command, I logged out and back in to apply the changes, allowing me to build and manage Docker containers without permission issues.

![Image](https://imgur.com/88ThsPz.png)

---

## Container Registry

I'm using Amazon ECR in this project to store and manage my container images securely. ECR is a good choice for the job because it integrates seamlessly with AWS services like **EKS**, allowing Kubernetes to pull images efficiently with minimal authentication setup. It provides **scalability, security, and high availability**, ensuring that my containerized applications are deployed reliably across different environments.

Container registries like Amazon ECR are great for Kubernetes deployment because they provide a **centralized, secure, and scalable** storage solution for container images. They allow Kubernetes to **pull images efficiently**, ensuring **consistent deployments** across different environments. ECR integrates seamlessly with AWS services, reducing authentication complexity while improving **availability, version control, and automated updates** for containerized applications.

![Image](https://imgur.com/OXMPnrg.png)

---

## EXTRA: Backend Explained

After reviewing the app's backend code, I've learned that it is responsible for **fetching data** based on user input, using **Flask** to interact with an **external API**, and processing the retrieved information. The backend then formats the data into **JSON** for easy consumption by the frontend or other services. This structure ensures efficient data retrieval, processing, and response handling, making the application dynamic and responsive.

### Unpacking three key backend files

The **requirements.txt** file lists all the dependencies and libraries needed to run the application. It ensures that the correct versions of packages are installed, maintaining consistency across different environments. This file allows for easy installation using `pip install -r requirements.txt`, making application setup and deployment more efficient and reproducible.

The **Dockerfile** gives Docker instructions on how to build a containerized version of the application. Key commands in this Dockerfile include:
- `FROM` to specify the base image,
- `COPY` to add application files to the container,
- `RUN` to install dependencies,
- `CMD` or `ENTRYPOINT` to define how the container should execute the application.  
This ensures that the app runs consistently across different environments, making it easier to deploy with Kubernetes.

The **app.py** file contains the main application logic for the backend. It typically includes **routes, request handling, and business logic** using a web framework like Flask or Django. This file defines how the backend processes client requests, interacts with databases, and returns responses, making it essential for the functionality of the application.

---

---
