# LizardFS Docker Cluster

This is a sample configuration of a multiple node LizardFS cluster on Docker using Ubuntu 16.04 LTS. It consists of a master server with a management GUI, a shadow server, 3 chunkservers and one client machine. After a successful installation you have a fully working LizardFS cluster to play with its amazing features.

## Cluster configurations

**File docker-compose.yml**

- master **172.20.0.2**
- management web interface  [http://172.20.0.2:9425](http://172.20.0.2:9425)
- shadow **172.20.0.3**
- chunkserver-01 **172.20.0.11**
- chunkserver-02 **172.20.0.12**
- chunkserver-03 **172.20.0.13**
- client **172.168.20.0.5**

## Setup

Install Docker with composer from [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

Clone LizardFS docker config files:

```
git clone https://github.com/lizardfs/lizardfs-docker-cluster
```

### Start LizardFS cluster:

Go to repo directory:

```
cd lizardfs-docker-cluster
```

Build and run in background:

```
docker-compose build
docker-compose up -d
```

"-d" is for running Docker nodes in background, so Docker console output is invisible.

Check if instances are running with:

```
docker ps
```
You should have 1 master, 3 chunkservers and 1 client running.
```

### Stop the cluster
`docker-compose stop`

### Restart the stopped cluster
`docker-compose start`

### Remove containers
`docker-compose rm -f`
```

*based on moosefs-docker-cluster (https://github.com/moosefs/moosefs-docker-cluster/)*

