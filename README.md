# envoy-examples
A scratchpad for Envoy experiments

## Installing Envoy

This guide assumes you are running on Envoy on a Linux system, specifically Ubuntu. 
If you want to create a quick Ubuntu VM, consider [Multipass](https://multipass.run/).

RPMs and deb packages are notoriously out of date and unsupported on Linux.
The easiest way to install Envoy is to use [func-e](https://func-e.io/) to install and manage the envoy version.
The [Consul Service Mesh tutorial](https://learn.hashicorp.com/tutorials/consul/service-mesh-with-envoy-proxy#install-envoy-on-the-agent) goes into depth more about installing and running Envoy.

```bash
curl -L https://func-e.io/install.sh | sudo bash -s -- -b /usr/local/bin
func-e use 1.21.2
sudo cp ~/.func-e/versions/1.21.2/bin/envoy /usr/local/bin/
envoy version
```

## Running Envoy

To run envoy with debug tracing mode enabled, run the following command:

```bash
sudo envoy -c config.yaml --service-node node1 --service-cluster c1 -l trace
```

If you want to validate your envoy configuration before running it, you can use the validation mode.

```bash
sudo envoy --mode validate -c config.yaml
```

## Debugging Envoy

You can export the xDS configuration of Envoy using the Admin API exposed on localhost as follows:

```bash
curl http://127.0.0.1:19000/config_dump\?include_eds
```

## Examples

Each of the included directories contains a complete envoy configuration which can be tested with the commands included in the README.md.
