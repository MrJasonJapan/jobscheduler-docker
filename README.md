# SOS Jobscheduler

Dockerfile for Jobschedulerserver www.sos-berlin.com.
Adapted from the floedermann/jobscheduler Docker Hub page.
In particular, the usage of the mariadb:10.1.21 and java:8 repositories is the key difference here.
The js_agent container has also been added.

# General

- Ports:
  - 4446 (Webinterface, username/password: root/root)
  - 40444 (Agents)

# Docker Compose

docker-compose.yml

```
jobscheduler:
  build: .
  # image: spagettys/jobscheduler-docker:latest
  links:
    - db:mysql
  volumes_from:
    - datastore
  ports:
    - '4446:4446'
    - '40444:40444'
db:
  image: mariadb:10.1.21
  ports:
    - '3306:3306'
  environment:
    MYSQL_USER: jobscheduler
    MYSQL_PASSWORD: jobscheduler
    MYSQL_ROOT_PASSWORD: scheduler
    MYSQL_DATABASE: jobscheduler

datastore:
  image: busybox
  command: /bin/true
  volumes:
    - /var/lib/mysql
    - ./live:/opt/jobscheduler/data/scheduler/config/live

js_agent:
  image: js_agent
```

# Usage

### Install with "build: ." (line 2 of docker-compose.yml file)

docker-compose up --build

### Install with "image: spagettys/jobscheduler-docker:latest" (line 3 of docker-compose.yml file)

docker-compose up

### Uninstall

docker-compose down

### Uninstall including volumes (should fix issue where you can't login with root)

docker-compose down -v

# Login

http://localhost:4446 (root / root)

# How to View Test Job Chain with Test Job

After loggin in, navigate to the "Job Chains" tab, then click on the "test" folder in the left pane.
Click on "job_chain1" to view the job chain details. You should see "job01" in the job chain flow representation.

# How to use the Job Agent

comming soon... hopefully...
