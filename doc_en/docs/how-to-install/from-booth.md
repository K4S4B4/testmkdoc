---
title: From BOOTH
parent: How to install
grand_parent: English
nav_order: 1
---

# Install and update from BOOTH

## How to download
### Free trial version
Free trial version is available on BOOTH.  

[BOOTH store](https://akiya-souken.booth.pm/items/3026474){: .btn }  

It is required to try free version and confirm that the software works without problems in your environment before purchase of paid version.   
The free version has limited functionality only for data export.  
- Data sending via VMT protocol and VMC protocol stops and restarts every 10 seconds
- Maximum frames in a BVH file is limited to 300

### Paid version
Before purchase, please read and accept the terms and conditions from the following link.  
If you agree, you can get your purchase password and proceed to the purchase page at BOOTH.  

[Our HP](https://vrlab.akiya-souken.co.jp/product#buy){: .btn .btn-red }  

You need a pixiv account to purchase at BOOTH.

## How to install
You can install MocapForAll [manually](#manual-installation) or by using [network installer](#installation-by-network-installer) from BOOTH.  

### Manual installation

#### Main files
1. Download and unzip "MocapForAll_Full_vN.N.N.zip"
2. Execute MocapForAll.exe in "MocapForAll_Full_vN.N.N" folder
3. If the "UE4 Prerequisites" installation screen is displayed, install it.

#### Appendix (Optional)

If you do not need the functions in Appendix, you can skip this step.  
There are four Appendix as follows:

- Appendix1：Precision mode  
  Adds "Precision" mode for precise motion capture. Since the CPU / GPU usage is very high, it is not recommended to use with VR apps at the same time.
- Appendix2：HDRI maps  
  Adds maps which use HDRI images from [HDRI Haven](https://hdrihaven.com).  
- Appendix3：MetaHuman character  
  Adds a character created by Epic games' MetaHuman Creator. Used to test motion capture on MocapForAll.
- Appendix4：TensorRT mode (Deprecated)  
  Adds "GPU_TensorRT" mode which provides GPU acceleration on supported NVIDIA GPUs. As described below, CUDA, cuDNN, and TensorRT need to be installed. (In most cases, the standard "GPU_DirectML" mode will suffice.)
  This feature is deprecated because the improvement of performance is often very small or sometimes negative, and whether it works depends on the user's environment.

##### How to install Appendix
1. Download and unzip "AppendixN_xxxxx_yyyyy.zip".
2. Overwrite "MocapForAll_Full_vN.N.N\MocapForAll" with "AppendixN_xxxxx_yyyyy\MocapForAll".
3. If you install "Appendix4_TensorRT_mode", follow the [installation guide of TensorRT](./install-tensorrt).


### Installation by Network Installer
1. Download and unzip "Network_Installer_-_MocapForAll_Full_vN.N.N.zip".

2. Execute "Network_Installer_-_MocapForAll_Full_vN.N.N.exe".

3. Select the required Appendix. See [Appendix](#appendix-optional) for the contents.

   To use "Appendix4_TensorRT_mode", see [Installation of TensorRT](./install-tensorrt) and install the required software.

4. Run MocapForAll from the Start menu or MocapForAll.exe in the installation path.

5. If the "UE4 Prerequisites" installation screen is displayed, install it.


## How to update from BOOTH

### Manual update

1. Download and unzip "MocapForAll_Full_vN.N.N.zip".
2. Overwrite the old version of "MocapForAll_Full_vM.M.M" with new "MocapForAll_Full_vN.N.N".

### Update by Network Installer

Same as installation.

If you wan to reduce the data size to download, select only "Main Files" in "Select Components" screen without selecting "Appendix" and execute installation.   
Since the installer does not delete files, the previous Appendix remains .  
After that, Appendix will be treated as not installed on the "Select Components" screen of the installer, but this cause no problem.
