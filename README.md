# labfinalDevops

1. Create a virtual machine
   - should know
2. Install Nginx (not using Docker) to the virtual machine and show the default home page.
    ```
    sudo apt update
    ```
   ```
   sudo apt install nginx -y
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```
    ```
   curl localhost
    ```
3. Edit the HTML to show the new index.html in the Nginx
   ```
   sudo nano /var/www/html/index.nginx-debian.html
   ```

   Save (Ctrl+O, Enter, Ctrl+X), then reload Nginx:
   ```
   sudo systemctl reload nginx
   ```
4. Install Docker in the Virtual Machine, and Call the hello-world Image to Run
   ```
   sudo apt install docker.io -y
   sudo systemctl start docker
   sudo systemctl enable docker
   ```
   ```
   sudo usermod -aG docker $USER
   ```
   ```
   newgrp docker
   ```
   ```
   docker run hello-world
   ```
5. Run the Docker Image Nginx and Show the Default Page
   ```
   docker run -d -p 81:80 nginx
   ```
   ```
   curl localhost:81
   ```
6. Proctor Sends HTML File, Create a New Image to Show It, Run Container
    ```
   wget http://example.com/custom.html  # If given a URL
    ```
   ```
   nano custom.html
   # Paste the content, Ctrl+O, Enter, Ctrl+X to save
   ```
   ```
   nano Dockerfile
   ```
   ```
   FROM nginx:latest
   COPY custom.html /usr/share/nginx/html/index.html
   ```
   ```
   docker build -t my-nginx-image .
   ```
   ```
   docker run -d -p 82:80 my-nginx-image
   ```
   ```
   curl localhost:82
   ```
7. Push the Image You Created to Your Docker Hub
   ```
   docker login
   # Enter username/password
    ```
    ```
   docker tag my-nginx-image awesomekid/my-nginx-image:latest
    ```
   ```
   docker push awesomekid/my-nginx-image:latest
   ```
8. Map the Volume of Your Container to Show the Website from Question 3
   ```
   sudo cp /var/www/html/index.nginx-debian.html /var/www/html/index.html
   sudo chmod -R 755 /var/www/html
   docker run -d -p 83:80 -v /var/www/html:/usr/share/nginx/html nginx
   ```
    ```
   curl localhost:83   
    ```
9. Proctor Provides docker-compose.yml, Run It, Show Output
   test docker-compose.yml
   ```
   nano ~/docker-compose.yml
   ```
   ```
   version: '3'
   services:
   web:
    image: nginx:latest
    ports:
      - "84:80"
    volumes:
      - ./html:/usr/share/nginx/html
   redis:
    image: redis:alpine
    ports:
      - "6379:6379"
   ```
   ```
   mkdir ~/html
   nano ~/html/index.html
   ```
   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>Proctor Test</title>
   </head>
   <body>
       <h1>Proctor’s Docker Compose Test</h1>
       <p>This is running via docker-compose.yml!</p>
   </body>
   </html>
   ```
   ```
   sudo apt install docker-compose -y
   ```
   ```
   docker-compose up -d
   ```
   ```
   curl localhost:84
   ```
10. Create a new HTML file in the VM, Write your docker-compose.yml to run your image, and map the volume to your new HTML file, and show the output.

   ```
   mkdir ~/question10
   cd ~/question10
   ```
   ```
   nano new-page.html
   ```   
   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>Question 10 Test</title>
   </head>
   <body>
       <h1>My New Docker Compose Page</h1>
       <p>This is for Question 10, running my custom image!</p>
   </body>
   </html>
   ```
   ```
   nano docker-compose.yml
   ```
   ```
   version: '3'
   services:
      web:
       image: my-nginx-image
       ports:
         - "85:80"
       volumes:
         - ./new-page.html:/usr/share/nginx/html/index.html
   ```
   ```
   docker-compose up -d
   ```
   ```
   curl localhost:85
   ```

   
