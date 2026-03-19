# Lab 3 — Zephyr on Longan Nano
 
Full course wiki:  
https://github.com/parastuffs/4EIOS-Operating-Systems/wiki 
 
--- 
 
## Introduction
This lab introduces Zephyr RTOS, a lightweight real-time operating system running on the microcontroller of the Longan Nano board. 
  
 
## What is Zephyr? 
 
Zephyr RTOS is a real-time operating system designed for embedded systems and microcontrollers.  
 
Instead of writing a single bare-metal program, Zephyr provides: 
 
- A kernel 
- Thread/task scheduling 
- Device drivers 
- Network stacks 
- Hardware abstraction 
- Libraries for sensors, communication, and more 
 
It is similar to other RTOS like: 
 
- FreeRTOS 
- VxWorks 
- RTEMS 
 
Zephyr is open-source and maintained by the Linux Foundation. 
 
## What is the Longan Nano? 
 
The Sipeed Longan Nano is a small development board featuring: 
 
- GD32VF103 microcontroller 
- RISC-V CPU 
- GPIO, SPI, I2C, timers, and other peripherals 
 
It can be programmed using: 
 
- Bare-metal C 
- Arduino-style firmware 
- An RTOS like Zephyr 
 
 
## What Zephyr enables on the board 
 
### Threads (Tasks) 
Zephyr schedules multiple threads automatically. 
 
### Timers 
You can blink an LED periodically without using busy-wait loops. 
 
 
## Setup & Installation (Fedora) 
 
1. Update the system 
```bash 
sudo dnf upgrade --refresh 
```
2. Install development tools 
```
sudo dnf group install development-tools 
```
3. Install Zephyr dependencies 
```
sudo dnf install git python3 python3-pip python3-venv cmake ninja-build \ 
gperf ccache dfu-util device-tree-compiler wget xz file make gcc gcc-c++ 
```
 
 

Setup Zephyr workspace 
```
mkdir zephyrproject 
cd zephyrproject 
```
Install west (Zephyr tool) 
```
pip3 install --user west 
export PATH="$HOME/.local/bin:$PATH" 
```
Initialize Zephyr 
```
west init 
west update 
west zephyr-export 
```
Additional Python tools 
```
pip3 install --user semver 
pip3 install --user patool 
```
 
 

### Install Zephyr SDK 

Download the full Linux x86_64 SDK from: 
https://github.com/zephyrproject-rtos/sdk-ng/releases/tag/v0.17.4 

Extract SDK 
```
mkdir ~/dev/OS/zephyr-sdk 
cd ~/dev/OS/zephyr-sdk 
tar xf zephyr-sdk-0.17.4_linux-x86_64.tar.xz 
```
Run setup 
```
cd zephyr-sdk-0.17.4 
./setup.sh 
```
 
 

### Configure environment 

Add toolchain to PATH 

Edit ~/.bashrc and add: 
```
export ZEPHYR_SDK_INSTALL_DIR=~/dev/OS/zephyr-sdk/zephyr-sdk-0.17.4 
export PATH="$ZEPHYR_SDK_INSTALL_DIR/riscv64-zephyr-elf/bin:$PATH" 
```
Apply changes: 
```
source ~/.bashrc 
```
Load SDK environment 
```
source ~/dev/OS/zephyr-sdk/zephyr-sdk-0.17.4/environment-setup-x86_64-pokysdk-linux 
```
Make it permanent: 
```
echo 'source ~/dev/OS/zephyr-sdk/zephyr-sdk-0.17.4/environment-setup-x86_64-pokysdk-linux' >> ~/.bashrc 
source ~/.bashrc 
```
Verify installation 
```
which riscv64-zephyr-elf-gcc 
riscv64-zephyr-elf-gcc --version 
```
 
 

### Troubleshooting 

If installation fails, reinstall dependencies: 
```
sudo dnf install git python3 python3-pip python3-venv cmake ninja-build \ 
gperf ccache dfu-util device-tree-compiler wget xz file make gcc gcc-c++ 
```
 
 


 