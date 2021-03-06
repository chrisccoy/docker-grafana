# Grafana Docker image

This project builds a Docker image with the latest master build of Grafana.

## Running your Grafana container

Start your container binding the external port `3000`.

```
docker run -d --name=grafana -p 3000:3000 appcelerator/grafana
```

Try it out, default admin user is admin/changeme.

## Configuring your Grafana container

All options defined in conf/grafana.ini can be overriden using environment
variables, for example:

```
docker run \
  -d \
  -p 3000:3000 \
  --name=grafana \
  -e "GRAFANA_PASS=changeme" \
  -e "INFLUXDB_HOST=influxdb" \
  -e "INFLUXDB_USER=grafana" \
  -e "INFLUXDB_PASS=changeme" \
  appcelerator/grafana
```

## Grafana container with persistent storage (recommended)

```
# create /var/lib/grafana as persistent volume storage
docker run -d -v /var/lib/grafana --name grafana-storage busybox:latest

# start grafana
docker run \
  -d \
  -p 3000:3000 \
  --name=grafana \
  --volumes-from grafana-storage \
  appcelerator/grafana
```

## Running specific version of Grafana

```
# specify right tag, e.g. 2.6.0 - see Docker Hub for available tags
docker run \
  -d \
  -p 3000:3000 \
  --name grafana \
  appcelerator/grafana:2.6.0
```

## Official Grafana with unofficial plugins (community project):

Unofficial plugins/datasources: Zabbix, DalmatinerDB, Ambari, Atsd, Bosun,
Cloudera Manager, Druid, Chnocchi, PRTG, ...

```
# create /var/lib/grafana as persistent volume storage
docker run -d -v /var/lib/grafana --name grafana-xxl-storage busybox:latest

# start grafana-xxl
docker run \
  -d \
  -p 3000:3000 \
  --name grafana-xxl \
  --volumes-from grafana-xxl-storage \
  monitoringartist/grafana-xxl
```

Visit [Grafana XXL project](https://github.com/monitoringartist/grafana-xxl)
for more details.
