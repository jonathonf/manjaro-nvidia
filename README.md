# manjaro-nvidia
PKGBUILD files for packaging the latest NVIDIA drivers for Manjaro.

# How to install
Clone the repo, build and install `nvidia-utils`, then build the extramodule for
each kernel you have installed:

```
git clone https://github.com/jonathonf/manjaro-nvidia.git
cd manjaro-nvidia/nvidia-utils
makepkg -Csrc
sudo pacman -Udd *pkg*xz
cd ../nvidia-414
makepkg -Csric
```

In common with building any package you'll need `base-devel` installed first.
You could also use a clean chroot or other build container.

If you need `multilib` support, build `lib32-nvidia-utils` too. If you don't, don't. :)

You may also want to build `nvidia-settings` to match the current driver version.

# How to maintain
You must rebuild the extramodule each time the kernel is updated.

I suggest incrementing the `pkgrel` by one point to match the new kernel point-release 
version. This should make it easy to keep track of whether you've done it yet.

# How to update manually
Bump the `pkgver` in the relevant PKGBUILD file, then attempt a rebuild. Minor
version updates for the same series are unlikely to alter soname versions, but
if they do (or you switch to a different series) you'll have to browse the
extracted package source to find where the files have moved to.

`makepkg` should tell you during the `package()` step if any files are no longer
in the expected place, but not if a new file is needed. That's up to you to spot.
;)
