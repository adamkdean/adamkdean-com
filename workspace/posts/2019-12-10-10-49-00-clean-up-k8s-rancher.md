---
title: Clean up k8s/Rancher
slug: clean-up-k8s-rancher
date: 2019-12-10 10:49
---

This script is mostly for myself in the future. While playing around with Kubernetes and Rancher, machines become polluted with directories in `/var`, `/etc`, and `/opt`. Pollution is bad. This script will remove those as well as wiping down a system.

Warning: this contains a system prune, and removes everything.

```
#!/bin/bash
#
# Clean up k8s/rancher
# (Run as root or rm -rf will fail)

docker ps -qa | xargs docker rm -f
docker system prune

cleanupdirs="/var/lib/etcd /etc/kubernetes /etc/cni /opt/cni /var/lib/cni /var/run/calico"
for dir in $cleanupdirs; do
  echo "Removing $dir"
  rm -rf $dir
done
```
