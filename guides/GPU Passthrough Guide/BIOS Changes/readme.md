# BIOS Configuration for Passthrough

Make sure your BIOS is on its latest update.

---

✅ **Enable SVM/Virtualization Mode**

✅ **Enable VT-d**  
_Required for passthrough to work at all; [supported CPUs](https://hsve.cc/supporteddevices)._

✅ **Enable SR-IOV**  
_If present._

❌ **Disable CSM/Legacy Boot**

✅ **Enable ACS**  
_If present, set to Enabled (Auto doesn’t work)._

✅ **Set PEG {NUMBER} ASPM to L0 or L0sL1**  
_Set whichever amount you've got to mentioned, if L0 is present, pick that._

✅ **Enable 4G Decoding**

❌ **Disable Resizable BAR/Smart Access Memory**  
_You might experience ‘Code 43 error’ if enabled._

✅ **Enable IOMMU**  
_If present, mostly for AMD boards; [supported CPUs](https://hsve.cc/supporteddevices)._

✅ **Set Primary Display to CPU/iGPU**  
_If your CPU has an iGPU, if not skip this._

✅ **Set Pre-Allocated Memory to 64M**  
_If your CPU has an iGPU, if not skip this too._
