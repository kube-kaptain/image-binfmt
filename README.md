# Image Binfmt

Image Binfmt is a re-tagged `tonistiigi/binfmt` image for in-house use.


## Origin

The image produced by this project is simply the one specified in
`KaptainPM.yaml` under `spec.main.docker.retag`, under a new name and in-house
control. Upstream source is [tonistiigi/binfmt](https://github.com/tonistiigi/binfmt),
maintained by Tõnis Tiigi of the Docker BuildKit team. It is the same image
Docker's own `setup-qemu-action` uses.

Upstream publishes three tag families per QEMU version: `qemu-*`, `buildkit-*`
and `desktop-*`. This project uses `qemu-*`, the general purpose one. Each also
has a `-NN` build number twin; this project pins those, because the plain
`qemu-vX.Y.Z` tag is moved when upstream rebuilds the same QEMU version.


## Versioning

The version is taken from the QEMU version in `sourceTag` plus a build counter,
so `qemu-v10.2.3-68` produces `10.2.3.1`, `10.2.3.2`, etc. Bumping only the
upstream build number produces the next patch of the same prefix.


## Purpose

Registers QEMU user-mode emulators with the host kernel's `binfmt_misc` so that
foreign architecture container images can run, which multi-arch builds need for
any `RUN` step. It must be run privileged, so it is worth controlling exactly
which image that is:

```
docker run --privileged --rm <this image> --install arm64
```


## Consumption

As with all publicly available images, it is okay to use this when getting
started. Once up and running, mirror it yourself, or fork this repo and retag
the upstream image under your own control.
