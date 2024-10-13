Configuring DNS in Active Directory Domain Services (AD DS) involves setting up forward and reverse lookup zones, which are essential for name resolution in your network. Here’s how to do it step-by-step:

### Step 1: Open DNS Manager

1. **Open Server Manager**.
2. Click on **Tools** and select **DNS** from the dropdown.

### Step 2: Configure a Forward Lookup Zone

1. In the **DNS Manager** console, expand the server node.
2. Right-click on **Forward Lookup Zones** and select **New Zone**.
3. **New Zone Wizard** will open. Click **Next**.
4. Choose the zone type:
   - **Primary zone** (recommended for AD-integrated zones).
   - Click **Next**.
5. Select **Store the zone in Active Directory** if this is an AD-integrated zone.
6. Choose the replication scope (e.g., **To all DNS servers in the Active Directory domain**).
7. Click **Next**.
8. Enter the **Zone Name** (e.g., `example.com`).
9. Configure any additional options as required (e.g., Dynamic updates).
10. Click **Next**, then **Finish**.

### Step 3: Add DNS Records to the Forward Lookup Zone

1. In the **DNS Manager**, expand the newly created zone.
2. Right-click on the zone (e.g., `example.com`) and select **New Host (A or AAAA)**.
3. Enter the **Name** (e.g., `www` for `www.example.com`) and the **IP Address**.
4. Click **Add Host**.
5. Repeat to add additional records as necessary (e.g., mail server).

### Step 4: Configure a Reverse Lookup Zone

1. Right-click on **Reverse Lookup Zones** and select **New Zone**.
2. Click **Next** in the **New Zone Wizard**.
3. Choose **Primary zone** and click **Next**.
4. Select **Store the zone in Active Directory** if required.
5. Choose the replication scope and click **Next**.
6. Specify the **Network ID** (e.g., `192.168.1` for a subnet of `192.168.1.0/24`).
7. Click **Next** and configure dynamic updates as needed.
8. Click **Finish**.

### Step 5: Add PTR Records to the Reverse Lookup Zone

1. In the **DNS Manager**, expand the reverse lookup zone you just created.
2. Right-click on the zone and select **New Pointer (PTR)**.
3. In the **New Resource Record** window, enter the **Host IP Address** (e.g., `192.168.1.10`).
4. In the **Host Name** field, enter the fully qualified domain name (FQDN) (e.g., `www.example.com`).
5. Click **OK**.

### Step 6: Verify DNS Configuration

1. Open a Command Prompt.
2. Use `nslookup` to verify that the forward and reverse lookups are functioning:
   ```bash
   nslookup www.example.com
   nslookup 192.168.1.10
   ```

### Conclusion

You’ve successfully configured both forward and reverse lookup zones in Active Directory DNS, added necessary records, and verified your configuration. This setup is crucial for enabling name resolution within your network and for services like Active Directory.
