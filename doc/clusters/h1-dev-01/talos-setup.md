# Setup

```bash
talosctl gen config \
    hl-dev-01 https://10.130.5.146:6443 \
    --config-patch @patch.yaml 
```
Apply the generated config to the control planes

```bash
talosctl apply-config --insecure --nodes 10.130.5.146 --file controlplane.yaml
talosctl apply-config --insecure --nodes 10.130.5.147 --file controlplane.yaml
talosctl apply-config --insecure --nodes 10.130.5.148 --file controlplane.yaml
```

Apply the config to the worker nodes

```bash
talosctl apply-config --insecure --nodes 10.130.5.149 --file worker.yaml
talosctl apply-config --insecure --nodes 10.130.5.150 --file worker.yaml
talosctl apply-config --insecure --nodes 10.130.5.151 --file worker.yaml 
```

Export talos-config settings

```shell
export TALOSCONFIG="talosconfig"
talosctl config endpoint 10.130.5.146     
talosctl config node 10.130.5.146   
```

Configure endpoint for the talosconfig

```bash
talosctl config endpoint 10.130.5.146
```

Set which node configs will be passed to

```shell
talosctl config node 10.130.5.146
```

Bootstrap the etcd

```shell
talosctl bootstrap
```

Pull the admin kubeconfig

```shell
talosctl kubeconfig .
```

Install Cilium CNI

```bash
cilium-cli install \ 
    --helm-set=ipam.mode=kubernetes \
    --helm-set=kubeProxyReplacement=true \
    --helm-set=securityContext.capabilities.ciliumAgent="{CHOWN,KILL,NET_ADMIN,NET_RAW,IPC_LOCK,SYS_ADMIN,SYS_RESOURCE,DAC_OVERRIDE,FOWNER,SETGID,SETUID}" \
    --helm-set=securityContext.capabilities.cleanCiliumState="{NET_ADMIN,SYS_ADMIN,SYS_RESOURCE}" \
    --helm-set=cgroup.autoMount.enabled=false \
    --helm-set=cgroup.hostRoot=/sys/fs/cgroup \
    --helm-set=k8sServiceHost=localhost \
    --helm-set=k8sServicePort=7445
```