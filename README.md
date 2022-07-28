# Install Apache Airflow Standalone Ubuntu 
## Environment
* Ubuntu server 18.04.2 LTS (manhnk9@172.17.80.26, password: 1)
* Python 3.6.9

1. Install pip3
```
sudo apt install python3-pip
```
2. Uninstall gunicorn (avoid mismatch version)
* Check if gunicorn have been installed
```
pip3 list | grep gunicord
```
* If existed
```
pip3 uninstall gunicorn
```
3. Install Airlow
```
sudo pip3 install apache-airflow
```
4. Set up Airflow as a systemd service
* airflow-webserver.service (default port: 8080)
```
sudo vi /etc/systemd/system/airflow-webserver.service
```
```
[Unit]
Description=Airflow webserver daemon
After=network.target
[Service]
EnvironmentFile=/etc/environment
User=manhnk9
Type=simple
ExecStart= /usr/local/bin/airflow webserver
Restart=on-failure
RestartSec=5s
PrivateTmp=true
[Install]
WantedBy=multi-user.target
```
```
chmod 664 /etc/systemd/system/airflow-webserver.service
systemctl enable airflow-webserver.service
systemctl start airflow-webserver
```
Every time you make any changes airflow-webserver.service file
```
systemctl daemon-reload
```
* airflow-scheduler.service
```
sudo vi /etc/systemd/system/airflow-scheduler.service
```
```
Description=Airflow scheduler daemon
After=network.target
Description=Airflow scheduler daemon
After=network.target
[Service]
EnvironmentFile=/etc/environment
User=manhnk9
Type=simple
ExecStart= /usr/local/bin/airflow scheduler
Restart=on-failure
RestartSec=5s
PrivateTmp=true
[Install]
WantedBy=multi-user.target
```
```
chmod 664 /etc/systemd/system/airflow-scheduler.service
systemctl enable airflow-scheduler.service
systemctl start airflow-webserver
```
Every time you make any changes airflow-scheduler.service file
```
systemctl daemon-reload
```

## Add admin user
```
airflow users create \
    --username admin \
    --firstname Peter \
    --lastname Parker \
    --role Admin \
    --email spiderman@superhero.org
```

