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
