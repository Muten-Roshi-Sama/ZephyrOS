# Build and flash first example: Blinky 

### Build :
```bash
cd zephyrproject/zephyr 
west build -p always -b longan_nano samples/basic/blinky 
```
### Flash to board 
Ensure dfu-util is installed: 
```bash
sudo dnf install dfu-util 

west flash --runner dfu-util 
```
