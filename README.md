Fitness App Microservices

A Java Spring Boot Microservices project for a fitness application with multiple independent services communicating via REST, RabbitMQ, and Kafka. The system uses Eureka for service discovery, Config Server for centralized configuration, API Gateway for routing, and SpringAI integration for AI-based services.

Table of Contents

Features

Technologies

Architecture

Requirements

Setup & Run

Microservices Overview

Testing

Notes

Features

Microservice architecture with independent deployable services.

Centralized configuration with Spring Cloud Config Server.

Service discovery using Eureka Server.

API Gateway for routing and security.

Event-driven communication via RabbitMQ and Kafka.

Data persistence using PostgreSQL and MongoDB.

AI service integration via SpringAI / OpenAI API.

Monitoring endpoints using Spring Boot Actuator.

Technologies

Java 17/23

Spring Boot 3.4

Spring Cloud (Eureka, Config, Gateway)

Spring Data JPA + PostgreSQL

Spring Data MongoDB

RabbitMQ & Kafka

SpringAI (OpenAI)

Docker & Docker Compose

Maven

Architecture
              +-----------------+
              |   API Gateway    |
              +-----------------+
                      |
        +---------------------------+
        |           Eureka          |
        +---------------------------+
          |         |        |
+---------+  +-------------+  +------------+
| UserService | ActivityService | AI Service |
+---------+  +-------------+  +------------+
          |           |        |
       PostgreSQL     MongoDB   RabbitMQ/Kafka


Config Server: Centralized configuration for all microservices.

Eureka Server: Service registry and discovery.

Gateway: Routes external requests to appropriate services.

Userservice: Handles user management (Postgres DB).

ActivityService: Tracks user activity (MongoDB + RabbitMQ).

AI Service: Provides AI-powered recommendations using SpringAI.

Kafka & RabbitMQ: Event streaming and message queue.

Requirements

Docker Desktop (with WSL2 on Windows)

Java 17/23

Maven 3.8+

Optional: Postman or curl for testing

Setup & Run
1. Start Dependencies (Docker)
docker-compose up -d


This will start:

MongoDB → 27017

PostgreSQL → 5432

RabbitMQ → 5672 (management UI: 15672)

Zookeeper → 2181

Kafka → 9092

Check with:

docker ps

2. Run Config Server
cd configserver
mvn spring-boot:run


Port: 8888

Config URL: http://localhost:8888

3. Run Eureka Server
cd eureka
mvn spring-boot:run


Port: 8761

Dashboard: http://localhost:8761

4. Run Microservices

Userservice (Postgres):

cd userservice
mvn spring-boot:run


ActivityService (Mongo + RabbitMQ):

cd activityservice
mvn spring-boot:run


AI Service (Mongo + RabbitMQ + SpringAI):

cd aiservice
export SPRING_AI_OPENAI_API_KEY="sk_XXXX"  # Linux/mac
# OR PowerShell (Windows):
# setx SPRING_AI_OPENAI_API_KEY "sk_XXXX"
mvn spring-boot:run

5. Run API Gateway
cd gateway
mvn spring-boot:run


Default port: 8080

Test route: http://localhost:8080/<service-endpoint>