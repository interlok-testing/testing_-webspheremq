# WebsphereMQ Testing

[![license](https://img.shields.io/github/license/interlok-testing/testing_webspheremq.svg)](https://github.com/interlok-testing/testing_webspheremq/blob/develop/LICENSE)
[![Actions Status](https://github.com/interlok-testing/testing_webspheremq/actions/workflows/gradle-build.yml/badge.svg)](https://github.com/interlok-testing/testing_webspheremq/actions/workflows/gradle-build.yml)

Project tests interlok-webspheremq features

## What it does

This project contains a single instance of Interlok that will attempt to connect to a locally running WebpshereMQ instance.  It is assumed WebsphereMQ can be contacted on tcp://localhost:1414.  Once started a single polling trigger will produce a message every 10 seconds and send that message to a queue named "DEV.QUEUE.1".  
This channel maintains a transacted JMS session, meaning after every message has been consumed and moved from the first queue to the second the session will 'commit' or 'rollback' should there be a failure.

A second channel which is set to not start by default will provide the same messaging bridge but without the transacted session.  You'll need to log into the UI to start this channel manually.

![wmq diagram](/wmq.png "wmq diagram")
 
## Getting started

Before starting Interlok you need to create a Solace docker container with

* `docker-compose up`

Then start Interlok

* `./gradlew clean build`
* `(cd ./build/distribution && java -jar lib/interlok-boot.jar)`
