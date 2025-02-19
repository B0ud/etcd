# etcd local-tester

> [!WARNING]
> etcd-local-tester is now deprecated in favor of our much more comprehensive [robustness testing suite](https://github.com/etcd-io/etcd/tree/main/tests/robustness). In a future etcd release this historic tool will be removed as it is no longer maintained.

The etcd local-tester runs a fault injected cluster using local processes. It sets up an etcd cluster with unreliable network bridges on its peer and client interfaces. The cluster runs with a constant stream of `Put` requests to simulate client usage. A fault injection script periodically kills cluster members and disrupts bridge connectivity.

# Requirements

local-tester depends on `goreman` to manage its processes and `bash` to run fault injection.

# Building

local-tester needs `etcd`, `benchmark`, and `bridge` binaries. To build these binaries, run the following from the etcd repository root:

```sh
./scripts/build.sh
pushd tools/benchmark/ && go build && popd
pushd tools/local-tester/bridge && go build && popd
```

# Running

The fault injected cluster is invoked with `goreman`:

```sh
goreman -f tools/local-tester/Procfile start
```
