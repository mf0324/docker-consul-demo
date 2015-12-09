Automatic proxified docker setup demo
======================================


## What is this?

This is a demo using:

* docker
* docker-compose for composition
* consul for service discovery
* registrator to automatically feed consul with new containers
* tutum/hello-world as the demo application

## How to run

```
$ docker-compose up -d
```

## What is there to see?

Once the stack is started, you can view:

* the consul dashboard at [http://consul-admin.127.0.0.1.xip.io](http://consul-admin.127.0.0.1.xip.io)
* the haproxy dashboard at [http://proxy-admin.127.0.0.1.xip.io](http://proxy-admin.127.0.0.1.xip.io)
* the running application at [http://hello-dev.127.0.0.1.xip.io](http://hello-dev.127.0.0.1.xip.io)


## Scale the app

If you type:

```
$ docker-compose scale web=2
```

You will see:

* A new node added to the [consul dashboard](http://consul-admin.127.0.0.1.xip.io)
* A new backend added to the [haproxy dashboard](http://proxy-admin.127.0.0.1.xip.io)
* A changing ID when refreshing the [application page](http://hello-dev.127.0.0.1.xip.io)


## Health checking

Health checking is implemented at two levels in this stack:

* [haproxy](http://proxy-admin.127.0.0.1.xip.io) checks that port 80 of each member is up
* [consul](http://consul-admin.127.0.0.1.xip.io) checks that `/` of each member returns a 200 status

If either check fails, the node will not be proxified.


## TODO

- [ ] Test with an overlay network and:

  - [ ] get rid of links
  - [ ] use consul DNS instead of links

- [ ] Test on swarm
- [ ] Port to an AWS ECS stack with CloudFormation

