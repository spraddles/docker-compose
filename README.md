### Instructions
- install Docker Desktop: https://www.docker.com/products/docker-desktop
- download this repo (docker-compose) and make sure it's in the same root DIR as the Frontend + Backend GIT repos, i.e. so you have all 3 repos at the same level
- get a dump of Production database and rename to 'database.sql' in the 'src' DIR
- run 'docker compose up' to start (you can now edit your code live on your Local repos & this will be reflected in the Docker Container)
- run 'docker compose down' to stop


This will create the following endpoints on your Local: 
- Database: http://localhost:3306
- PHPmyAdmin: http://localhost:8080/index.php
- Backend: http://localhost:8765
- Frontend: http://localhost:8000/marketing/home.html


### Other commands
- 'docker compose down && docker system prune --all -f' removes all containers, networks, images, and persistent volumes (e.g. Database)
- sometimes this prune command doesn't work (known Docker bug) so just repeat it a couple times & it will work after a few tries


### Issues
- phpMyAdmin can't connect error: wait about 30 seconds for all Docker services to run (due to healthcheck issues)


### Tasks
- frontend service: add in 'grunt watch'
- database service: create a better healthcheck for MySQL, current one has issues
- backend service create a healthcheck for the backend
- frontend service: add 'depends on backend' when backend healthcheck exists
- create a base image for common OS (i.e. backend + frontend both use 'ubuntu:18.04')
- remove un-needed .sh files in service directories


### Notes
- the first time you run Docker it will take a few minutes, subsequent runs will go faster
- SQL database: remember to update this file often to keep parity with the Prod Database
- SQL database: this is volume mounted & persists in Docker, meaning changes you make to it will stay unless you remove the volume (use the prune command to do this)
- if you have problems, run the prune command and then run docker ('docker compose up')
- localhost in Docker is 0.0.0.0 (not 127.0.0.1)
- you cannot use COPY or ADD commands in a Dockerfile with Docker Compose
- you cannot use COPY or ADD commands if you are Bind mounting (aka Host mount), but you can with Volume mounting
