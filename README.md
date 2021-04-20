EPFL STI DevOps Challenge
v 0.40

----------------------------------------------------------------------------

As requested per the challenge task (found here https://github.com/jaepetto/STI-devops-challenge), this repository includes 4 main components
 - Django web container, running Gunicorn server, based on https://github.com/realpython/dockerizing-django
 - 2 Nginx reverse proxy contianers
 - PostgreSQL DB container
 - HaProxy Load Balancer container

1. Prerequisites
   ```docker```\n
   ```docker-compose```\n
   ```snap```
2. Setup
   In order to run initial setup on Ubuntu, either run
   ```./setup.sh```
   or
   ```sudo snap install docker```

3. Build
   In order to build the container, run ```docker-compose up -d --build```

4. Prepare Django
   You also need to migrate Django DBs to PostgreSQL DB. For that, run:
   ```nano epflchallenge/apps/todo/migrations/__init__.py```
   then
   ```docker run -ti epfl_challenge_web_1 bash```
   then
   ```mkdir epflchallenge/apps/todo/migrations```
   then
   ```python manage.py makemigrations```
   and finally
   ```python manage.py migrate```
5. Find the IP
   ```docker inspect web```
6. Go to the IP and see the page


-------------------------------------------------------------------------------
Several important comments:
1. The application uses ```.env``` file to store environment variables, such as PostgreSQL host, user and password, for use in Django ```settings.py```
2. HaProxy uses a script to open the ports
3. Failover can be increased by simply adding additional Nginx node in ```docker_compose.yml``` and ```haproxy.cfg```
4. HaProxy and Nginx can be configured to accept connections over HTTPS, which is important in this day and age.
