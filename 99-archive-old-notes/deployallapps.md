GLOBAL / INITIAL (run once per host)

(Use apt for Debian/Ubuntu, replace with yum/dnf on RHEL/CentOS)

# update + basics
sudo apt update -y
sudo apt install -y git curl wget unzip build-essential

# Java build tools
sudo apt install -y openjdk-17-jdk maven   # or openjdk-11-jdk if needed
java -version
mvn -v

# Node
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
node -v; npm -v

# Python
sudo apt install -y python3 python3-venv python3-pip
python3 --version; pip3 --version

# Docker (optional)
sudo apt install -y docker.io
sudo systemctl enable --now docker

# pm2 and gunicorn global installers (optional)
sudo npm install -g pm2
sudo pip3 install gunicorn

COMMON VERIFY & TROUBLESHOOT COMMANDS (use all the time)
# processes
ps -ef | grep -E "java|node|gunicorn|pm2|nginx" | grep -v grep

# listening ports
sudo ss -tulnp

# check a specific port
sudo ss -tulnp | grep :5000

# view logs
# systemd
sudo journalctl -u myservice -f
# files
tail -n 200 /path/to/logfile.log
# tomcat
sudo tail -f /opt/apache-tomcat-11/logs/catalina.out
# pm2
pm2 logs my-node-app --lines 200

A. JAVA (Spring Boot or simple Java app)
1) Clone & prepare
cd /opt
sudo git clone https://github.com/your/repo-java.git my-java-app
cd my-java-app

2) Install dependencies & build (Maven)
mvn clean package -DskipTests
# artifact: target/myapp-<version>.jar  (or .war)
ls target

3) Run locally (dev quick test)
# run jar (dev)
java -jar target/myapp-1.0.jar
# It prints: "Started Application in ... Listening on port: 8080" (default)
# If you need to run in background (dev)
nohup java -jar target/myapp-1.0.jar > /var/log/myapp.out 2>&1 &

4) Production (systemd) — single instance

Create /etc/systemd/system/myjava.service:

[Unit]
Description=My Java App
After=network.target

[Service]
User=appuser
WorkingDirectory=/opt/my-java-app
ExecStart=/usr/bin/java -jar /opt/my-java-app/target/myapp-1.0.jar
Restart=on-failure
Environment=JAVA_OPTS=-Xms512m -Xmx1g

[Install]
WantedBy=multi-user.target


Then:

sudo systemctl daemon-reload
sudo systemctl enable --now myjava
sudo journalctl -u myjava -f

5) Production (scale / multiple instances)

Two options:

a) Multiple JVMs on different ports, fronted by Nginx (simple)
Run two instances on port 8081 and 8082:

nohup java -jar target/myapp-1.0.jar --server.port=8081 > /var/log/myapp-8081.log 2>&1 &
nohup java -jar target/myapp-1.0.jar --server.port=8082 > /var/log/myapp-8082.log 2>&1 &


Nginx load-balance config (example /etc/nginx/conf.d/myjava.conf):

upstream myjava {
    server 127.0.0.1:8081;
    server 127.0.0.1:8082;
}
server {
    listen 80;
    server_name myjava.example;
    location / { proxy_pass http://myjava; proxy_set_header Host $host; proxy_set_header X-Real-IP $remote_addr; }
}


sudo nginx -t && sudo systemctl reload nginx

b) Docker + multiple replicas (recommended in real infra):
Build Dockerfile, push image, run multiple containers or use Kubernetes.

6) WAR on Tomcat (if used)
# copy WAR
sudo cp target/myapp.war /opt/apache-tomcat-11/webapps/
# restart tomcat
sudo /opt/apache-tomcat-11/bin/shutdown.sh
sudo /opt/apache-tomcat-11/bin/startup.sh
# logs
sudo tail -f /opt/apache-tomcat-11/logs/catalina.out

7) Change port

Spring Boot: edit src/main/resources/application.properties:

server.port=9090


or override at runtime:

java -Dserver.port=9090 -jar target/myapp-1.0.jar


Tomcat: edit /opt/apache-tomcat-11/conf/server.xml connector port and restart.

8) Stop / restart / status
sudo systemctl stop myjava
sudo systemctl restart myjava
sudo systemctl status myjava
# or kill specific PID
ps -ef | grep myapp
sudo kill <PID>

B. NODE.JS (Express / general)
1) Clone & prepare
cd /opt
sudo git clone https://github.com/your/repo-node.git my-node-app
cd my-node-app

