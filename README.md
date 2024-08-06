### install etcdctl
- [github](https://github.com/etcd-io/etcd/releases)

```
ETCD_VER=v3.5.15

# choose either URL
GOOGLE_URL=https://storage.googleapis.com/etcd
GITHUB_URL=https://github.com/etcd-io/etcd/releases/download
DOWNLOAD_URL=${GOOGLE_URL}

rm -f /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz
rm -rf /tmp/etcd-download-test && mkdir -p /tmp/etcd-download-test

curl -L ${DOWNLOAD_URL}/${ETCD_VER}/etcd-${ETCD_VER}-linux-amd64.tar.gz -o /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz
tar xzvf /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz -C /tmp/etcd-download-test --strip-components=1
rm -f /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz

/tmp/etcd-download-test/etcd --version
/tmp/etcd-download-test/etcdctl version
/tmp/etcd-download-test/etcdutl version
```



```
# 必要, 使用etcd version 3 的api

export ETCDCTL_API=3
etcdctl version

## 設置 Flannel 網絡配置
etcdctl --endpoints=http://192.168.5.40:2379 put /coreos.com/network/config '{"Network":"10.0.0.0/8", "SubnetLen": 24, "Backend": {"Type": "vxlan"}}'
# etcdctl --endpoints=http://192.168.5.40:2379 put /coreos.com/network/config '{"Network":"10.0.0.0/8", "SubnetLen": 20, "Backend": {"Type": "vxlan"}}'
## 檢查 etcd 中的網絡配置
etcdctl --endpoints=http://192.168.5.40:2379 get /coreos.com/network/config
## 檢查 etcd 中的子網分配
etcdctl --endpoints=http://192.168.5.40:2379 get --prefix /coreos.com/network/subnets
```
