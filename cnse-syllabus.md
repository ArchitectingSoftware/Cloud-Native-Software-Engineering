## Cloud Native Software Engineering Syllabus

**INSTRUCTOR:** [Dr. Brian Mitchell](https://www.cs.drexel.edu/~bmitchell)


#### Course Objectives
Introduction to various aspects of software design, development and architecture used to create modern cloud computing software products.  Focus will be placed on covering software engineering concepts, techniques and technologies used to build and deploy applications that run at scale on cloud infrastructure.  Key topics include cloud native software engineering concepts such as working with API-driven infrastructure, software design/architecture considerations for cloud native applications, and various modern technology stacks used in creating cloud software products.  

This course does not require previous background in cloud computing but does assume the student has some background in software design, software architecture and software development.   

#### Lecture Format
This course will balance both theory and practical application.  Most lectures will be structured with 2/3 of the content on cloud native software engineering concepts, with the remaining 1/3 being hands on tutorials on specific cloud native technologies.  

#### Topis (Roughly by Week)
1.	Introduction to cloud computing
    -	Cloud computing models – IaaS, PaaS, FaaS
    -	Fully managed cloud services
    -	Cloud infrastructure concepts – Regions, Availability Zones
    -	Cloud native application characteristics – Scalability, Elasticity, Resiliency, Automation
    -	The big 3 cloud providers – AWS, Azure, GCP
    -	**Tutorial:** _Introduction to the Go programming language_

2.	Software Architectures for Cloud Native Application
    - Event-based architectures
    - Cloud Architecture Patterns for resiliency and scale
    - **Tutorial:** _Go programming continued, API frameworks for Golang_

3.	Designing Cloud Native Applications
    - Domain Driven Design Composition
    - Reference Architectures for Cloud Computing Products
    - **Tutorial:** _API Construction and Analysis – Request/Reply (REST) & Event Based APIs_

4.	API Construction and Deployment
    - Best practices for API construction
    - API Framework components – Routes, Middleware, Asynchronous actions
    - Deep dive into creating Go-based APIs with Golang-Gin.  Design, Deployment, Testing
    - API Ecosystem – API Catalogs, API Gateways, API Security w/ oAuth
    - **In Class Workshop:**  _Guided tour creating and developing two collaborating APIs_

5.	Containerization
    - Docker Architecture Overview
    - Container Architecture Overview
    - Practices for Building, Deploying, and managing containers
    - **Tutorial:** _Docker_

6.	Container Orchestration
    - Why containers must be orchestrated
    - Container integration concepts
    - Container architecture concepts
    - Container networking 
    - **Tutorial:** _Container Orchestration – Docker Compose_

7.	Kubernetes – Industrial Strength Container Orchestration
    - Kubernetes Overview
    - Kubernetes Architecture
    - **Tutorial:** _Kubernetes Part 1_

8.	Kubernetes – Industrial Strength Container Orchestration
    - Kubernetes Architecture Continued
    - Kubernetes offerings in the cloud
    - Managing Kubernetes Deployments – e.g., Helm Charts
    - **Tutorial:** _Kubernetes Part 2_

9.	Function as a Services
    - FaaS concepts
    - FaaS tradeoffs vs Containers
    - **Tutorial:** _OpenFaaS/ KNative_

10.	Additional Considerations for Cloud Native Software Engineering
    - Security Policy Management - IAM
    - Data Considerations for Cloud Native Applications
    - Walkin topics for discussion
    - **In Class Demo:** _Cloud Database Setup_

11. Final course programming assignments due - coordinating containerized APIs.  See the section on the course project for more information. 

#### Expected Learning
By the end of this course the student should be expected to have a solid grasp on:

* Basic knowledge of programming languages used in modern cloud platforms – this class will focus on Go – aka GoLang

* Software architectures, frameworks and patterns used to construct resilient and scalable microservices and modern API based software products

* Working with Popular cloud native services such as Docker, Kubernetes, and FaaS offerings

* Cloud infrastructure architecture – regions, availability zones, edge locations

#### Programming & The Course Project
This course places significant emphasis on hands on software development using the `go` programming language, but also assumes that students have no prior knowledge of `go`.  The initial programming assignments will be derived from the in-class tutorial to get students up to speed.  From there, there will be hands on assignments that cover building and containerizing simple APIs using modern `go` frameworks such as `gin` and `fiber`.   The final half of the course will focus on combining what we have learned into a course project that will incorporate:

* API design best practices
* API implementation and containerization
* API integration and orchestration with 3rd party containerized services such as `redis` and `mysql`.
* Deployment of a multi-API system consisting of both student-developed and 3rd party code into a container orchestration system.

#### Textbook
There is no required textbook for this course.  Materials will be provided by the instructor in Blackboard, and students will be expected to review online materials (websites, Blogs, YouTube videos) provided by the instructor.

#### Time Commitment
The time commitment required to successfully complete this course **_will vary significantly_** depending on students experience with software development toolchains, programming languages and build tools. If you have any questions or doubts about your readiness to take this course please setup time with the instructor to discuss.

#### Grading
Grades **FOR THIS TERM** will be weighted as follows:

1. 65% hands on assignments (both programming and non-programming)
2. 30% online quizzes, roughly 3 of them over the term.
3. 5% for class participation and providing feedback targeted at ongoing course improvements. 

---
##### _The full PDF version of this syllabus is here: [CNSE-Full-Syllabus](./assets/Cloud-Native-Software-Engineering-Syllabus.pdf)_.  The PDF has all of the super fine print, but the grading breakdown and latest coure changes are reflected here. Please make sure you read it.