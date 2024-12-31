# Documentation: Integration of Docker with Jenkins for Spring Boot User Management Project

## Process Overview

### 1. Project Setup and Unit Tests
- Developed a Spring Boot REST API for user management
- Created unit tests using JUnit and Spring Boot Test
- Tests cover user creation, retrieval, and basic CRUD operations
- Repository: https://github.com/mohammedz1ane/demo-project

### 2. Setting Up Jenkins on Windows

Initial attempt with Docker (encountered issues):

``` bash
Download Jenkins image
docker pull jenkins/jenkins:lts
Run Jenkins container
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins jenkins/jenkins:lts
Get initial password
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Solution: Installed Jenkins directly on Windows
- Downloaded Jenkins WAR file
- Ran using `java -jar jenkins.war`
- Accessed via http://localhost:8080

### 3. Jenkins Configuration with GitHub
- Installed necessary plugins (Docker, Pipeline, Git)
- Connected to GitHub repository
- Configured Docker Hub credentials (username: zianemed)
- Set up pipeline with Jenkinsfile from repository

### 4. Docker Integration Challenges
1. **Initial Issues:**
   - Docker in Docker limitations on Windows
   - Permission problems with Docker socket
   - Network connectivity between containers

2. **Solutions Implemented:**
   - Installed Docker Desktop for Windows
   - Configured Docker daemon access
   - Set up proper networking in docker-compose

### 5. Pipeline Implementation
- Created three-stage pipeline:
  1. Build Docker image
  2. Push to Docker Hub
  3. Deploy application

### 6. Deployment Process
1. **Initial Challenges:**
   - MariaDB container connectivity issues
   - Spring Boot application configuration
   - Windows path compatibility

2. **Solutions:**
   - Implemented healthcheck for MariaDB
   - Updated application properties for container environment
   - Modified file paths for Windows compatibility

### 7. Current Status and Improvements
- Successfully building Docker images
- Pushing to Docker Hub repository
- Automated deployment process
- Remaining challenge: Windows-specific Docker networking

## Commands Used

### Jenkins Setup
``` bash
Initial Docker approach (later changed to direct installation)
docker pull jenkins/jenkins:lts
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins jenkins/jenkins:lts
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

### Docker Operations
``` bash
Build and push operations now handled by Jenkins pipeline
docker login
docker build -t zianemed/demo-project .
docker push zianemed/demo-project
```

## Conclusion

The integration process revealed several key learnings:
1. Windows-specific considerations for Docker and Jenkins
2. Importance of proper container networking
3. Benefits of direct Jenkins installation over containerization
4. Successful automation of build and deployment process
