# atitool

atitool is a console utility to control and monitor AMD GPU device operating parameters.

---

- Clock and Voltage management
- PowerPlay support
- Device information and status reporting
- I2C operations off GPU
- MC control/status
- GRBM soft reset
- PCIE control/status
- Serial ID reporting
- HDCP A-Key reporting

## Software and Hardware Requirements

`atitool` requires a supported AMD GPU device and Linux to function.

## Installation

Decompress `atitool.tar.xz` package under designated folder. Run `atitool` as executable file while making sure the user has administrative rights.

## Help

For help execute `atitool` without parameters.

- `./atitool clock` Displays options for clock operations
- `./atitool powerplay` Displays options for PowerPlay operations
- `./atitool pcie` Displays options for PCIE operations
- `./atitool vctf` Displays options for Voltage/Current/Thermal/Fan control
- `./atitool sid` Displays options for ASIC Serial ID
- `./atitool mc` Displays options for memory controller settings
- `./atitool flash` Displays options for ROM operations
- `./atitool display` Displays options for Display operations
- `./atitool clockoutput` Displays options for clock observation operations
- `./atitool reset` Displays options for reset operations
- `./atitool efuse` Displays options for verifying EFUSE infomation
- `./atitool hwid` Displays options for various ASIC/Board related info
- `./atitool baco` Displays options for BACO (Bus Alive Chip Off) operations
- `./atitool cail` Displays options for CAIL (Common ASIC Init Library) operations
- `./atitool fw` Displays options for firmware related operations for SMC and micro engines
- `./atitool btc` Displays options for Boot Time Caibration and Power Supply Monitor logging
- `./atitool pace` Displays options for getting/setting PACE table
- `./atitool pm` Displays options for Power Management parameters logging
- `./atitool gpustatus` Displays options for GPU status
- `./atitool raserrortest` Displays options for RAS error injection/detection and error counters

## Commands

- `./atitool -v=silent` Run ATITOOL in silent mode with no screen output
- `./atitool -UseVbiosImage{=<filename>}` Use vbios image from a file
- `./atitool -DumpVbiosImage{=<filename>}` Dump vbios image to a file
- `./atitool -i` Displays a list of all present ATI graphics devices
- `./atitool -i=<#>` Select a target device to apply commands. Supports both simple index (reported by `-i`) and PCI location (`-i=PCI:<bn>.<dn>.<fn>`)
- `./atitool -usefinddevice` Debug flag to target a specific device (requires `-i=PCI:xx.yy.zz`)
- `./atitool -asicinit` Initialize ASIC into working state (ie. secondary GPU) Can be combined with `-i=<#>`
- `./atitool -forceasicinit` Initialize ASIC into working state even if it's already initialized
- `./atitool -skipvbiospost` Do not perform VBIOS post on uninitialized GPUs
- `./atitool -sriovLoadUcode` Load SRIOV Ucodes. Applies to -asicinit.
- `./atitool -debug=<#>` Enable debug logging (generates `TOOL.LOG`), `<#> = verbosity`
- `./atitool -logpath=<#>` Specify location of debug log file (`TOOL.LOG`)
- `./atitool -logtoconsole` Content sent to debug log (`TOOL.LOG`) is redirected to console. Useful on read only filesystems
- `./atitool -pxversion` Check the PowerXpress version of the system
- `./atitool -boardid=<#>` Override board ID with given string. Useful when VBIOS image is missing board ID string

## Usage

Please note that not all command line options listed below are applicable to all supported ASICs.

```sh
./atitool clock
```

Output:

