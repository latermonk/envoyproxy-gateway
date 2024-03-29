# Get started with Envoy Proxy in 5 minutes
https://tetrate.io/blog/get-started-with-envoy-in-5-minutes/    

## Lab env
https://killercoda.com/playgrounds/scenario/ubuntu   

## run two services
```
docker run -dit --env BG_COLOR="blue" -p 5050:3000 gcr.io/tetratelabs/color-app:1.0.0

docker run -dit --env BG_COLOR="green" -p 5000:3000 gcr.io/tetratelabs/color-app:1.0.0

```


## Install dunc-e
```
curl -L https://func-e.io/install.sh | bash -s -- -b .

sudo install func-e /usr/local/bin
```

## test

```
wget https://raw.githubusercontent.com/latermonk/envoyproxy-gateway/main/envoy/lab00-config.yaml

mv  lab00-config.yaml config.yaml

func-e run -c config.yaml

```


*config.yaml*
admin interface:
```
admin:
  access_log_path: /tmp/admin_access.log
  profile_path: /tmp/envoy.prof
  address:
    socket_address: { address: 127.0.0.1, port_value: 9901 }
```
config.yaml
```
static_resources:
  listeners:
  - name: listener_0
    address:
      socket_address:
        address: 0.0.0.0
        port_value: 10000    
    filter_chains:
    - filters:
      - name: envoy.filters.network.http_connection_manager
        typed_config:
          "@type": type.googleapis.com/envoy.extensions.filters.network.http_connection_manager.v3.HttpConnectionManager
          stat_prefix: edge
          http_filters:
          - name: envoy.filters.http.router
            typed_config:
              "@type": type.googleapis.com/envoy.extensions.filters.http.router.v3.Router
          route_config:
            virtual_hosts:
            - name: all_domains
              domains: ["*"]
              routes:
              - match:
                  prefix: "/blue"
                route:
                  cluster: blue
              - match:
                  prefix: "/green"
                route:
                  cluster: green
  clusters:
  - name: blue
    connect_timeout: 5s
    load_assignment:
      cluster_name: blue
      endpoints:
      - lb_endpoints:
        - endpoint:
            address:
              socket_address:
                address: 127.0.0.1
                port_value: 5050
  - name: green
    connect_timeout: 5s
    load_assignment:
      cluster_name: green
      endpoints:
      - lb_endpoints:
        - endpoint:
            address:
              socket_address:
                address: 127.0.0.1
                port_value: 5000
```



# Test

```
curl localhost:10000/blue
```

```
curl localhost:10000/green
```
