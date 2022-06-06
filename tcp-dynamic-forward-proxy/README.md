# TLS-only Dynamic Forward Proxy

## Usecase
Dynamic Forward Proxy uses the SNI information on any TLS-based connection to route the request to the upstream with the that hostname. Does not require to the hostname to be known in advance and caches the DNS results.

## Testing
Create the `iptables` rule that mimics transparent proxy mode.

```bash
sudo iptables -t nat -A OUTPUT -p tcp -m owner --uid-owner ubuntu --dport 443 -j REDIRECT --to-port 10000 #assumes ubuntu user
sudo envoy -c tcp-dynamic-forward-proxy.yaml --service-node node1 --service-cluster c1 -l trace&
curl https://www.google.com
```

## Relevant Docs
* [Dynamic Forward Proxy](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/dynamic_forward_proxy_filter#config-http-filters-dynamic-forward-proxy)

