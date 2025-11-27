## claude Code + Gemini - Complete Setup Guide
# Beginner se Professional 

---

## 📋 **Requirement Check Karo**

### ✅ **Pehle ye check karo:**
1. Windows 10/11 hai?
2. Internet connection hai?
3. Administrator access hai?

---

## 🚀 **PART 1: Node.js Install Karo**

### **Step 1: Download Karo**
1. Browser mein jao: https://nodejs.org
2. **LTS version** (Left wala green button) download karo
3. File download hogi (approx 30MB)

### **Step 2: Install Karo**
1. Downloaded file pe double-click karo
2. "Next" dabate jao
3. Sab kuch **default** rakho
4. "Install" karo
5. Khatam hone ka wait karo (2-3 minute)

### **Step 3: Verify Karo**
**PowerShell** kholo (Windows Search mein "PowerShell" type karo) aur likho:

```powershell
node --version
```

**Agar ye dikha:**
```
v20.x.x
```
✅ **Perfect! Next step pe jao**

---

## 🔑 **PART 2: Google Gemini API Key Banao**

### **Step 1: Google Account se Login**
1. Browser mein jao: https://aistudio.google.com/apikey
2. Apne Google account se sign in karo

### **Step 2: API Key Create Karo**
1. **"Create API Key"** button pe click karo
2. **"Create API key in new project"** select karo
3. Key copy karo (ye aisi hogi: `AIzaSyDXXXXXXXXXXXXXXXXXXXXXXX`)

### **Step 3: Key Safe Rakho**
📝 Notepad mein paste kar ke save kar lo (baad mein chahiye hogi)

✅ **Done! Next step**

---

## 💻 **PART 3: Claude Code Install Karo**

### **Step 1: PowerShell Kholo (Administrator mode)**
1. Windows Search mein **"PowerShell"** likho
2. Right-click karo → **"Run as Administrator"** select karo
3. Blue window khulegi

### **Step 2: Claude Code Install Karo**
Is command ko copy-paste karo:

```powershell
npm install -g @musistudio/claude-code
```

**Wait karo** (2-3 minute lagenge). Jab khatam ho:

### **Step 3: Verify Karo**
```powershell
claude --version
```

**Ye dikha:**
```
2.0.x (Claude Code)
```
✅ **Perfect!**

---

## 🔧 **PART 4: Router Install Karo**

### **Step 1: Router Install**
Same PowerShell mein:

```powershell
npm install -g @musistudio/claude-code-router
```

Wait karo (1-2 minute).

### **Step 2: Verify**
```powershell
ccr --version
```

**Output aisa hoga:**
```
1.x.x
```
✅ **Done!**

---

## ⚙️ **PART 5: Configuration Setup (SABSE IMPORTANT)**

### **Step 1: Config Folder Banao**
PowerShell mein ye commands chalaao:

```powershell
# Config folder banao
mkdir "$env:USERPROFILE\.claude-code-router" -Force
```

### **Step 2: Config File Banao**
**Pura code copy karo** aur PowerShell mein paste kar ke Enter dabao:

```powershell
@"
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "`$GOOGLE_API_KEY",
      "models": [
        "gemini-2.0-flash-exp",
        "gemini-1.5-flash",
        "gemini-1.5-pro"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-2.0-flash-exp",
    "background": "gemini,gemini-2.0-flash-exp",
    "think": "gemini,gemini-2.0-flash-exp",
    "longContext": "gemini,gemini-1.5-pro",
    "longContextThreshold": 60000
  }
}
"@ | Out-File -FilePath "$env:USERPROFILE\.claude-code-router\config.json" -Encoding UTF8
```

✅ **Config file ban gayi!**

---

## 🔐 **PART 6: Environment Variables Set Karo**

### **⚠️ BAHUT IMPORTANT STEP - DHYAN SE KARO**

PowerShell mein ye commands **ek ek kar ke** chalaao:

### **Step 1: Google API Key Set Karo**
```powershell
[System.Environment]::SetEnvironmentVariable("GOOGLE_API_KEY", "YAHAN_APNI_GOOGLE_KEY_LAGAO", "User")
```

**⚠️ IMPORTANT:** `YAHAN_APNI_GOOGLE_KEY_LAGAO` ko apni actual Google API key se replace karo!

**Example:**
```powershell
[System.Environment]::SetEnvironmentVariable("GOOGLE_API_KEY", "AIzaSyDabcdef123456789", "User")
```

### **Step 2: Base URL Set Karo**
```powershell
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "http://127.0.0.1:3456", "User")
```

### **Step 3: Dummy API Key Set Karo**
```powershell
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "sk-ant-dummy-key", "User")
```

✅ **Sab set ho gaya!**

---

## 🔄 **PART 7: PowerShell Restart Karo**

### **BAHUT ZARURI:**
1. Abhi wali PowerShell window **band** kar do
2. **Naya PowerShell** kholo (Administrator mode mein)
3. Ye environment variables load honge

---

## ✅ **PART 8: Verify Karo - Sab Sahi Hai?**

Naye PowerShell mein ye commands chalaao:

### **Check 1: Google Key**
```powershell
echo $env:GOOGLE_API_KEY
```
**Aapki Google key dikh rahi hai?** ✅

### **Check 2: Base URL**
```powershell
echo $env:ANTHROPIC_BASE_URL
```
**Output:** `http://127.0.0.1:3456` ✅

