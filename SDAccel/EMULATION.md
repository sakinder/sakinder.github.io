Running Software and Hardware Emulation in XOCC Flow
In the XOCC/Makefile flow, users manage compilation and execution of host code and kernels
outside the Xilinx® SDAccel™ development environment. Follow the steps below to run
software and hardware emulation:
1. Create the emulation configuration file.
For software or hardware emmulation, the runtime library needs to know what devices and
how many to emulate. This information is provided to the runtime library by an emulation
configuration file. SDAccel provides a utility, emconfigutil to automate creation of the
emulation configuration file.
The emconfigutil command creates the configuration file emconfig.json in the output directory.
The emconfig.json file must be in the same directory as the host executable.
The following example creates a configuration file targeting two xilinx:adm-pcie-7v3:1ddr:3.0 devices.
2. Set XILINX_SDX environment variable
The XILINX_SDX environment needs to be set and pointed to the SDAccel installation path for the emulation to work. 
> **Below are examples assuming SDAccel is installed in /opt/Xilinx/SDx/2016.3**
* C Shell:
```setenv XILINX_SDX /opt/Xilinx/SDx/2016.3```
* Bash:
```export XILINX_SDX=/opt/Xilinx/SDx/2016.3```
3. Set emulation mode
Setting XCL_EMULATION_MODE environment variable to 1 or true changes the application
execution to emulation mode so that the runtime looks for the file emconfig.json in the
same directory as the host executable and reads in the target configuration for the emulation
runs.
C Shell:
setenv XCL_EMULATION_MODE true
Bash:
export  XCL_EMULATION_MODE=true
Setting the XCL_EMULATION_MODE environment variable to 0 or false, or unsetting it will
turn off the emulation mode.
4. Run CPU and hardware emulation
With the configuration file emconfig.json and XCL_EMULATION_MODE set to true, execute
the host application with proper arguments to run CPU and hardware emulation:
$./host.exe kernel.xclbin
## Running Application on FPGA
Use the following steps to run an application on an FPGA device with host executable and kernel
binaries compiled in the XOCC flow.
1. Source the setup.sh (Bash) or setup.csh (Csh/Tcsh) script file generated by the xbinst
utility. See Board Installation chapter for more details.
2. Run the application:$./host.exe kernel.xclbin