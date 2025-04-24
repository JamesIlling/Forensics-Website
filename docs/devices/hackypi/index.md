# HackyPi

![HackyPi](img/overview.jpg)

## Introduction

The HackiPi is an Arm Cortex M0+ with a 1.14 inch TST display on it. The device is available from [SB Componenets](https://shop.sb-components.co.uk/products/hackypi-compact-diy-usb-hacking-tool).
There is [software git repository](https://github.com/sbcshop/HackyPi-Software), which contains some examples, including how to use the device as a keyboard (BadUSB device).

This is a pretty small device (54.74mm x 23.20mm) (slightly larger with the enclosure) taken from the [hardware git repository](https://github.com/sbcshop/HackyPi-Hardware/tree/main). 
The main processor is a Rasperry Pi RP2040, which supports circuit python / python / Pico C++.

### Pros and Cons

| Pros                                | Cons                                        |
| :---------------------------------- | :------------------------------------------ |
| Has a screen for visual feedback    | Obviously not a normal USB                  |
| Requires no drivers installed (PnP) | Limited to Keystroke Injection Attack       |
| Easy to code                        | 3D printed case, which doesnt fit perfectly |
| Cheap (~£30)                        |                                             |

### Uses

* Keystroke Injection Attack (BadUSB)

## Detailed investigation

### Registry information from creation

Detection under windows:

| Vendor id | Product Id | Interface | Description             | Notes                                              | Keys                                                                                                                                  |
| :-------- | ---------- | --------- | ----------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 0x239A    | 0x80F4     |           | Root device             |                                                    |                                                                                                                                       |
| 0x239A    | 0x80F4     | 0x00      | USB Serial              | USB serial COM PORT                                | HKEY_LOCAL_MACHINE\System\ControlSet001\Enum\USB\VID_239A&PID_80F4&MI_00\6&722f050&0&0000                                             |
| 0x239A    | 0x80F4     | 0x01      |                         | Does Not appear in registry                        |                                                                                                                                       |
| 0x239A    | 0x80F4     | 0x02      | USB Mass Storage Device | USES USBSTOR (Disk&Ven_Raspberr&Prod_Pico&Rev_1.0) | HKEY_LOCAL_MACHINE\System\ControlSet001\Enum\USB\VID_239A&PID_80F4&MI_02\6&722f050&0&0002                                             |
| 0x239A    | 0x80F4     | 0x03      | Human Interface Device  | HID Keyboard Device                                | HKEY_LOCAL_MACHINE\System\ControlSet001\Enum\HID\VID_239A&PID_80F4&MI_03&Col01\7&191edf42&0&0000                                      |
| 0x239A    | 0x80F4     | 0x03      | Human Interface Device  | HID Mouse Device                                   | HKEY_LOCAL_MACHINE\System\ControlSet001\Enum\HID\VID_239A&PID_80F4&MI_03&Col02\7&191edf42&0&0001                                      |
| 0x239A    | 0x80F4     | 0x03      | Human Interface Device  | HID-compliant consumer control device              | HKEY_LOCAL_MACHINE\System\ControlSet001\Enum\HID\VID_239A&PID_80F4&MI_03&Col03\7&191edf42&0&0002                                      |
| 0x239A    | 0x80F4     | 0x04      | CircuitPython Audio     | Internal AUX jack                                  | HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\MMDevices\Audio\Render\{a05d30b9-85c5-4cd5-ae39-e2a9537ca17e}\Properties |
