Perfect ✅ — here’s a **brief, complete summary** of all the commands you ran to get your JavaFX app working in **PowerShell without admin**:

---

## 1️⃣ Install JDK (user-level, no admin)

```powershell
# Download JDK 17 ZIP
$jdkUrl = "https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.10+7/OpenJDK17U-jdk_x64_windows_hotspot_17.0.10_7.zip"
$zip = "$env:USERPROFILE\temurin17.zip"
$dest = "$env:USERPROFILE\jdk17"

Invoke-WebRequest -Uri $jdkUrl -OutFile $zip
Expand-Archive -Path $zip -DestinationPath $dest

# Set Java environment variables for this session
$env:JAVA_HOME = "$env:USERPROFILE\jdk17\jdk-17.0.10+7"
$env:Path = "$env:JAVA_HOME\bin;$env:Path"

# Verify Java
java -version
javac -version
```

---

## 2️⃣ Install JavaFX (user-level)

```powershell
# Download JavaFX SDK
$fxUrl = "https://download2.gluonhq.com/openjfx/17.0.10/openjfx-17.0.10_windows-x64_bin-sdk.zip"
$fxZip = "$env:USERPROFILE\javafx.zip"
$fxDir = "$env:USERPROFILE\javafx"

Invoke-WebRequest -Uri $fxUrl -OutFile $fxZip
Expand-Archive -Path $fxZip -DestinationPath $fxDir

# Optional: check that .jar files exist
Get-ChildItem "$fxDir\javafx-sdk-17.0.10\lib"
```

---

## 3️⃣ Compile your JavaFX project

```powershell
javac --module-path "$fxDir\javafx-sdk-17.0.10\lib" `
      --add-modules javafx.controls,javafx.fxml `
      *.java
```

---

## 4️⃣ Run your JavaFX application

```powershell
java --module-path "$fxDir\javafx-sdk-17.0.10\lib" `
     --add-modules javafx.controls,javafx.fxml `
     SpareBnbApp
```

---

### ⚡ Optional: shorten commands by setting an environment variable

```powershell
$env:FX="$env:USERPROFILE\javafx\javafx-sdk-17.0.10\lib"

# Compile
javac --module-path $env:FX --add-modules javafx.controls,javafx.fxml *.java

# Run
java --module-path $env:FX --add-modules javafx.controls,javafx.fxml SpareBnbApp
```

---

✅ With this, **your JavaFX app runs in PowerShell only**, no admin rights, no GUI installer.

If you want, I can make a **single PowerShell script** that does all of this in one go — download JDK, JavaFX, compile, and run — so you just run **one file** to launch your app.

Do you want me to do that?
