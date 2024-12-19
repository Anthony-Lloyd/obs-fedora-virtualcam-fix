# OBS Virtual Camera Fix on Fedora 41

This guide provides steps to set up the OBS Virtual Camera on Fedora 41.

---

## Prerequisites

### Enable RPM Fusion Repositories
RPM Fusion is required for additional software packages. Verify your repository list to ensure RPM Fusion is enabled:

```bash
dnf repolist
```

Example output:
```plaintext
repo id                                                     repo name
fedora                                                      Fedora 41 - x86_64
updates                                                     Fedora 41 - x86_64 - Updates
rpmfusion-free                                              RPM Fusion for Fedora 41 - Free
rpmfusion-nonfree                                           RPM Fusion for Fedora 41 - Nonfree
...
```

If RPM Fusion is not present in the list, follow the next section to enable it.

---

## Download and Install RPM Fusion Repositories
You can browse the RPM Fusion repository at the following links:
- [RPM Fusion Free Repository](https://download1.rpmfusion.org/free/fedora/)
- [RPM Fusion Nonfree Repository](https://download1.rpmfusion.org/nonfree/fedora/)

### Fedora 41 Specific Links
For Fedora 41, download and install the required RPM Fusion packages using these commands:

```bash
wget https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-41.noarch.rpm
wget https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-41.noarch.rpm
sudo dnf install ./rpmfusion-free-release-41.noarch.rpm
sudo dnf install ./rpmfusion-nonfree-release-41.noarch.rpm
```

---

## Installing OBS and Dependencies

### Step 1: Install OBS Studio
If OBS Studio is not installed, install it with the following command:

```bash
sudo dnf install obs
```

### Step 2: Install Virtual Camera Dependencies
Install the necessary kernel module and utilities for the virtual camera:

```bash
sudo dnf install lsb_release v4l2loopback kmod-v4l2loopback
```

---

## Loading and Configuring the Virtual Camera

### Step 1: Load the Kernel Module
After installing the dependencies, load the `v4l2loopback` kernel module with the following commands:

```bash
sudo depmod
sudo modprobe v4l2loopback devices=1 max_buffers=2 exclusive_caps=1 card_label="VirtualCam"
```

### Step 2: Configure `v4l2loopback`
Use `v4l2loopback-ctl` to further configure the virtual camera:

```bash
v4l2loopback-ctl
```

---

## Additional Notes

- If you encounter issues during installation or configuration, ensure your system is fully updated:

```bash
sudo dnf update
```

- You may need to reboot your system for changes to take effect.
- Check the status of the `v4l2loopback` module to confirm it is loaded:

```bash
lsmod | grep v4l2loopback
```

---

## Resources and Credits

- [RPM Fusion Free Repository](https://download1.rpmfusion.org/free/fedora/)
- [RPM Fusion Nonfree Repository](https://download1.rpmfusion.org/nonfree/fedora/)
- Original guide credit: [Wains' Blog](https://blog.wains.be/2021/2021-10-03-obs-studio-virtual-camera-fedora/)
