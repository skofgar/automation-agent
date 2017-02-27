# About this repository
This repository contains a Dockerfile that simplifies the creation of a docker image for the deployment of the MongoDB MMS Automation Agent.
In order to start this image some required flags need to be passed along (baseUrl, groupId and apiKey), please review the instructions below.

For more detailed installation steps please review [MMS Automation Agent Installation Guide](https://docs.cloudmanager.mongodb.com/tutorial/nav/install-automation-agent/).


# Run
In order to run a container three flags need to be provided. The three flags are:
 * `--mmsBaseUrl`
 * `--mmsGroupId`
 * `--mmsApiKey`

These three inputs can be retrieved from the [MongoDB Ops Manager](https://docs.opsmanager.mongodb.com/current/) under `Settings > Group Settings > GroupID and Agent API Key` ([docs](https://docs.opsmanager.mongodb.com/current/reference/automation-agent/#asetting.mmsGroupId)).

# Example
This is an example how an image could be run in it's own network.

## Create network

```
docker network create --subnet=172.18.0.0/16 mongoNet
```

## Create image
_Note: Before this image can be added [MongoDB OPS Manager](https://www.mongodb.com/products/ops-manager) needs to be set up._

```
docker run -d --name testAgent --net mongoNet --ip 172.18.0.11 -p 27010:27000 --privileged skofgar/automation-agent --mmsBaseUrl=http://172.18.0.2:8080 --mmsGroupId=1234567890 --mmsApiKey=12345567890
```

# Credits

This Dockerfile is inspired by https://github.com/mcascallares/mongodb-automation
