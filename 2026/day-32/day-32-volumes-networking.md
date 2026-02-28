## Task 1: The Problem

# Run a Postgres or MySQL container
# Create some data inside it (a table, a few rows — anything)
# Stop and remove the container
# Run a new one — is your data still there?

<img width="361" height="283" alt="image" src="https://github.com/user-attachments/assets/ac81d377-36c6-46ed-abee-176135be59aa" />
My database: sql_imp_data was deleted as the cotainer was removed.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Named Volumes

# Create a named volume
<img width="893" height="162" alt="image" src="https://github.com/user-attachments/assets/0d4ecfe1-0c0e-487c-ad1a-570fdc816679" />

# Run the same database container, but this time attach the volume to it
<img width="1530" height="58" alt="image" src="https://github.com/user-attachments/assets/2ee1bbec-898c-46ca-b258-56c319cd74c0" />

# Add some data, stop and remove the container
<img width="466" height="379" alt="image" src="https://github.com/user-attachments/assets/1e3f8d50-c924-420f-a393-667066e91963" />
<img width="1069" height="94" alt="image" src="https://github.com/user-attachments/assets/3e8ebd7e-4977-4370-a9b5-c7cec69a9246" />

# Run a brand new container with the same volume
<img width="1563" height="64" alt="image" src="https://github.com/user-attachments/assets/cb8d5669-9544-47d6-b73f-4c7eafbb1370" />

# Is the data still there?
<img width="899" height="733" alt="image" src="https://github.com/user-attachments/assets/f00f564b-9129-45c3-8965-8181261fe914" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Bind Mounts

# Create a folder on your host machine with an index.html file
<img width="805" height="89" alt="image" src="https://github.com/user-attachments/assets/14ae1489-1e98-4dad-8651-5f1e39120b21" />

# Run an Nginx container and bind mount your folder to the Nginx web directory
<img width="1755" height="392" alt="image" src="https://github.com/user-attachments/assets/bfe3eb9a-47ec-4cf6-bde3-555adcff026b" />

# Access the page in your browser
Accessible but blank as indix.html was kept blank.

# Edit the index.html on your host — refresh the browser
Added lined to index.html.
<img width="320" height="199" alt="image" src="https://github.com/user-attachments/assets/1ee15c79-c99c-4394-8a39-82a808a0e5ff" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Docker Networking Basics

# List all Docker networks on your machine
<img width="857" height="140" alt="image" src="https://github.com/user-attachments/assets/4bdc0fe0-a9ca-4e9d-b312-f7d925f3d8e9" />

# Inspect the default bridge network
<img width="954" height="465" alt="image" src="https://github.com/user-attachments/assets/ae65979a-bbc8-48fd-834c-8eb6b800e85f" />
<img width="1020" height="375" alt="image" src="https://github.com/user-attachments/assets/0dc3f970-6451-46ad-b613-ab39b0fb4b39" />

# Run two containers on the default bridge — can they ping each other by name?
<img width="446" height="60" alt="image" src="https://github.com/user-attachments/assets/67882ffa-7d80-4a46-8210-f6a5711f7f5b" />
ping by container name doesn't work as there is no DNS server.

# Run two containers on the default bridge — can they ping each other by IP?
<img width="657" height="165" alt="image" src="https://github.com/user-attachments/assets/34e1cda3-bf8b-4c4b-bf3c-529956f6656a" />

Ping to other container ip address works.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Custom Networks











