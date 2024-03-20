# Setup

```bash
talosctl gen config hl-dev-01 https://10.130.5.142:6443 --output-dir $PWD 
talosctl apply-config --insecure --nodes 10.130.5.142 --file $PWD/controlplane.yaml 
talosctl apply-config --insecure --nodes 10.130.5.143 --file $PWD/controlplane.yaml
talosctl apply-config --insecure --nodes 10.130.5.144 --file $PWD/worker.yaml
talosctl apply-config --insecure --nodes 10.130.5.145 --file $PWD/worker.yaml
talosctl config endpoint 10.130.5.142     
talosctl config node 10.130.5.142
talosctl bootstrap                                                                                                                   ✔  19:07:19 
talosctl kubeconfig .
```

