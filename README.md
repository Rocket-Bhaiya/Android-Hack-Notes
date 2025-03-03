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
