# 32BlitFlashTest
Test binaries and instructions for testing external flashing.

Currenly Supports
1. Display list of bin files on SDCard (just one page), program external flash and run.
2. Switch between running loader and app from "System Menu"
3. Reset over CDC
4. Save bin files to SDCard over CDC
5. Program external flash over CDC.
6. Display debug logging from 32Blit.

## Flash the 32Blit

First flash the 32Blit with the loader application found in Loader folder.
The Loader application will display a list of *.bin files on the SDCard.
If you have no *.bin files you should see "No files found." displayed.


## Info

In the following examples my 32Blit is attached to /dev/cu.usbmodem305B395634371 on OSX, COM3 on Windows and /dev/serial/by-id/usb-STMicroelectronics_32Blit_CDC_305B39563437-if00 on Linux..
All commands are from the root of this repository.
The Bin folder contains the examples built to run from external flash.

On Linux there may be a chance that the device file changes for your Blit32, so maybe between ttyACM0 and ttyACM1 for example.
You can use the device file in /dev/serial/by-id/ instead as this will not change.

## Reseting the 32Blit

To reset the 32Blit we send the _RST command:

So for OSX: 
```
./OSX/32Blit _RST /dev/cu.usbmodem305B395634371
```
Linux: 
```
./Linux/32Blit _RST /dev/serial/by-id/usb-STMicroelectronics_32Blit_CDC_305B39563437-if00
```
Windows : 
```
Windows\32Blit.exe _RST COM3
```


## Saving bin file to SDCard
To save a bin file to the SDcard we use the SAVE command:

So for OSX: 
```
./OSX/32Blit SAVE /dev/cu.usbmodem305B395634371 Bins/logo.bin
```
Linux: 
```
./Linux/32Blit SAVE /dev/serial/by-id/usb-STMicroelectronics_32Blit_CDC_305B39563437-if00 Bins/logo.bin
```
Windows : 
```
Windows\32Blit.exe SAVE COM3 Bins/logo.bin
```

You should see:
```
Getting info from 32Blit...No reset needed.
Sending binary file *********************************************************************
Sending complete.
```

The 32Blit screen should now re-display the list of bin files on the SDCard and you should see logo.bin
If you know press the A button, the loader will load logo.bin from the SDCard and program the external flash and run it.



Now that the Logo app is running, lets try saving another file:

So for OSX: 
```
./OSX/32Blit SAVE /dev/cu.usbmodem305B395634371 Bins/hardware-test.bin
```
So for Linux: 
```
./Linux/32Blit SAVE /dev/serial/by-id/usb-STMicroelectronics_32Blit_CDC_305B39563437-if00 Bins/hardware-test.bin
```
Windows : 
```
Windows\32Blit.exe SAVE COM3 Bins/hardware-test.bin
```

You should see:
```
Getting info from 32Blit...Reset needed.
Reseting 32Blit and waiting for USB connection, please wait...
Reconnected to 32Blit after reset.
Sending binary file ***********************************************************************
Sending complete.
```

The screen should now show both logo.bin and hardware.bin, you can move between them with the DPad.
Select hardware-test.bin and press A and it should run.

Now press the "System Menu" button and scroll down and select "Switch Exe", you should now be back on the loader screen.


## Programming the external flash directly.

To program a bin file directly to the external flash we use the PROG command,
This command after programming will keep the com port open to display any
32Blit debug messages, I have put a debugf() call in Render() in the Logo app so lets use that:

So for OSX: 
```
/OSX/32Blit PROG /dev/cu.usbmodem305B395634371 Bins/logo.bin
```
Linux: 
```
/Linux/32Blit PROG /dev/serial/by-id/usb-STMicroelectronics_32Blit_CDC_305B39563437-if00 Bins/logo.bin
```
Windows : 
```
Windows\32Blit.exe PROG COM3 Bins/logo.bin
```

You should see:
```
Getting info from 32Blit...No reset needed.
Sending binary file *********************************************************************
Sending complete.
Waiting for USB connection for debug logging, please wait...
Connected to 32Blit.
render 1794
render 2918
render 2944
render 2965
render 2991
render 3018
render 3044
render 3065
render 3091
render 3117
```

Use ctrl/c to stop the output.


So if you could test out various commands and check if everything works it would be fantastic.










 


