# Proxmox macOS Support Devices
<br></br>
Select from the below 2 options to get started:
<br></br>
### [WiFi/Bluetooth Devices](https://github.com/HSVEOCT/docs/blob/main/guides/Supported%20Devices%20Guide/readme.md#wifibluetooth-devices-list)
### [Compatible GPUs](https://github.com/HSVEOCT/docs/blob/main/guides/Supported%20Devices%20Guide/readme.md#compatible-gpus)

<br></br>
<br>
## WiFi/Bluetooth Devices List

## Notice
You yourself are responsible for which one of the adapters listed below. If the one you bought doesn’t work as intended, there’s nothing we can do or take any responsibility for!

Should you already have a built-in Wi-Fi/Bluetooth card installed on your motherboard and it’s incompatible, make sure to remove it or disable in BIOS if possible. Will cause interference with any external cards installed.

### Fenvi Cards 
As of right now, using Fenvi cards through Proxmox for macOS, you’ll have to stick to Monterey/Ventura and the 5.15.53 kernel is recommended. Especially if you’re using AMD GPU for passthrough.
The 6.2.* kernel will cause the VM to freeze and restart upon connecting to access points.
```
Fenvi FV-HB1200 | Desktop PCI-E (Recommended)
Fenvi T191 | Desktop PCI-E (Recommended)
Fenvi BCM94360NG | M.2 Card
Fenvi BCM94360CD | Desktop PCI-E
WDXUN BCM943602CS | Desktop PCI-E
Fenvi BCM94360NG | Antenna Kit
WIRCARD BCM94360CS2 | M.2 Card
BCM94360CS2 | M.2 Adapter
BCM94360CS2/BCM943224PCIEBT2 | M.2 Adapter
BCM943602CS BCM94360CS2 BCM943224PCIEBT2 BCM94331CD | M.2 to USB Header adapter
```

### USB/Built-In Antennas
```
Alfa AWUS036AC
Alfa AWUS036ACH
Archer T2U Plus (AC600)
Archer T2U NANO, MINI, AC600
Archer T3U
Archer T3U Plus
Archer T2U MINI V3
Archer T2U Plus
ArcherT4U V1, V2, V3
Archer T9UH V1, V2
ASUS USB AC68
ASUS USB-N13
ASUS USB Nano-AC53
BrosTrend FBA_AC3
COMFAST CF-811AC
COMFAST CF-812AC
Comfast CF-758F
Comfast CF-WU810N
Cudy WU1300S
Cudy WU700
Cudy WU650
CXFTEOXK
DLink DWA-121 N150
DLink DWA-131 E
DLink DWA-171 C
DLink DWA-182 D
DLink DWA-192 A
EDIMAX EW-7611UCB
EDIMAX EW-7722UTn V2
EDIMAX_EW-7822ULC
EDIMAX EW-7612Uan V2
EDIMAX EW-7833UAC
EDIMAX N300
EDIMAX EW-7811Un (N150)
EDUP EP-AC1689
Fenvi AC1300 (RTL8812bu)
FILOWA USB WiFi-RTL8812BU
Foktech AC600 Nano
Jensen Eagle 100-AC
Kextech MINI USB RTL8192
Linksys WUSB6300 V2
Linksys WUSB6400M
M-Tech UW-01 USB
Netgear A6100
Netgear A6150
Netgear A7000
Netis WF2120 N Nano USB
Plexgear AC1200
Sitecom WLA7100
TL-WN823Nv2/v3
TL-WN725Nv3
TL-WN723Nv2/v3
TL-WN722Nv2/v3
TL-WN821Nv6
TL-WN822Nv4/v5
TENDA W311-MINI
Tenda U3 Mini
TENDA U12
TRENDnet N150 Micro
TRENDnet TEW-808UBM
TRENDnet TEW-908UB
YUNCLOUD Realtek (RTL8814AU)
ZAPO W58L (RTL881lAU)
```
---
## Compatible GPUs
Avoid these brands; XFX, PowerColor, HIS and VisionTek. As they run a vBIOS that doesn’t work well with macOS.
RTX and GTX 10xx/1xxx NOT supported. No support in macOS Sonoma for Nvidia.
### AMD RX 5000/6000 Cards (Use 5xxx/6xxx EFI Folder)
```
Radeon RX 6950 XT*
*Fake ID spoof required!

Radeon RX 6900 XT*
Compatible
*Be mindful of the XTXH variants. There’s just a handful of them, like the Red Devil card, those need spoofing and can be tricky to get working.

Radeon RX 6800 XT
Compatible

Radeon RX 6800
Compatible

Radeon RX 6650 XT
*Fake ID spoof required

Radeon RX 6600 XT
Compatible

Radeon RX 6600
Compatible

Radeon RX 5700 XT
Compatible

Radeon RX 5700
Compatible

Radeon RX 5600 XT
Compatible

Radeon RX 5600
Compatible

Radeon RX 5500 XT
Compatible

Radeon RX 5500
Compatible
```

### AMD Native Cards (Use Native GPUs EFI Folder)
``` 
Radeon Vega 64*
Temperamental
*Can sometimes be tricky to get fully working with PCI-Passthrough, might get issues with audio.

Radeon Vega 56*
Temperamental
*Can sometimes be tricky to get fully working with PCI-Passthrough, might get issues with audio.

Radeon VII
Compatible

Radeon RX 590
Compatible

Radeon RX 580*
Compatible
2048SP variants (Chinese knock-offs), vBIOS Re-flash required

Radeon RX 570
Compatible

Radeon RX 560X
Compatible

Radeon RX 560
Compatible

Radeon RX 550*
*Baffin Core variants only

Radeon RX 480
Compatible

Radeon RX 470D
Compatible

Radeon RX 470
Compatible

Radeon RX 460
Compatible

Radeon Pro WX 9100
Compatible

Radeon Pro WX 7100
Compatible

Radeon Pro WX 5100
Compatible

Radeon Pro WX 4100
Compatible
```

### Legacy NVIDIA Cards
Please note NVIDIA cards only work with macOS up to Ventura. Sonoma and later is not supported (OCLP patches required)
```
Geforce GTX 780 Ti
Compatible

Geforce GTX 780
Compatible

Geforce GTX 770
Compatible

Geforce GTX 760 Ti
Compatible

Geforce GTX 760
Compatible

Geforce GT 740*
*GK107 variants only

Geforce GT 730*
*GK208 variants only

Geforce GT 720
Compatible

Geforce GT 710*
*GK208 variants only

Geforce GTX 690
Compatible

Geforce GTX 680
Compatible

Geforce GTX 670
Compatible

Geforce GTX 660 Ti
Compatible

Geforce GTX 660*
*GK104 variants only

Geforce GTX 650*
*GK107 variants only

Geforce GT 640*
*GK107 and GK208 variants only

Geforce GT 635
Compatible

Geforce GT 630*
*GK107 and GK208 variants only

Quadro K6000

Quadro K5200

Quadro K5000

Quadro K4200

Quadro K2000D

Quadro K2000

Quadro K600

Quadro K420

Quadro 410
```
