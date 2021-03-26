# mqtt-cowboy-crash

## What's this?

A simple demo of how rabbitmq-server will log a crash when using MQTT over websockets.

## Instructions

### Setup rabbitmq-server

* Install a clean rabbitmq-server
* Enable MQTT and Web MQTT plugin

`rabbitmq-plugins enable rabbitmq_mqtt rabbitmq_web_mqtt`

* Add vhost to use for MQTT

`rabbitmqctl add_vhost mqtt-vhost`

* Add mqtt user

`rabbitmqctl add_user mqtt mqtt`

* Make user mqtt a management user

`rabbitmqctl set_user_tags mqtt management`

* Set permissions

`rabbitmqctl set_permissions -p mqtt-vhost mqtt '.*' '.*' '.*'`

* Set topic permissions (only read permissions)

`rabbitmqctl set_topic_permissions -p mqtt-vhost mqtt amq.topic '' '.*'`

* Add config to enable anonymous mqtt login:

```
mqtt.default_user    = mqtt
mqtt.default_pass    = mqtt
mqtt.allow_anonymous = true
mqtt.vhost           = mqtt-vhost
mqtt.exchange        = amq.topic
```

* Restart rabbitmq-server

### Run demo webapp

```
npm install
npm start
```

Open http://localhost:8080 in a browser and follow the instructions.
If port `8080` is unavailable, `http-server` will pick another port to expose the demo on.
