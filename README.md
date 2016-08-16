# Docker Image with StatsD, InfluxDB and Grafana

:facepunch: Battle-tested


## Versions

* StatsD:   0.8.0
* InfluxDB: 0.13
* Grafana:  3.1.1

## Quick Start

To start the container the first time launch:

```sh
docker run -d \
  --name grafana \
  -p 3003:9000 \
  -p 3004:8083 \
  -p 8086:8086 \
  -p 22022:22 \
  -p 8125:8125/udp \
  advantageous/grafana:latest:latest
```

You can replace `latest` with the desired version listed in changelog file.

To stop the container launch:

```sh
docker stop grafana
```

To start the container again launch:

```sh
docker start grafana
```

## Mapped Ports

```
Host		Container		Service

3003		9000			grafana
8086		8086			influxdb
3004		8083			influxdb-admin
8125		8125			statsd
22022		22				sshd
```
## SSH

```sh
ssh root@localhost -p 22022
```
Password: root

## Grafana

Open <http://localhost:3003>

```
Username: root
Password: root
```

### Add data source on Grafana

1. Open `Data Sources` from left side menu, then click on `Add data source`
2. Choose a `name` for the source and flag it as `Default`
3. Choose `InfluxDB` as `type`
4. Choose `direct` as `access`
5. Fill remaining fields as follows and click on `Add` without altering other fields

```
Url: http://localhost:8086
Database:	datasource
User: datasource
Password:	datasource
```

Now you are ready to add your first dashboard and launch some query on database.

## InfluxDB

### Web Interface

Open <http://localhost:3004>

```
Username: root
Password: root
Port: 8086
```

### InfluxDB Shell (CLI)

1. Establish a ssh connection with the container
2. Launch `influx` to open InfluxDB Shell (CLI)

## Build

```
docker build -t advantageous/grafana:v1   .
docker build -t advantageous/grafana:latest  .
```

## Push
```
docker push  advantageous/grafana
```
