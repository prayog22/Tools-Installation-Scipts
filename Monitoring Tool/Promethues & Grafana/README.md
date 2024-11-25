# Getting started with Grafana and Prometheus
## Step 1. Install Grafana and build your first dashboard
>  To install the latest OSS release:
#
    sudo apt-get install -y apt-transport-https software-properties-common wget
# 
    sudo mkdir -p /etc/apt/keyrings/
>  Add this repository for stable releases

# 
    wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
#
    echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
# 
    echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
> Updates the list of available packages
# 
    sudo apt-get update
#
    sudo apt-get install grafana -y
>  Start the server with systemd
#
    sudo systemctl daemon-reload
#
    sudo systemctl start grafana-server
#
    sudo systemctl status grafana-server
> Configure the Grafana server to start at boot:
#
    sudo systemctl enable grafana-server.service
### Open your web browser and go to http://localhost:3000/.

## step 2 : Download Prometheus and node_exporter

> Update the system
#
    sudo apt update 
> we need to create the configuration and data directories for Prometheus.
> run the command:
#
    sudo mkdir -p /etc/prometheus
> For the data directory, execute:
#
    sudo mkdir -p /var/lib/prometheus
> Once the directories are created, grab the compressed installation file:
#
    wget https://github.com/prometheus/prometheus/releases/download/v2.53.1/prometheus-2.53.1.linux-amd64.tar.gz
> Once downloaded, extract the tarball file.
#
    tar -xvf prometheus-2.53.1.linux-amd64.tar.gz
> Then navigate to the Prometheus folder.
# 
    cd prometheus-2.53.1.linux-amd64.tar.gz
> Move the  prometheus and promtool binary files to /usr/local/bin/ folder.
#
    sudo mv prometheus promtool /usr/local/bin/
> Move console files in console directory and library files in the console_libraries  directory to /etc/prometheus/ 
#
    sudo mv consoles/ console_libraries/ /etc/prometheus/
> Move the prometheus.yml template configuration file to the  /etc/prometheus/ directory.
#
    sudo mv prometheus.yml /etc/prometheus/prometheus.yml
> To check the version of Prometheus installed
#
    prometheus --version
## Step 3: Configure System group and user
> To create a prometheus group execute the command:
#
    sudo groupadd --system prometheus
> Create prometheus user and assign it to the just-created prometheus group.
#
    sudo useradd -s /sbin/nologin --system -g prometheus prometheus
> Configure the directory ownership and permissions as follows.
#
    sudo chown -R prometheus:prometheus /etc/prometheus/ /var/lib/prometheus/
# 
    sudo chmod -R 775 /etc/prometheus/ /var/lib/prometheus/
## Step 4: Create a systemd file for Prometheus
#
    sudo nano /etc/systemd/system/prometheus.service
> Paste the following lines of code.
#
    [Unit]
    Description=Prometheus
    Wants=network-online.target
    After=network-online.target

    [Service]
    User=prometheus
    Group=prometheus
    Restart=always
    Type=simple
    ExecStart=/usr/local/bin/prometheus \
     --config.file=/etc/prometheus/prometheus.yml \
     --storage.tsdb.path=/var/lib/prometheus/ \
     --web.console.templates=/etc/prometheus/consoles \
     --web.console.libraries=/etc/prometheus/console_libraries \
     --web.listen-address=0.0.0.0:9090

    [Install]
    WantedBy=multi-user.target
> Save the changes and exit the systemd file.
* Then proceed and start the Prometheus service.
#
    sudo systemctl start prometheus
* Enable the Prometheus service to run at startup. Therefore invoke the command:
#
    sudo systemctl enable prometheus
* Then confirm the status of the Prometheus service.
#
    sudo systemctl status prometheus

### Launch your browser and visit your server's IP address followed by port 9090.

# Thank You 