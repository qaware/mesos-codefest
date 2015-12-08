# Mesos and Marathon 101
Keep https://mesosphere.github.io/marathon/docs open in a browser, you'll need it.

## Placeholders
- $DCOS_CLI_HOME: DCOS command line tool directory
- $MASTER_IP_ADDRESS: Mesos Master IP address

## Install Marathon

Since Marathon is installed by default on DCOS this is a NOP.

## Launch apps via the Marathon UI

- Got to DCOS dashboard and click on the Marathon service
- In the Marathon UI
 - Start simple app such as `while [ true ] ; do echo "Hello DCOS" ; sleep 5 ; done`
 - Scale up and down
 - Make yourself familiar with health checks

## Launch apps via Marathon HTTP API

Note that we will use [HTTPie](http://httpie.org) in the following but you can use `curl` should you wish to do that.

    $ cd $DCOS_CLI_HOME
    $ http POST http://$MASTER_IP_ADDRESS/service/marathon/v2/apps < mesos-codefest/mesos-marathon/marathon-hello-world.json

There are more sample app specs here in this directory:

- `marathon-peek.json` that launches a Docker images that introspects itself
- `marathon-private-registry.json` that launches a Docker registry
- `marathon-mattermost.json` that launches an OSS Slack clone (using a MySQL database underneath)

## List apps via Marathon HTTP API

    $ http http://$MASTER_IP_ADDRESS/service/marathon/v2/apps
    
## Launch & list apps via Java Code
- [Sample code](https://github.com/adersberger/cloudcomputing/blob/master/06-cluster-scheduling/uebung/loesung/src/main/java/edu/qaware/cc/marathon/MarathonController.java)

## Use Marathon in DCOS

    $ cd $DCOS_CLI_HOME
    $ dcos marathon app add marathon-mattermost.json
    $ dcos marathon app list
