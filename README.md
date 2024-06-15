# AZURE-VIRTUAL-MACHINE
# Setting Up an Ubuntu VM with GUI on Azure

This project will guide you to create an Ubuntu Virtual Machine (VM) on Azure, install a GUI, configure an RDP server, and connect to it using Remote Desktop Protocol (RDP).

## Prerequisites

- An active Azure account.
- Basic knowledge of Azure portal and SSH.

## Step-by-Step Guide

### 1. Create a Virtual Machine

1. **Open the Azure portal** and navigate to **Virtual Machines**.
2. Click **Add** and choose **Linux** for the operating system.
3. Select **Ubuntu** for the image and choose your desired version (LTS versions recommended for stability).
4. Configure VM settings:
   - **Name**: Provide a name for your VM.
   - **Resource Group**: Select an existing resource group or create a new one.
   - **Region**: Choose the region closest to you.
   - **Size**: Select a VM size based on your requirements.
   - **Storage**: Configure the storage settings as needed.

### 2. Install the GUI

RDP typically requires a graphical desktop environment (GUI). By default, Ubuntu VMs in Azure are server versions without a GUI.

1. After creating the VM, go to **Connect** and choose **SSH**.
2. Use the username and password you provided during VM creation to connect via SSH.
3. Once connected via SSH, update the package lists:
   ```bash
   sudo apt update
   ```
4. Install the GUI (e.g., Xfce):
   ```bash
   sudo apt install xfce4 xfce4-goodies -y
   ```

### 3. Configure RDP Server

1. Install the `xrdp` package to enable RDP connections:
   ```bash
   sudo apt install xrdp -y
   ```
2. Start the xrdp service and enable it to start on boot:
   ```bash
   sudo systemctl enable xrdp
   sudo systemctl start xrdp
   ```
3. Add the xrdp user to the `ssl-cert` group:
   ```bash
   sudo adduser xrdp ssl-cert
   ```

### 4. Secure Remote Access

1. Configure the firewall to allow RDP connections:
   ```bash
   sudo ufw allow 3389
   sudo ufw enable
   ```

### 5. Connect with RDP

1. Find the Public IP address of your VM in the Azure portal overview.
2. On your local Windows machine, open **Remote Desktop Connection**.
3. Enter the VM's Public IP address and click **Connect**.
4. You'll be prompted for the username and password you created during VM creation.

## Additional Notes

- Ensure your VM size has sufficient resources (CPU, RAM) to run a GUI.
- For better security, consider setting up an SSH key pair instead of using a password.

## Troubleshooting

- If you encounter connection issues, verify the firewall settings and ensure the xrdp service is running.
- Check the network security group (NSG) rules in Azure to ensure port 3389 is open.

## References

- [Azure Virtual Machines Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/)
- [XRDP Documentation](http://www.xrdp.org/)



Happy virtualizing! 🚀

