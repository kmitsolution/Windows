To create a user group in Active Directory on Windows Server 2019 and configure it to allow logon via Group Policy, follow these steps:

### Step 1: Create a User Group in Active Directory

1. **Open Active Directory Users and Computers:**
   - Press `Windows + R`, type `dsa.msc`, and press `Enter`.

2. **Create a New Group:**
   - In the left pane, navigate to the organizational unit (OU) where you want to create the group.
   - Right-click the OU, select **New**, then choose **Group**.
   - Fill in the group details:
     - **Group name**: Enter a name for the group (e.g., `Remote Desktop Users`).
     - **Group scope**: Choose `Global` or `Universal`, as appropriate.
     - **Group type**: Select `Security`.
   - Click **OK**.

3. **Add Users to the Group:**
   - Right-click the newly created group and select **Properties**.
   - Go to the **Members** tab and click **Add**.
   - Enter the names of users you want to add to this group, then click **OK**.

### Step 2: Allow Logon via Group Policy

1. **Open Group Policy Management Console:**
   - Press `Windows + R`, type `gpmc.msc`, and press `Enter`.

2. **Create or Edit a Group Policy Object (GPO):**
   - Navigate to the OU where you want to link the GPO.
   - Right-click the OU and select **Create a GPO in this domain, and Link it here** or select an existing GPO and click **Edit**.

3. **Configure Remote Desktop Settings:**
   - In the Group Policy Management Editor, navigate to:
     ```
     Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> User Rights Assignment
     ```

4. **Modify Logon Rights:**
   - Double-click on **Allow log on through Remote Desktop Services**.
   - Click **Add User or Group**.
   - Type the name of the group you created (e.g., `Remote Desktop Users`), then click **OK**.

5. **Enable Remote Desktop Connections:**
   - Navigate to:
     ```
     Computer Configuration -> Policies -> Administrative Templates -> Windows Components -> Remote Desktop Services -> Remote Desktop Session Host -> Connections
     ```
   - Double-click **Allow users to connect remotely using Remote Desktop Services**.
   - Set it to **Enabled**, then click **OK**.

### Step 3: Refresh Group Policy

1. Open Command Prompt on the server and run:
   ```bash
   gpupdate /force
   ```

### Step 4: Verify Configuration

1. **Check Remote Desktop Settings:**
   - Right-click on **This PC** or **My Computer**, select **Properties**.
   - Click on **Remote settings** on the left.
   - Ensure that **Allow remote connections to this computer** is selected.

2. **Check Firewall Settings:**
   - Open **Windows Defender Firewall with Advanced Security**.
   - Ensure that the rule for **Remote Desktop - User Mode (TCP-In)** is enabled.

### Conclusion

Once these steps are completed, users who are members of the group you created will have the permissions to log on via Remote Desktop. Test the setup to ensure everything is working as expected.
