## 1. Download Docker PostgreSQL Image
I have Docker installed on my MAC, so pull the Docker PostgreSQL Image directly by:

**docker pull postgres**

Create a local folder and mount it as a data volume for our running container to store all the database files in a known location:

**mkdir ${HOME}/postgres-data/**

Then set up a PostgreSQL docker container by:

**docker run --name postgresql -e POSTGRES_USER=myusername -e POSTGRES_PASSWORD=mypassword -p 5432:5432 -v ${HOME}/postgres-data/:/var/lib/postgresql/data -d postgres**

Then we have a running PostgreSQL instance.

## 2. Install PGAdmin on Docker
Next we are going to set up DB admin tool pgAdmin. Get the image and run the instance of the image with the following commands:

**docker pull dpage/pgadmin4:latest**

**docker run --name my-pgadmin -p 82:80 -e 'PGADMIN_DEFAULT_EMAIL=yuezhou896@gmail.com' -e 'PGADMIN_DEFAULT_PASSWORD=postgresmaster'-d dpage/pgadmin4**

## 3. Accessing the PostgreSQL from the pgAdmin tool
Look for the IP address of the PostgreSQL container on our host by:

**docker inspect postgresql -f "{{json .NetworkSettings.Networks }}"**

Then we log in into pgAdmin web and add our PostgreSQL as a new server.

## 4. Create a new table and import csv file
Create a new table based on data schema:

**CREATE TABLE golfdata
(id serial,
height NUMERIC,
ball_speed NUMERIC,
launch_angle NUMERIC,
landing_angle NUMERIC,
hang_time NUMERIC,
curve NUMERIC,
flat_carry NUMERIC,
side_angle NUMERIC
);**

Then use import/export on the web to import local csv file into DB.

Check the table using:

**select * from golfdata**
