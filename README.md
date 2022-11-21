# Explode My SQL

The whole purpose of this micromaterial is to create a MySQL database, and then turn some knobs until it blows up. To do this, we'll need a few things:

1) A k3s cluster to run some pods (most likely via k3d)
2) A running MySQL datastore in a pod, that's filled with a bunch of data. The persistent data volume will be about 20GiB, so we can probably insert a few million rows or so...
3) A bunch of pods that read, and another bunch that write (this ratio will be configurable)
4) A web UI with some sort of UI elements (sliders/knobs/etc) that allow us to control how many of which type of pods there are (readers/writers).

We may also want to be able to configure what _type_ of reading and writing they're doing as well, but I haven't gotten that far in the design yet.

## Steps to run this locally

First, install `k3d` via the instructions at https://k3d.io/v5.4.6/.

Then, start up your k3s cluster via the instructions at https://k3d.io/v5.4.6/#quick-start.

After that's all set up, run the following (we'll script this out eventually) to get the MySQL DB and persistent volume set up:

```
kubectl apply -f mysql-pv.yaml
```

and then also

```
kubectl apply -f mysql-deployment.yaml
```

once that's all fired up, you should be able to access a client like the following:

```
kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql -ppassword
```

...to be continued...