2) Install dependencies
npm ci          # preferred if package-lock.json exists
# or
npm install

3) Run locally (dev)
node index.js
# or if package.json has script:
npm start


Default dev port usually 3000 or defined in code/env. To run background for quick test:

nohup node index.js > /var/log/my-node-app.out 2>&1 &

4) Production — PM2 (process manager)
sudo npm install -g pm2   # one-time
# start in cluster mode (4 instances) - auto-balance across CPU cores
pm2 start index.js -i 4 --name my-node-app
pm2 save                  # save process list
pm2 startup systemd       # follow printed command (run it with sudo)
# view
pm2 list
pm2 logs my-node-app

5) Production — Docker

Dockerfile:

FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]


Build & run:

docker build -t mynode:1.0 .
docker run -d --name mynode -p 3000:3000 mynode:1.0

6) Change port

Best practice: use environment variable PORT. Example:

const port = process.env.PORT || 3000;
app.listen(port, ...);


Start with different port:

PORT=9090 pm2 restart my-node-app
# or
docker run -d -p 9090:3000 -e PORT=3000 mynode:1.0

7) Stop / restart
pm2 stop my-node-app
pm2 restart my-node-app
pm2 delete my-node-app
# manual
ps -ef | grep node
sudo kill <PID>

C. PYTHON (Flask example)
1) Clone & prepare
cd /opt
sudo git clone https://github.com/mmumshad/simple-webapp-flask.git simple-webapp-flask
cd simple-webapp-flask

2) Create virtualenv & install deps
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
deactivate

3) Run locally (dev)
python3 app.py
# default Flask port 5000 (or defined in app.run)

4) Production — Gunicorn + systemd

Start manually:

cd /opt/simple-webapp-flask
./venv/bin/gunicorn app:app -w 3 -b 127.0.0.1:8000


Create /etc/systemd/system/simple-flask.service:

[Unit]
Description=Gunicorn Flask App
After=network.target

[Service]
User=webapp
Group=www-data
WorkingDirectory=/opt/simple-webapp-flask
Environment="PATH=/opt/simple-webapp-flask/venv/bin"
ExecStart=/opt/simple-webapp-flask/venv/bin/gunicorn --workers 3 --bind 127.0.0.1:8000 app:app

[Install]
WantedBy=multi-user.target


Then:

sudo systemctl daemon-reload
sudo systemctl enable --now simple-flask
sudo journalctl -u simple-flask -f

5) Change port

Edit ExecStart bind 127.0.0.1:8000 → 0.0.0.0:9090 or :9090 then sudo systemctl restart simple-flask

Or start gunicorn with different bind:

./venv/bin/gunicorn app:app -w 4 -b 0.0.0.0:9090 --daemon

6) Scale workers

Gunicorn scale with worker count:

# run 4 workers
./venv/bin/gunicorn app:app -w 4 -b 127.0.0.1:8000

7) Stop / restart / logs
sudo systemctl stop simple-flask
sudo systemctl restart simple-flask
sudo journalctl -u simple-flask -n 200
# if run with nohup
tail -n 200 /home/thor/nohup.out

D. NGINX reverse proxy & load balancing (common to all)

Example to reverse-proxy to a single backend (Gunicorn/Node/Java):

server {
    listen 80;
    server_name myapp.example;

    location / {
        proxy_pass http://127.0.0.1:8000;           # backend
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}


For load balancing multiple app instances:

upstream myapp {
    server 127.0.0.1:8081;
    server 127.0.0.1:8082;
}
server {
    listen 80;
    location / { proxy_pass http://myapp; }
}


Reload:

sudo nginx -t && sudo systemctl reload nginx

E. Quick common tasks (copy/paste)
# clone repo
cd /opt
sudo git clone <repo_url> my-app
cd my-app

# Java build
mvn clean package -DskipTests

# Node install
npm ci

# Python venv install
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
deactivate

# run gunicorn in background
./venv/bin/gunicorn app:app -w 3 -b 0.0.0.0:8000 --daemon

# pm2 start 4 instances
pm2 start index.js -i 4 --name my-node-app

# check listening ports
sudo ss -tulnp

# check process
ps -ef | grep -E "gunicorn|node|java" | grep -v grep

# see logs (systemd)
sudo journalctl -u myservice -f

# tail files
tail -n 200 /var/log/myapp.out

# change port quick with sed (lab quick fix)
sudo sed -i 's/8080/9090/g' path/to/file

# stop all pm2 apps
pm2 stop all
pm2 delete all