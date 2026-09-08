## Testing the IBERT Example Design

The VMK365 IBERT design helps test the SFP and QSFP interfaces of the board via loopback.
The SFP and QSFP interfaces are on the Banks 204 and 205, respectively.

### Steps to test the hardware design

This section describes the steps to test the IBERT design.

1. Connect to the board and start hardware server using the below command on systest.
    ```bash
    connect "hw_server"
    ```
2. Open Hardware Manager in the Vivado GUI.
3. Click on **Open Target**, on the green banner.
4. Click on **Open New Target**.
5. Select **Remote Server** and provide the Host Name and port number.
6. Click **Program Device** on the green banner. Ensure PDIs and LTX files are being programmed.
7. When device programming completes, the IBERT core should be visible in the hardware panel.

#### Interacting with IBERT Using the Serial I/O Analyzer

1. Go to the **Serial I/O Links** tab and select **Create Links**
2. In this design, each TX and RX channels will be linked together so all available links can be added by clicking the + button until all links are added.
3. Click on **Create**
4. After the links are created, they will be displayed in the **Serial I/O Tabs**. By default, IBERT will default to **User Design** for the TX and RX patterns, allowing user design data to be used. To bring the links up, change the TX and RX patterns for all links to **PRBS 31** by clicking the TX and RX pattern drop down for **Link Group 0**.
5. Next, right-click **Link 0**, and select **Create Scan**.
6. For **Horizontal Increment** and **Vertical Increment**, select 2. Leave all other values default.
7. After the scan finishes, the Eye Diagram will be shown.
