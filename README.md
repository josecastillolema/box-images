# box-images
Collection of [toolbox](https://github.com/containers/toolbox/) and [distrobox](https://github.com/89luca89/distrobox) images.

## Toolbox

### fedora-toolbox (default)

```sh
cd toolbox/fedora-toolbox/44
podman build -t localhost/toolbox:44 .
toolbox create -i localhost/toolbox:44 fedora-toolbox-44
toolbox enter
```

### ocaml-5

OCaml with all the [OCaml Platform](https://ocaml.org/docs/platform) tooling.

```sh
cd toolbox/ocaml-5
podman build -t localhost/ocaml:5 .
toolbox create -i localhost/ocaml:5 ocaml
toolbox enter ocaml
```

### opam

[OCaml Package Manager](https://opam.ocaml.org/) (opam) without OCaml.
```sh
cd toolbox/opam
podman build -t localhost/opam .
toolbox create -i localhost/opam opam
toolbox enter opam
```

### mirage

OCaml (v4) with all the necessary [Mirage](https://mirage.io/) tooling to build unikernels.

```sh
cd toolbox/mirage
podman build -t localhost/mirage .
toolbox create -i localhost/mirage mirage
toolbox enter mirage
```

### perf-tuning

All the necessary tools for the *[Red Hat Performance Tuning: Linux in Physical, Virtual, and Cloud](https://www.redhat.com/en/services/training/rh442-red-hat-enterprise-performance-tuning)* (RH442) course.

```sh
cd toolbox/perf-tuning
podman build -t localhost/perf-tuning:8.0 .
toolbox create -i localhost/perf-tuning:8.0 perf-tuning
toolbox enter perf-tuning
```

## Distrobox

### dpu-sim

Development environment for [dpu-simulator](https://github.com/ovn-kubernetes/dpu-simulator). Includes libvirt-devel, podman-remote, and helm.

```sh
# Host prerequisites
$ sudo sysctl -w fs.inotify.max_user_instances=8192 fs.inotify.max_user_watches=1048576 fs.inotify.max_queued_events=32768
$ sudo modprobe openvswitch

# Build and create
$ cd distrobox/dpu-sim
$ podman build -t localhost/dpu-sim .
$ distrobox create --name dpu-dev --image localhost/dpu-sim --root
$ distrobox enter --root dpu-dev
⬢[dpu-dev]$ git clone https://github.com/ovn-kubernetes/dpu-simulator.git
⬢[dpu-dev]$ cd dpu-simulator
⬢[dpu-dev]$ sudo ./bin/dpu-sim --config config-kind.yaml
⬢[dpu-dev]$ sudo chown $USER:$USER kubeconfig/dpu-sim-host.kubeconfig
⬢[dpu-dev]$ sudo chown $USER:$USER kubeconfig/dpu-sim-dpu.kubeconfig
```
