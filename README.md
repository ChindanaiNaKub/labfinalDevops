# labfinalDevops

1. Create a virtual machine
   - should know
2. Install Nginx (not using Docker) to the virtual machine and show the default home page.
   - sudo apt update
   - sudo apt install nginx
   - sudo systemctl enable nginx
   - sudo systemctl start nginx
4. Edit the HTML to show the new index.html in the Nginx
   - cd /var/www/html
   - sudo nano index.html
   - add anything to index.html ( press CTRL + X, Y and Enter to save )
   - sudo chmod 644 index.html
   - sudo chown www-data:www-data index.html
   - sudo systemctl restart nginx
5.  Install Docker in the virtual machine, and call the hello-world image to run
   - soon
6. 
