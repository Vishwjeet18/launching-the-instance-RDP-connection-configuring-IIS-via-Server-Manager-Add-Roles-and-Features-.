# launching-the-instance-RDP-connection-configuring-IIS-via-Server-Manager-Add-Roles-and-Features-.



---

## **1. Launch a Windows Server EC2 Instance**

1. **Go to AWS Console → EC2 → Launch Instance**.
2. **Name your instance** → e.g., `IIS-Windows-Server`.
3. **AMI (Amazon Machine Image)** → Choose **Microsoft Windows Server** (2019, 2022, or similar).
4. **Instance type** → Minimum **t2.micro** (for free tier) or higher.
5. **Key pair** → Select existing or create a new `.pem` key (for password decryption later).
6. **Network settings**:

   * Allow **RDP (port 3389)**.
   * Allow **HTTP (port 80)** if you want public website access.
   * Allow **HTTPS (port 443)** if you need SSL.
7. **Launch instance**.

---

## **2. Get RDP Connection Details**

1. Go to **EC2 → Instances** → Select your Windows instance.
2. Click **Connect** → Choose **RDP Client** tab.
3. Click **Get Password**.
4. Upload your **.pem key** → Click **Decrypt Password** → Copy the password.
5. Copy the **Public IPv4 address** of the instance.

---

## **3. Connect via RDP**

1. On your local PC, press **Win + R** → type `mstsc` → Enter.
2. Enter **Public IPv4 address** → Click **Connect**.
3. Username = **Administrator**
   Password = **Decrypted password from AWS**.
4. Click **Yes** on security prompt → You’re now inside your Windows Server EC2.

---

## **4. Add IIS via Server Manager**

1. Once inside the server, **Server Manager** opens automatically.
2. Click **Add roles and features**.
3. **Before You Begin** → Click **Next**.
4. **Installation Type** → Select **Role-based or feature-based installation** → Next.
5. **Server Selection** → Ensure your EC2 is selected → Next.
6. **Server Roles**:

   * Tick **Web Server (IIS)**.
   * Add features if prompted.
7. **Features** → Keep defaults → Next.
8. **Role Services**:

   * Default Web Server → Leave default or add **ASP.NET**, **FTP Server**, etc., if needed.
9. Click **Install** → Wait for completion → Close.

---

## **5. Test IIS**

1. Open a browser **inside the server** → type `http://localhost` → You should see the IIS welcome page.
2. To test externally:

   * On your local PC, open browser → type `http://<Public IPv4>` → IIS welcome page should appear.
   * If it doesn’t, ensure **Security Group** has **port 80** open.

---

## **6. Common Paths & Management**

* **Default Web Directory**: `C:\inetpub\wwwroot`
* **IIS Manager**: Press **Windows Key → type "IIS" → Internet Information Services (IIS) Manager**.


✅ This process gives you a **fully working IIS web server** on EC2 with RDP access.
If you want, I can also give you a **diagram + quick command checklist** so you can do this setup in under 10 minutes.
