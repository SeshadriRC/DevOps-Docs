### Before running the script perform below things in server. Also run the script as a root user.


Now we found the exact issue.

Error:

```text id="d34v2f"
Failed to check br_netfilter:
stat /proc/sys/net/bridge/bridge-nf-call-iptables:
no such file or directory
```

That means **bridge netfilter kernel module is not loaded**.

Flannel requires:

```text id="sgzgxw"
br_netfilter
```

Load it.

Run:

```bash
sudo modprobe br_netfilter
```

Verify:

```bash
lsmod | grep br_netfilter
```

Expected:

```text
br_netfilter
bridge
```

Then enable required sysctl values:

```bash
sudo tee /etc/sysctl.d/k8s.conf <<EOF
net.bridge.bridge-nf-call-iptables=1
net.bridge.bridge-nf-call-ip6tables=1
net.ipv4.ip_forward=1
EOF
```

Apply:

```bash
sudo sysctl --system
```

Verify:

```bash
cat /proc/sys/net/bridge/bridge-nf-call-iptables
```

Expected:

```text
1
```

Restart Flannel:

```bash
kubectl delete pod -n kube-flannel -l app=flannel
```

Watch:

```bash
kubectl get pods -A -w
```

Expected flow:

```text
kube-flannel     Running
coredns          Running
node             Ready
app pod          Running
```

Finally check:

```bash
kubectl get nodes
```

Expected:

```text
ip-172-31-5-15   Ready
```

Your cluster is very close — networking is the only blocker now.


----

- Also if weave not working, then install flannel

```bash
kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
```
