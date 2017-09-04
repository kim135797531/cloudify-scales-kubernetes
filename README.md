# Prerequisites
* Cloudify Manager
* Cloudify 4.1 CLI
* ...

# Plugin
## To execute wagon build (of plugin)
```bash
git clone https://github.com/kim135797531/cloudify-scales-kubernetes/
cd ./cloudify-scales-kubernetes
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
cfy blueprints upload ./wordpress-blueprint.yaml
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

# Remove deployment, blueprint and plugin
```bash
cfy executions start uninstall -d cloudify-scales-kubernetes
cfy deployments delete cloudify-scales-kubernetes
cfy blueprints delete cloudify-scales-kubernetes
# Check plugin id
cfy plugins list
cfy plugins delete [PLUGIN_ID]
```


