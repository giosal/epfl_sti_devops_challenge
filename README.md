EPFL STI DevOps Challenge
v 0.40

----------------------------------------------------------------------------

As requested per the challenge task, this repository includes 4 main components
 - Django web container, running Gunicorn server
 - 2 Nginx reverse proxy contianers
 - PostgreSQL DB container
 - HaProxy Load Balancer container

1. Prerequisites
   '''docker'''
   '''docker-compose'''
   '''snap'''
2. Setup
   In order to run initial setup on Ubuntu, either run
   '''./setup.sh'''
   or
   '''sudo snap install docker'''

3. Build
   In order to build the container, run '''docker-compose up -d --build'''

4. Prepare Django
   You also need to migrate Django DBs to PostgreSQL DB. For that, run:
   '''nano epflchallenge/apps/todo/migrations/__init__.py'''
   then
   '''docker run -ti epfl_challenge_web_1 bash'''
   then
   '''mkdir epflchallenge/apps/todo/migrations'''
   then
   '''python manage.py makemigrations'''
   and finally
   '''python manage.py migrate'''