- `-clkstatus` Display BIOS default and current clock values
- `-clklog` Log output to a file called `ATICLK.LOG`
- `-clksave=fn` Save clock settings to a file `fn` (file name is optional where default name is `clkstat.inf`)
- `-clkappend=fn` Append clock settings to a file `fn` (file name is optional where default name is `clkstat.inf`)
- `-clkload=fn` Load clock settings from a file `fn` (file name is optional where default name is `clkstat.inf`)
- `-eng=<#>` Set Engine clock (SCLK in fusion) to new value `#` (MHz)
- `-mem=<#>` Set Memory clock to new value `#` (MHz)
- `-socclk=<#>` Set SOC clock to a new value `#` (MHz)
- `-clkrestore` Restore to BIOS default values
- `-incclk=<#>` Increase mem/eng clock to BIOS default + delta `#` (MHz)
- `-decclk=<#>` Decrease mem/eng clock to BIOS default - delta `#` (MHz)
- `-incmclk=<#>` Increase mem clock to current clk + delta `#` (MHz)
- `-incsclk=<#>` Increase eng clock to current clk + delta `#` (MHz)
- `-incmclkpct=<#>` Increase mem clock by # percent of current clk (MHz)
- `-incsclkpct=<#>` Increase eng clock by # percent of current clk (MHz)
- `-decmclk=<#>` Decrease mem clock to current clk - delta `#` (MHz)
- `-decsclk=<#>` Decrease eng clock to current clk - delta `#` (MHz)
- `-biosclkctrl` Use AtomBIOS to change engine clock
- `-clkinst=<#>` Specify clock instance for multi instance clocks
- `-allinst` Set clock on all instances for multi instance clocks
- `-adjpll` Adjust PLL to change clock
- `-favordclk` Favor DCLK over VCLK
- `-favorvclk` Favor VCLK over DCLK
- `-clkcounter` Display clock counters
- `-dyngfx=<on/off>` Enable/Disable dynamic gfx clock gating
- `-test:memeq=<#>` Is current memory clock = `#`?
- `-test:memgt=<#>` Is current memory clock > `#`?
- `-test:memlt=<#>` Is current memory clock < `#`?
- `-test:engeq=<#>` Is current engine clock = `#`?
- `-test:enggt=<#>` Is current engine clock > `#`?
- `-test:englt=<#>` Is current engine clock < `#`?
- `-dclk=<#>` Set UVD DCLK to new value `#` (MHz)
- `-vclk=<#>` Set UVD VCLK to new value `#` (MHz)
- `-maxvco=<#>` Specify UPLL VCO limit (MHz) for DCLK/VCLK
- `-uvdclkstatus=<#>`  UVD clock gating status : On,Off
- `-skipmemparam` Skip memory parameter changes
- `-skipmempll` Skip memory PLL reprogramming
- `-gteq` Set mem/eng clock to a value >= the value specified. For use with insclkpct/incmclkpct
- `-lclk=<#>` Set LCLK to a new value `#` (Mhz)
- `-eclk=<#>` Set VCE ECLK (APU) to a new value `#` (Mhz)
- `-ecclk=<#>` Set VCE ECCLK to new value `#` (MHz)
- `-evclk=<#>` Set VCE EVCLK to new value `#` (MHz)
- `-favorecclk` Favor ECCLK over EVCLK
- `-favorevclk` Favor EVCLK over ECCLK
- `-maxvcovce=<#>` Specify VCEPLL VCO limit (MHz) for ECCLK/EVCLK
- `-aclk=<#>` Set ACP CLK to a new value `#` (Mhz)
- `-samclk=<#>` Set SAMU CLK to a new value `#` (Mhz)
- `-pspclk=<#>` Set PSP CLK to a new value `#` (Mhz)
- `-smnclk=<#>` Set SMN CLK to a new value `#` (Mhz)
- `-smcclk=<#>` Set SMC CLK to a new value `#` (Mhz)
- `-dcefclk=<#>` Set DCEF CLK to a new value `#` (MHz)
- `-ispclk=<#>` Set ISP CLK to a new value `#` (MHz)
- `-sfhclk=<#>` Set SFH (Sensor Fusion Hub) CLK to a new value `#` (MHz)
- `-shubclk=<#>` Set SHUBCLK to a new value `#` (MHz)
- `-fclk=<#>` Set FCLK to a new value `#` (MHz)
- `-dispclk=<#>` Set DISPLCLK to a new value `#` (Mhz)
- `-dppclk=<#>` Set DPPLCLK to a new value `#` (Mhz)
- `-usbdfsclk=<#>` Set USBDFSLCLK to a new value `#` (Mhz)
- `-sclkdiv=<#>` Set SCLK DFS divider
- `-lclkdiv=<#>` Set LCLK DFS divider
- `-vclkdiv=<#>` Set VCLK DFS divider
- `-dclkdiv=<#>` Set DCLK DFS divider
- `-eclkdiv=<#>` Set ECLK DFS divider
- `-aclkdiv=<#>` Set ACLK DFS divider
- `-samclkdiv=<#>` Set SAMCLK DFS divider
- `-pspclkdiv=<#>` Set PSPCLK DFS divider
- `-dispclkdiv=<#>` Set DISPCLK DFS divider
- `-smnclkdiv=<#>` Set SMNCLK DFS divider
- `-smcclkdiv=<#>` Set SMCCLK DFS divider
- `-dcefclkdiv=<#>` Set DCEFCLK DFS divider
- `-ispclkdiv=<#>` Set ISPCLK DFS divider
- `-sfhclkdiv=<#>` Set SFHFCLK DFS divider
- `-shubclkdiv=<#>` Set SHUBCLK DFS divider
- `-clockinfo` Show current clock status in full screen mode, continuously refreshed. Requires terminal emulation.
- `-refresh=#` Applies to clockinfo. Screen refresh period in ms.
- `-enablecks` Enable CKS when SCLK change is requested.
- `-cksstatus` Show current CKS status.
- `-bypassffcdisable`  not disable FFC on MCLK changes.
- `-enableacg` Use ACG for clock change (if supported)
- `-useafll` Use AFLL for clock change (if supported)
- `-gcea` Apply GCEA settings after changing GFXCLK/MCLK (if supported)
