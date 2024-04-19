# 1. Obtaining the Dynamic Server Address

1. Open Command Prompt.
2. Use the `IPCONFIG` command to find the server's IP address (IPv4 Address), for example, 192.168.153.130.

---

# 2. Setting a Static IP Address

1. Open the Initial Configuration Task.
2. Click on "Configure Networking".
3. Uncheck IPv6 and then IPv4.
4. Insert the server's IP address and subnet mask.
5. Click OK.

---

# 3. Enabling Automatic Updates and Remote Desktop Connection

1. In the Initial Configuration Task, click on "Enable automatic update and feedback".
2. In the Initial Configuration Task, click on "Enable Remote Desktop" and select "Allow connections".

---

# 4. Turning Off the Firewall

1. Open the Configure Windows Firewall.
2. Select the option "Turn off Windows Firewall".

---

# 5. Setting the Computer Name and Domain

1. Click on "Change" next to "Provide computer name and domain".
2. Change the computer name.
3. Restart the system.

---

# 6. Installing Active Directory Domain Services

1. Open Server Manager.
2. Click on "Roles" and then "Add Roles".
3. Select "Active Directory Domain Services" and follow the on-screen instructions.

---

# 7. Configuring the DHCP Server

1. Open Server Manager.
2. Click on "Roles" and then "Add Roles".
3. Select "DHCP server" and follow the on-screen instructions.

---

# 8. Configuring Remote Desktop Services

1. Open Server Manager.
2. Click on "Roles" and then "Add Roles".
3. Select the necessary services for Remote Desktop.
4. Follow the on-screen instructions.

---

# 9. Configuring IPv4 DNS Server

1. Open the Server Manager.
2. Navigate to "Roles" and then "Add Roles".
3. Select "DNS Server" and follow the on-screen instructions to configure it.

---

# 10. Turning off Windows Firewall

1. Open the "Control Panel" and navigate to "System and Security".
2. Click on "Windows Firewall" and then "Turn Windows Firewall on or off".
3. Turn off Windows Firewall for all network profiles.

---

# 11. Configuring DNS Server for IPv4

1. Open the Server Manager.
2. Navigate to "Roles" and then "DNS Server".
3. Configure the DNS server settings for IPv4 by setting the IP address of the server.

---

# 12. Configuring Additional Roles and Features

1. Open the Server Manager.
2. Navigate to "Roles" and then "Add Roles".
3. Select any additional roles and features required for your server setup.

---

# 13. Defining Organizational Units in Active Directory

1. Open the "Active Directory Users and Computers" tool from the Administrative Tools menu.
2. Right-click on the domain name and select "New Organizational Unit".
3. Specify the name of the organizational unit and click "OK".

---

# 14. Creating Users in Active Directory

1. Open the "Active Directory Users and Computers" tool from the Administrative Tools menu.
2. Right-click on the organizational unit where you want to create the user.
3. Select "New" and then "User".
4. Fill in the user details and click "Finish" to create the user.

---

# 15. Defining Shared Storage Space on the Server

1. Open "File Explorer" and navigate to the drive where you want to create the shared folder.
2. Right-click and select "New" > "Folder" to create a new folder.
3. Right-click on the folder, select "Properties", and then go to the "Sharing" tab.
4. Click on "Share", select the appropriate permissions, and click "Share".

---

# 16. Mapping Network Drives

1. Open "File Explorer".
2. Click on "This PC".
3. Click on "Map network drive".
4. Choose a drive letter and enter the path of the shared folder.
5. Check the box "Reconnect at sign-in" if needed, and click "Finish".

---

# 17. Enabling Remote Desktop Access on the Server

1. Open "Control Panel".
2. Navigate to "System" and click on "Remote settings".
3. Under the "Remote" tab, select "Allow remote connections to this computer".
4. Click on "Select Users" and add the users who will have remote access.
5. Click "Apply" and then "OK" to save the changes.

---

# 18. Configuring Windows Firewall for Remote Desktop Access

1. Open "Control Panel".
2. Navigate to "System and Security" and click on "Windows Firewall".
3. Click on "Allow an app or feature through Windows Firewall".
4. Ensure that "Remote Desktop" is allowed for all network types.

---

# 19. Checking Remote Access from Server to PC

1. Open "Remote Desktop Connection" on the server.
2. Enter the IP address or hostname of the PC.
3. Click "Connect" and enter the credentials if prompted.
4. Ensure that the remote connection is successful.

---

# 20. Checking Remote Access from PC to Server

1. Open "Remote Desktop Connection" on the PC.
2. Enter the IP address or hostname of the server.
3. Click "Connect" and enter the credentials if prompted.
4. Ensure that the remote connection is successful.

---

# 21. Applying Password Policy Restrictions

1. Open "Group Policy Management" on the server.
2. Navigate to the appropriate Group Policy Object (e.g., Default Domain Policy).
3. Edit the policy and configure password policy settings such as minimum length and complexity requirements.
4. Apply the changes and force a group policy update if necessary.

---

# 22. Enforcing Group Policy Update

1. Open Command Prompt with administrative privileges.
2. Run the command `gpupdate /force` to enforce a group policy update on the server.
3. Wait for the update to complete.

---

# 23. Verifying Remote Access Functionality

1. Test remote access from the server to PC and vice versa using Remote Desktop Connection.
2. Ensure that users can log in successfully with their credentials.
3. Verify that network resources can be accessed remotely.

---

# 24. Completing the Installation and Configuration

1. Review all configurations and settings to ensure they are correctly applied.
2. Perform any additional testing or verification as necessary.
3. Document the setup for future reference.
4. Close all open applications and restart the server if needed.

