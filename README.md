EPFL STI DevOps Challenge
v 0.40

----------------------------------------------------------------------------

As requested per the challenge task (found here https://github.com/jaepetto/STI-devops-challenge), this repository includes 4 main components
 - Django web container, running Gunicorn server, based on https://github.com/realpython/dockerizing-django
 - 2 Nginx reverse proxy contianers
 - PostgreSQL DB container
 - HaProxy Load Balancer container

1. Prerequisites
   ```docker```<br/>
   ```docker-compose```<br/>
   ```snap```<br/>
2. Setup
   In order to run initial setup on Ubuntu, either run<br/>
   ```./setup.sh```<br/>
   or<br/>
   ```sudo snap install docker```<br/>

3. Build
   In order to build the container, run ```docker-compose up -d --build```<br/>

4. Prepare Django
   You also need to migrate Django DBs to PostgreSQL DB. For that, run:<br/>
   ```nano epflchallenge/apps/todo/migrations/__init__.py```<br/>
   then (based on previous experience, running migrations outside of container's bash may not complete successfully)<br/>
   ```docker run -ti epfl_challenge_web_1 bash```<br/>
   then<br/>
   ```mkdir epflchallenge/apps/todo/migrations```<br/>
   then<br/>
   ```python manage.py makemigrations```<br/>
   and finally<br/>
   ```python manage.py migrate```<br/>
5. Find the IP<br/>
   ```docker inspect web```<br/>
6. Go to the IP and see the page<br/>


-------------------------------------------------------------------------------
Several important comments:
1. The application uses ```.env``` file to store environment variables, such as PostgreSQL host, user and password, for use in Django ```settings.py```
2. HaProxy uses a script to open the ports
3. Failover can be increased by simply adding additional Nginx node in ```docker_compose.yml``` and ```haproxy.cfg```
4. HaProxy and Nginx can be configured to accept connections over HTTPS, which is important in this day and age.
5. In order to update containers without downtime, it's enough to run ```docker-compose up -d --build```
