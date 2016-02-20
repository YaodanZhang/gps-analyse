# GPS Path Dashboard

## How to set up work station

### Set up virtual machine

1) Install Vagrant and VirtualBox

2) Initialize VM config

```
vagrant init ubuntu/trusty64;
```

3) Change the configuration in file ```Vagrantfile``` to set up network

4) Start up virtual machine

```
vagrant up --provider virtualbox
```

### Provision work station

1) Change the ip address and ssh method in hosts/gps

2) Check & change the configurations in each role. (defaults/main.yml)

3) Run the following script

```
ansible-playbook -i hosts/gps gps.yml
```

## How to use

### 1. Prepare data

Put some gps data into the Elasticsearch. The default index (```{{elastic_index}}```) and type (```{{elastic_type}}```) are set in playbooks/roles/config/defaults/main.yml.

The following is an example:

1) Create index for daily logs

```
curl -XPUT localhost:9200/soda-20160220
```

2) Change the setting of this index.

```
curl -XPUT localhost:9200/soda-20160220/_mapping/gps -d '{
    "gps": {
        "properties": {
            "location": {
                "type": "geo_point"
            },
            "timestamp": {
                "type": "date",
                "format": "strict_date_optional_time||epoch_millis"
            },
            "vin": {
                "type": "string"
            }
        }
    }
}'
```

3) Add data into it

```
curl -XPUT localhost:9200/soda-20160220/gps/1 -d '{
    "vin": "A0001",
    "timestamp": "2016-02-19T16:00:04.045+08:00",
    "location": {
        "lat": 30.59394691620327,
        "lon": 104.06529086129288
    }
}'
```

### 2. Open Dashboard

Open Kibana dashboard, click open icon and you can find the pre-set gps heat map dashboard named as "gps".

It's easy to select vehicle/time range in it. Please refer Kibana tutorial for usage:
- https://www.elastic.co/guide/en/kibana/current/index.html
- https://www.elastic.co/webinars/getting-started-with-kibana?baymax=rtp&elektra=docs&iesrc=ctr

## License

BSD

## Author Information

@YaodanZhang
