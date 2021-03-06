WHAT IS THIS?
=============

Wlan module source code for the devices:
* bq aquaris V


BUILD INSTRUCTIONS?
===================

Specific sources are separated by releases with it's corresponding number. First, you should
clone the projects:

        $ git clone https://github.com/bq/aquaris-V.git ; git clone https://github.com/bq/wlan_module_qcom.git

After it, choose the release you would like to build:

*Aquaris V*

        $ mv aquaris-V kernel ; cd kernel ; git checkout tags/{release} ; cd ..
        $ mv wlan_module_qcom wlan ; cd wlan ; git checkout tags/{release} ; cd ..

Download a prebuilt gcc:

        $ git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8

Create KERNEL_OUT directory:

        $ mkdir KERNEL_OUT

Your directory tree should look like this:
* kernel
* arm-eabi-4.8
* KERNEL_OUT
* wlan

Build the kernel according the next table of product names:

| device                    | product                 |
| --------------------------|-------------------------|
| bq aquaris V              | nappa                   |


        $ make -C kernel O=../KERNEL_OUT  ARCH=arm CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi- {product}_defconfig
        $ make O=../KERNEL_OUT/ -C kernel ARCH=arm CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi-

You can specify "-j CORES" argument to speed-up your compilation, example:

        $ make O=../KERNEL_OUT/ -C kernel ARCH=arm CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi- -j 8

Finally, build the wlan module:

        $ make -C kernel/ M=../wlan/ O=../KERNEL_OUT/ ARCH=arm CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi- modules WLAN_ROOT=../wlan/ MODNAME=wlan BOARD_PLATFORM=msm8937 CONFIG_PRONTO_WLAN=m

You can specify "-j CORES" argument to speed-up your compilation, example:

        $ make -C kernel/ M=../wlan/ O=../KERNEL_OUT/ ARCH=arm CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi- modules WLAN_ROOT=../wlan/ MODNAME=wlan BOARD_PLATFORM=msm8937 CONFIG_PRONTO_WLAN=m -j 8

