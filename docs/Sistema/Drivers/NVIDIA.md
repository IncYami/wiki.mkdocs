---
description: A guide on how to configure and install NVIDIA GPU drivers in AtlasOS
icon: simple/nvidia
---

# :simple-nvidia: Installing NVIDIA graphics drivers

We recommend using NVCleanstall, as it is a GUI alternative to manually stripping drivers.

## :simple-nvidia: Driver Installation

- Download [NVCleanstall](https://www.techpowerup.com/download/techpowerup-nvcleanstall).
- Open the application and click ``Next``.

??? question "Is the download unusually slow or stuck?"
    Go to [NVIDIA's advanced driver search](https://www.nvidia.com/download/find.aspx) and download the latest Game Ready Driver after selecting your hardware and operating system.
    Launch NVCleanstall, choose ``Use driver files on disk`` and locate the previously downloaded driver. Hit ``Next`` and continue with the installation.

- **For Desktops:** Make sure that only ``Display Driver`` is checked and click ``Next``.
- **For Laptops:** Check ``Display Driver`` and ``Optimus`` and click ``Next``. (More info on [NVIDIA's Website](https://www.nvidia.com/en-us/geforce/technologies/optimus))

- After the driver is downloaded tick the following:
    - Disable Installer Telemetry & Advertising
    - Perform a Clean Installation
    - Disable [Multiplane Overlay (MPO)](https://docs.atlasos.net/getting-started/post-installation/drivers/amd/#disable-multi-plane-overlay-mpo)
    - Disable Driver Telemetry in ``Show Expert Tweaks``
    - Use method compatible with Easy-Anti-Cheat
        - **This currently does not work on Windows 11 24H2!**
        - Automatically accept the "driver unsigned" warning
- Click ``Install`` and continue with the NVIDIA driver installation as usual.

## :material-cog: Configure NVIDIA Control Panel

This section was partly based on [valleyofdoom's documentation](https://github.com/valleyofdoom/PC-Tuning/blob/main/docs/configure-nvidia.md).

- Open the NVIDIA Control Panel by right-clicking on the desktop.
- Navigate to ``3D Settings -> Adjust image settings with preview``
    - Select **Use the advanced 3D image settings** and hit **Take me there**
- Configure the following in the ``3D Settings -> Manage 3D settings`` page:
    - Anisotropic filtering - Off
    - Antialiasing - Gamma correction - Off
    - Low Latency Mode - On (This setting limits pre-rendered frames to 1)
    - Power management mode - Prefer maximum performance
    - Shader Cache Size - Unlimited
    - Texture filtering - Quality - High performance
    - Threaded Optimization - Offloads GPU-related processing tasks on the CPU, it usually hurts frame pacing. If you are CPU bottlenecked, choose the ``Off`` option.
    - Vertical sync - Off
- Configure the following in the ``Display -> Change resolution`` page:
    - Configure your monitor resolution and refresh rate.
    - Output dynamic range - Full
    - Output color depth - Value matching your monitor specification
- Optionally increase the level of ``Digital vibrance`` in ``Display -> Adjust desktop color settings`` as it manages color saturation and intestity, and can reduce eye strain.
    - For an alternative way to adjust your digital vibrance, check out [VibranceGUI](https://vibrancegui.com).
- Configure the following in the ``Display -> Adjust desktop size and position`` page:
    - **For playing in native resolution:** Select scaling mode - No scaling
    - **For playing in stretched resolution:** Select scaling mode - Fullscreen
    - For setting up true display scaling, check out [CRU](https://www.monitortests.com/forum/Thread-Custom-Resolution-Utility-CRU).
- Set dynamic range to ``Full`` in ``Video -> Adjust video color settings -> Advanced``