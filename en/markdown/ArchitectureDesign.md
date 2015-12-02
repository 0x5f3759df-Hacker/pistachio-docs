# Architecture Design Of Pistachio

#Introduction

Pistachio is an open-source project based on the *Data Structure Assignment, Project 6 - Book Management System*.

Pistachio is released under the **[MIT License](https://opensource.org/licenses/MIT)**, and all documents of Pistachio are released under **[CC BY 4.0 License](http://creativecommons.org/licenses/by/4.0/)**. All rights reserved by **all members of our 0x5f3759df-Hacker Team**.

This document illustrates the architecture design of Pistachio.

---

#I.The architecture of the frontend

##Overview

##UI
###Major design

###Responsive page design

##MVVM architecture

##Performance optimization

###CSS/JS Code optimization
Compressing and streamlining the CSS/JS code, eliminating duplicated and unused code, merging the code via optimization and build. These could minimize the number of http requests.
###Using CDN
The essence of CDN is cache. CDN caches data where approach to users, thus providing the fastest access to resources for users. When deploying our service online, we will take advantage of Baidu CDN image to speed up.
###Resource loading order adjustment

---

#II.The architecture of the backend

##Overview

##Business layer

##API design

##Concurrency

##High availability architecture

##Scalable architecture

##Security architecture

##Distributed architecture

##High performance architecture
###Code optimization

###JVM optimization

- Java Heap : pending (plan, 2048MB -> Standalone)
- Java E:S ratio : pending -> default
- Java promotion threshold : pending
- GC : Parallel Scavenge + Concurrent Mark-Sweep

---

#III.Build, delivery and deployment

##Project dependencies

##Remote repositories
###Frontend

- Develpoment: Taobao npm repository + Bower repository
- Production: Baidu CDN

###Backend

- Gradle: We use Maven repository and OSC Maven repository at the same time (pulling the domestic repository via the continuous integration components might lead to project building failure due to the terrible network delay)

##Build environment

At present, we divide Pistachio into two parts, frontend and backend.

The frontend part process automatic building and testing with Gulp.js. Here is the build environment of the frontend:

- Node.js 4.2.2 LTS (Local build)
- Node.js 4.1 (Continuous integration)

The backend part process automatic building and testing with Gradle. Here is the build environment of the backend:

- Oracle JDK 1.8.0u65（HotSpot JVM） + Scala 2.11.7 + Gradle 2.9 (Local build)
- OpenJDK 1.8.0（HotSpot JVM） + Scala 2.11.7 + Gradle 2.6 (Continuous integration)

##Continuous integration

Pistachio uses [Travis CI](https://travis-ci.com) and [AppVeyor](https://ci.appveyor.com/) to process automatic continuous integration. Every time the we push a branch, the CI components will automatically build the project as well as return the build feedback timely.

##Delivery and deployment

The traditional way of deployment is very tedious. In order to eliminate various cumbersome environment configuration and accomplish one-key deployment, we make the best use of Docker, which is a lightweight virtualization container based on Linux kernal.

We will push our Dockerfile to the remote repository(GitHub and Docker Hub). Furthermore, the servers of the Docker Hub might be fucked by the GFW sometimes because they are deployed on Amazon S3, so for the purpose of high speed, we will also push the Dockerfile to domestic Docker service providers DaoCloud and TenxCloud. And we intend to demonstrate our project online on TenxCloud's service.
