# WebsphereMQ Testing

Project tests interlok-webspheremq features

## What it does

This project contains a single instance of Interlok that will attempt to connect to a locally running WebpshereMQ instance.  It is assumed WebsphereMQ can be contacted on tcp://localhost:1414.  Once started a single polling trigger will produce a message every 10 seconds and send that message to a queue named "DEV.QUEUE.1".  
This channel maintains a transacted JMS session, meaning after every message has been consumed and moved from the first queue to the second the session will 'commit' or 'rollback' should there be a failure.

A second channel which is set to not start by default will provide the same messaging bridge but without the transacted session.  You'll need to log into the UI to start this channel manually.

![wmq diagram](/wmq.png "wmq diagram")
 
## Getting started

Please note this project uses a licensed component; therefore you will need an Interlok license.
Once obtained create a file "src/main/interlok/config/license.properties" that contains your license key.

* `./gradlew clean build`
* `(cd ./build/distribution && java -jar lib/interlok-boot.jar)`

### docker

You can run websphereMQ in docker.

```
local IMAGE="ibmcom/mq:latest"
docker pull $IMAGE
docker run -it --rm -p 127.0.0.1:1414:1414 -p 127.0.0.1:9157:9157 -e LICENSE=accept -e MQ_QMGR_NAME=DevQueueManager \
   -e MQ_ADMIN_PASSWORD=admin -e MQ_APP_PASSWORD=admin \
   -e MQ_DEV=true -h webspheremq.local "$IMAGE"
```