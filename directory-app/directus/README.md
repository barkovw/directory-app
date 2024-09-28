https://docs.directus.io/self-hosted/quickstart.html

Create a Docker Compose File
Create a new empty folder on your Desktop called directus. Within this new folder, create the three empty folders database, uploads, and extensions.

Open a text editor such as Visual Studio Code, nano, Vim, TextEdit, or Notepad.

Copy and paste the following and save the file as docker-compose.yml:

yaml
version: "3"
services:
  directus:
    image: directus/directus:11.1.0
    ports:
      - 8055:8055
    volumes:
      - ./database:/directus/database
      - ./uploads:/directus/uploads
      - ./extensions:/directus/extensions
    environment:
      SECRET: "replace-with-secure-random-value"
      ADMIN_EMAIL: "admin@example.com"
      ADMIN_PASSWORD: "d1r3ctu5"
      DB_CLIENT: "sqlite3"
      DB_FILENAME: "/directus/database/data.db"
      WEBSOCKETS_ENABLED: "true"
Save the file. Let's step through it:

This file defines a single Docker container that will use the specified version of the directus/directus image.
The ports list maps internal port 8055 is made available to our machine using the same port number, meaning we can access it from our computer's browser.
Thevolumes section maps internal database, uploads and extensions data to our local file system alongside the docker-compose.yml - meaning data is stored and persisted outside of Docker containers.
The environment section contains any configuration variables we wish to set.
SECRET is required and should be a secure random value, it's used to sign tokens.
ADMIN_EMAIL and ADMIN_PASSWORD is the initial admin user credentials on first launch.
DB_CLIENT and DB_FILENAME are defining the connection to your database.
WEBSOCKETS_ENABLED is not required, but enables Directus Realtime.
The volumes section is not required, but without this, our database and file uploads will be destroyed when the Docker container stops running. The default database is SQLite - a self-contained server-less database that stores data to a file.

Run Directus
macOS/LinuxWindows
Open the Terminal and run the following commands one line at a time:


cd Desktop/directus
docker compose up
Directus should now be available at http://localhost:8055 or http://127.0.0.1:8055.

________________________________

https://www.civo.com/learn/fixing-networking-for-docker