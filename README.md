# tmp1 

## VMK365 Hardware Designs

The VMK365  hardware designs target the following paths:

- **VMK365_hdmi_single**:<br>
	HDMI Rx -> Scaler -> Frmbuf Wr -> DDR -> Frmbuf Rd-> Vmixer -> HDMI Tx<br>
	HDMI Rx -> Scaler -> Frmbuf Wr -> DDR -> Vmixer -> HDMI Tx
- **VMK365_hdmi_brcstr**: HDMI Rx -> Scaler -> AXI Broadcaster -> Frmbuf Wr -> DDR -> Frmbuf Rd -> Vmixer -> HDMI Tx
- **VMK365_hdmi_single_PMOD**: Loopback Design to test the PMOD interfaces.
- **vmk365_sdi0_rxtx**: SDI Rx0 -> Scaler -> Frmbuf Wr -> DDR -> Frmbuf Rd-> SDI Tx0
- **vmk365_sdi1_rxtx**: SDI Rx1 -> Scaler -> Frmbuf Wr -> DDR -> Frmbuf Rd-> SDI Tx1
- **vmk365_sdi2_rxtx**: SDI Rx2 -> Scaler -> Frmbuf Wr -> DDR -> Frmbuf Rd-> SDI Tx2
- **vmk365_sdi3_rxtx**: SDI Rx3 -> Scaler -> Frmbuf Wr -> DDR -> Frmbuf Rd-> SDI Tx3
- **vmk365_hdmitx_sdi4rx**: 4 SDI Rx interfaces -> Scaler -> Frmbuf Wr -> DDR -> Frmbuf Rd-> Vmixer -> HDMI Tx	

### Vivado Tool Version
- **Vivado™ 2026.2**

### Steps to build the hardware design

This section describes the steps required to build the hardware designs.

1. Navigate to the design folder that you want to recreate.
2. Source the vivado tool.
	```bash
	   source /proj/primebuilds/2026.2_PRIME_0609_1/installs/lin64/9999.0/Vivado/settings64.csh
	```   
3. Run the following command.
	```bash
	vivado -source <bd>.tcl &
	```
   This opens up the GUI and recreates the block design.
4. Click on Generate Bitstream. This starts the runs.
5. Hack the PDIs.
    ```bash
	cd .../*.runs/impl_1/gen_files/ 
	vi lpd_data.cdo
	```
Under the Boot Up Procedure, Add the following lines.
	```bash
	# pm_init_node(POWER_LPD, 0)
	log_string "HC Disabled"
	write 0xF2014170 0xFF2FF7FF
	write 0xF2014174 0xF7FFFFF7
	```
Save the file and comeback to the impl_1 folder. Run the following command to generate the PDIs again.
	```bash
	/proj/primebuilds/HEAD_PRIME_daily_latest/installs/lin64/HEAD/Vivado/bin/bootgen -arch versal_2ve_2vm -padimageheader=0 -log trace -image design_1_wrapper_boot.bif  -w -o design_1_wrapper_boot.pdi
	```

6. Export the Hardware.
	```bash
	File -> Export -> Export Hardware -> Include Device Image -> Export
