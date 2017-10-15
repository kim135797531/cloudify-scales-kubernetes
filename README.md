# Prerequisites
* Cloudify Manager
* Cloudify 4.1 CLI
* ...

# Plugin
## To clone this repository
```bash
git clone https://github.com/kim135797531/cloudify-scales-kubernetes/
cd ./cloudify-scales-kubernetes
```

## To execute wagon build (of plugin)
```bash
wagon create -f -s ./plugins/cloudify-kubernetes-plugin/
```
## To upload plugin
```bash
cfy plugin upload ./cloudify_kubernetes_plugin-1.2.0-py27-none-linux_x86_64-Ubuntu-trusty.wgn
```

# Blueprint
## To upload blueprint
```bash
# Default blueprint id will be set as cloudify-scales-kubernetes
cfy blueprints upload ./00-test.yaml
cfy blueprints upload ./01-wordpress-blueprint.yaml
```
## To deploy blueprint
```bash
# Default deployment id will be set as cloudify-scales-kubernetes
cfy deploy create -b cloudify-scales-kubernetes
```
## To install deployment
```bash
cfy executions start install -d cloudify-scales-kubernetes
```

## Summary
```bash
wagon create -f -s ./plugins/cloudify-kubernetes-plugin/
cfy plugin upload ./cloudify_kubernetes_plugin-1.2.0-py27-none-linux_x86_64-Ubuntu-trusty.wgn
cfy blueprints upload ./00-test.yaml
cfy deploy create -b cloudify-scales-kubernetes
cfy executions start install -d cloudify-scales-kubernetes
```

# Teardown
## To cancel the installing deployment
```bash
SERVER_IP=192.168.0.77
EXECUTION_ID=$(cfy executions list | grep -i started | awk '{print $2;}')
cfy executions cancel -f $EXECUTION_ID
# Check if cancelled
cfy executions list
```

## To force the canceling the installing deployment
```bash
curl -X PATCH \
     -H "Tenant: default_tenant" \
     -H "Content-Type: application/json" \
     -u admin:admin \
     -d '{"status": "cancelled"}' \
     http://SERVER_IP/executions/$EXECUTION_ID
```

## Remove deployment, blueprint and plugin
```bash
cfy executions start uninstall -d cloudify-scales-kubernetes -f
cfy deployments delete cloudify-scales-kubernetes -f
cfy blueprints delete cloudify-scales-kubernetes
# Check plugin id
PLUGIN_ID=$(cfy plugins list | grep -i cloudify-kubernetes-plugin | awk '{print $2;}')
cfy plugins delete $PLUGIN_ID
```