### **Check 3: Dummy Key**
```powershell
echo $env:ANTHROPIC_API_KEY
```
**Output:** `sk-ant-dummy-key` ✅

**Agar sab sahi hai to next step!**

---

## 🎯 **PART 9: Router Start Karo**

### **Step 1: Router Chalaao**
```cmd
ccr start
```

**Ye dikha:**
```
✅ Service started successfully
```

### **Step 2: Status Check**
```cmd
ccr status
```

**Output:**
```
✅ Service is running
```

🎉 **PERFECT! Router chal raha hai!**

---

## 🧪 **PART 10: FINAL TEST - Claude Code Chalaao!**

### **Step 1: Test Folder Banao**
```cmd
cd Desktop
mkdir test-project
cd test-project
```

### **Step 2: Claude Code Start Karo**
```cmd
claude
```

**Ye screen dikhe gi:**
```
Claude Code v2.0.55
Welcome back!
```

### **Step 3: Test Message Bhejo**
Claude interface mein likho:
```
hi, write a hello world program in python
```

**Agar response aaya to** 🎉🎉🎉
### ✅ **SUCCESSFULLY SETUP HO GAYA!!!**

---

## 🛠️ **TROUBLESHOOTING - Agar Problem Ho**

### **Problem 1: "Invalid API key"**
**Solution:**
```powershell
# Check karo key sahi hai
echo $env:GOOGLE_API_KEY

# Agar galat hai to dobara set karo
[System.Environment]::SetEnvironmentVariable("GOOGLE_API_KEY", "SAHI_KEY_YAHAN", "User")

# PowerShell restart karo
```

---

### **Problem 2: "Connection refused"**
**Solution:**
```cmd
# Router stop karo
ccr stop

# Dobara start karo
ccr start

# Status check karo
ccr status
```

---

### **Problem 3: Router nahi chal raha**
**Solution:**
```cmd
# Logs dekho
ccr logs

# Agar port busy hai
ccr stop
ccr start
```

---

### **Problem 4: Environment variables load nahi ho rahe**
**Solution:**
1. **Saare terminals band karo**
2. Computer **restart** karo
3. Naya PowerShell kholo
4. `ccr start` karo
5. Test karo

---

## 📌 **Daily Use Commands**

### **Har din jab kaam karna ho:**

```cmd
# 1. Router start karo (agar band ho)
ccr start

# 2. Apne project folder mein jao
cd path\to\your\project

# 3. Claude Code chalaao
claude

# 4. Kaam khatam hone par router band karo (optional)
ccr stop
```

---

## 🎓 **Pro Tips**

### **Tip 1: Model Change Karna**
Claude interface mein:
```
/model gemini-1.5-pro
```

### **Tip 2: Router Logs Dekhna**
```cmd
ccr logs
```

### **Tip 3: Config File Edit Karna**
```powershell
notepad $env:USERPROFILE\.claude-code-router\config.json
```

### **Tip 4: Router Auto-Start**
Windows startup mein add karne ke liye:
```powershell
# Startup folder kholo
explorer shell:startup

# Shortcut banao:
# Target: cmd.exe /c ccr start
```

---

## 📊 **Limits - Free Version**

✅ **Gemini API Free Tier:**
- **1,500 requests per day**
- **Fast responses**
- **No credit card needed**

---

## 🎯 **Summary - Quick Reference**

```powershell
# Setup commands (ek baar only)
npm install -g @musistudio/claude-code
npm install -g @musistudio/claude-code-router

# Environment variables (ek baar only)
[System.Environment]::SetEnvironmentVariable("GOOGLE_API_KEY", "YOUR_KEY", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "http://127.0.0.1:3456", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "sk-ant-dummy-key", "User")

# Daily use
ccr start      # Router start
claude         # Claude Code start
ccr stop       # Router stop
ccr status     # Check status
```

---

## ✅ **Checklist - Sab Sahi Hai?**

- [ ] Node.js install hai (`node --version` check karo)
- [ ] Google API key banaya
- [ ] Claude Code install hai (`claude --version`)
- [ ] Router install hai (`ccr --version`)
- [ ] Config file bana di
- [ ] Environment variables set kar diye
- [ ] PowerShell restart kiya
- [ ] Router chal raha hai (`ccr status`)
- [ ] Claude Code test kiya aur response aaya ✅

---

## 🎉 **Congratulations!**

Aap ab **Claude Code with Gemini** use kar sakte ho - **BILKUL FREE!**

Happy Coding! 🚀

---


### **Common Resources:**
- GitHub: https://github.com/musistudio/claude-code-router
- Gemini API: https://aistudio.google.com
