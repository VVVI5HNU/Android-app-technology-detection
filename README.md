# 🔍 Android Application Technology Detection Cheat Sheet

This repository provides a **quick, reliable, and practical approach** to identify the technology stack used to build an Android application using **static APK analysis**.

This methodology is commonly used during **Android Mobile VAPT (Vulnerability Assessment & Penetration Testing)** to determine the application architecture before performing framework-specific security testing.

---

## 📌 Why Identify Application Technology?

Identifying the underlying framework helps to:

- Select the correct interception and hooking strategy  
- Understand network behavior (proxy handling, SSL pinning)  
- Choose appropriate tools (Frida, Objection, native hooks)  
- Perform framework-specific security testing  
- Avoid time spent on ineffective testing approaches  

---

## 🧪 Prerequisites

- Android APK file  
- Linux / macOS terminal  
- `unzip` utility  

---

## 🚀 One-Line Commands to Identify Application Technology

Replace `app.apk` with your actual APK filename.

---

## 🟦 Flutter

```bash
unzip app.apk | grep -i flutter
```

### Indicators
- `libflutter.so`
- `assets/flutter_assets/`
- `vm_snapshot_data`
- `isolate_snapshot_data`

✔ Presence of any of the above confirms a **Flutter** application.

---

## 🟨 React Native

```bash
unzip app.apk | grep -i "reactnative\|hermes"
```

### Indicators
- `libreactnativejni.so`
- `libhermes.so`
- `index.android.bundle`
- `assets/index.android.bundle`

---

## 🟩 Ionic / Cordova / PhoneGap

```bash
unzip app.apk | grep -i "cordova\|phonegap"
```

or

```bash
unzip app.apk | grep -i "assets/www"
```

### Indicators
- `cordova.js`
- `assets/www/index.html`

---

## 🟥 Xamarin (.NET / C#)

```bash
unzip app.apk | grep -i "xamarin\|mono"
```

### Indicators
- `libmonodroid.so`
- `libmono-native.so`
- `assemblies/`

---

## 🟪 Unity (Game / 3D Applications)

```bash
unzip app.apk | grep -i unity
```

### Indicators
- `libunity.so`
- `libil2cpp.so`
- `assets/bin/Data/`

---

## 🟫 Native Android (Java / Kotlin)

Native Android applications **do not include framework-specific assets** such as Flutter, React Native, or Cordova.

If none of the above frameworks are detected, the application is most likely **Native Android**.

```bash
unzip app.apk | grep -Ei "flutter|reactnative|hermes|cordova|phonegap|ionic|unity|mono|xamarin"
```

✔ **No output → Native Android**

### Optional Kotlin Hint

```bash
unzip app.apk | grep -i kotlin
```

---

## 🧠 Pro Tip — Universal Detection Command

```bash
unzip app.apk | grep -Ei "flutter|reactnative|hermes|cordova|phonegap|ionic|unity|mono|xamarin"
```

This single command is commonly used in **real-world mobile VAPT engagements** for fast framework fingerprinting.

---

## 📝 Sample Reporting Statement

> “Static analysis of the APK revealed Flutter-specific assets (`assets/flutter_assets` and `libflutter.so`), confirming that the application is developed using the Flutter framework.”

---

## ⚠️ Important Notes

- This method is **non-intrusive** and does not require application execution  
- Always validate findings using **runtime analysis** (Frida / instrumentation)  
- Hybrid applications may contain **multiple framework indicators**  
- Security-hardened applications may **obfuscate assets**  

---

## 📚 Use Cases

- Android Mobile VAPT  
- SSL pinning and traffic interception planning  
- Reverse engineering and dynamic analysis preparation  
- Framework-specific security testing  

---

## 🤝 Contributions

Contributions are welcome.  
Feel free to submit pull requests for:

- Additional framework detection techniques  
- Automation scripts  
- Improvements aligned with **OWASP MASVS / MSTG**

---

## 📄 License

This repository is intended for **educational and authorized security testing purposes only**.
