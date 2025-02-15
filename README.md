Task - I
Deploy a basic web application using any platform or local server, using open-source tools and libraries.

Create or use a pre-existing simple web application: You may build a web application from scratch or use a pre-existing app. This app can be in any programming language (e.g., Python, Node.js, PHP, Ruby, etc.) and should be simple but functional (e.g., a “To-Do” list app or a basic portfolio page).

Deploy the web application: Deploy the application on a public server. You may use any publicly accessible server such as a free-tier instance from a cloud provider (AWS Free Tier, Google Cloud Free Tier, or Azure Free Tier), DigitalOcean, or a similar platform. Ensure the application is accessible via a web browser: Provide the public URL where the application can be accessed. Ensure that the app is publicly available and functional.

Solution
Launched an Ubuntu VM on GCP
SSH in to the VM
Switch to root user 
sudo su 

Update the packages
apt update && upgrade -y


Install python3 and pip
apt install python3 python3-pip -y

Install Flask
pip3 install flask


Verify installation
python3 --version
pip3 --version
python3 -m flask --version


Create a folder pythonapp in the home directory
In the pythonapp folder, create file app.py
from flask import Flask, render_template

app = Flask(__name__, template_folder="templates", static_folder="static") 

@app.route("/") 
def index(): 
        return render_template("index.html") 

if __name__ == "__main__": 
        app.run(host="0.0.0.0", port=5000, debug=True)


Also create two folders templates and static folder
In the templates folder, create a index.html file
In the static folder, create style.css and an image file
Setup systemd service to start the app automatically on reboot 
Create a service file for add script
vi /etc/systemd/system/myapp.service


[Unit]
Description=My Python Application
After=network.target

[Service]
ExecStart=/usr/bin/python3 /home/pythonapp/app.py
WorkingDirectory=/home/pythonapp
Restart=always
User=abhilashgopal2k
StandardOutput=append:/var/log/myapp.log
StandardError=append:/var/log/myapp.err

[Install]
WantedBy=multi-user.target


Enable and start the service 
systemctl daemon-reload
systemctl enable myapp
systemctl start myapp
systemctl status myapp


View the hosted service 
Search http://35.209.197.93:5000/ on browser
