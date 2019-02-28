# Running the Visualisation Dashboard form Sources (To be reviewed and completed by Bitergia)

All the documentation below describes how to setup and run the different components
related to the Web Dashboards.


## Install steps for the different components

### Install GrimoireLab Python Env

The data processing is done with GrimoireLab python platform.

A virtual env in Python is used to install the tools needed.

In Debian/Ubuntu you need to execute:

`sudo apt-get install python3-venv`

To create the python virtualenv and activate it:

```
mkdir ~/venvs
python3 -m venv ~/venvs/crossminer
source ~/venvs/crossminer/bin/activate
pip3 install grimoire-elk
```

### Install Elasticsearch and Kibana

An Elasticsearch and Kibana services are needed. docker-compose can be used to start them.

Elasticsearch needs this config:

`sudo sh -c "echo 262144 > /proc/sys/vm/max_map_count"`

