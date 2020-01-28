# go-socks5-proxy

Simple socks5 server using go-socks5 with authentication options

## Start container with proxy

```docker run -d --name socks5 -p 1080:1080 -e PROXY_USER=<PROXY_USER> -e PROXY_PASSWORD=<PROXY_PASSWORD>  varnav/go-socks5-proxy```

Leave `PROXY_USER` and `PROXY_PASSWORD` empty for skip authentication options while running socks5 server.

## List of all supported config parameters

|ENV variable|Type|Default|Description|
|------------|----|-------|-----------|
|PROXY_USER|String|EMPTY|Set proxy user (also required existed PROXY_PASS)|
|PROXY_PASSWORD|String|EMPTY|Set proxy password for auth, used with PROXY_USER|
|PROXY_PORT|String|1080|Set listen port for application inside docker container|

## Test running service

Without authentication

```curl --socks5 <docker host ip>:1080  http://ifcfg.co``` - result must show docker host ip (for bridged network)

or

```docker run --rm curlimages/curl:7.65.3 -s --socks5 <docker host ip>:1080```

With authentication - result must show docker host ip (for bridged network)

```curl --socks5 --user <PROXY_USER>:<PROXY_PASSWORD> <docker host ip>:1080  http://ifcfg.co```

or

```docker run --rm curlimages/curl:7.65.3 -s --socks5 <PROXY_USER>:<PROXY_PASSWORD>@<docker host ip>:1080```

## Run with Kubernetes


```
kubectl apply -f .\kubernetes-deployment.yml
kubectl expose deployment go-socks5-proxy --type LoadBalancer
```

## Use with Kubernetes

To get external IP address: `kubectl get service go-socks5-proxy`
To get login/password: 

```
kubectl get pods
kubectl logs go-socks5-proxy-geg440-klgeg
```


## Authors

* **Sergey Bogayrets**

See also the list of [contributors](https://github.com/serjs/socks5-server/graphs/contributors) who participated in this project.
