# Installing Java on Windows

## Overview

This guide covers the installation of Java (JDK/JRE) on Windows systems. We'll explore multiple installation methods and help you set up Java for development on Windows 10 and Windows 11.

![Java on Windows](https://raw.githubusercontent.com/github/explore/5b3600551e122a3277c2c5368af2ad5725ffa9a1/topics/java/java.png)

## Prerequisites

Before installing Java, ensure your Windows system is ready:

```powershell
# Check Windows version (Run in PowerShell or Command Prompt)
winver

# Check system architecture (64-bit or 32-bit)
wmic os get osarchitecture

# Alternative way to check system info
systeminfo | findstr /B /C:"OS Name" /C:"System Type"
```

![Windows System Info](https://www.java.com/en/img/download/windows-header-2x.jpg)

## Checking Existing Java Installation

First, check if Java is already installed:

```cmd
# Open Command Prompt (cmd) or PowerShell

# Check Java version
java -version

# Check Java compiler version
javac -version

# Find Java location
where java

# Check JAVA_HOME environment variable
echo %JAVA_HOME%
```

![Java Version Check Windows](https://cdn.programiz.com/sites/tutorial2program/files/java-version-windows.png)

## Installation Methods

### Method 1: Installing Oracle JDK (Official)

#### Step 1: Download Oracle JDK

1. Visit [Oracle's Java Downloads](https://www.oracle.com/java/technologies/downloads/)
2. Select Windows tab
3. Choose your version (recommended: Latest LTS - Java 17 or 21)
4. Download the Windows x64 Installer (.exe file)

![Oracle Download Page](https://www.oracle.com/a/ocom/img/cb71-java-logo.png)

#### Step 2: Install Oracle JDK

1. **Run the installer** as Administrator (right-click → Run as administrator)
2. **Click Next** on the welcome screen
3. **Choose installation location** (default: `C:\Program Files\Java\jdk-21`)
4. **Click Next** and then **Close** when installation completes

![Oracle JDK Installer](https://docs.oracle.com/en/java/javase/17/install/img/windows-jdk-installer.png)

### Method 2: Installing OpenJDK

#### Option A: Adoptium (Eclipse Temurin)

1. Visit [Adoptium website](https://adoptium.net/)
2. Select:

   - Operating System: Windows
   - Architecture: x64
   - Package Type: JDK
   - Version: 17 (LTS) or 21 (LTS)

3. Download the `.msi` installer
4. Run the installer with these options:
   - ✓ Add to PATH
   - ✓ Set JAVA_HOME variable
   - ✓ JavaSoft (Oracle) registry keys

![Adoptium Installer](https://adoptium.net/images/temurin-logo.png)

#### Option B: Microsoft Build of OpenJDK

```powershell
# Using Windows Package Manager (winget)
winget install Microsoft.OpenJDK.17

# Or download from Microsoft
# https://www.microsoft.com/openjdk
```

### Method 3: Using Chocolatey Package Manager

#### Step 1: Install Chocolatey (if not installed)

Run PowerShell as Administrator:

```powershell
# Check execution policy
Get-ExecutionPolicy

# Set execution policy if needed
Set-ExecutionPolicy Bypass -Scope Process

# Install Chocolatey
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

#### Step 2: Install Java using Chocolatey

```powershell
# Install OpenJDK 17
choco install openjdk17

# Install OpenJDK 21
choco install openjdk

# Install Oracle JDK 17
choco install oraclejdk17

# Install Temurin 17
choco install temurin17

# Install multiple versions
choco install openjdk11 openjdk17 openjdk21
```

![Chocolatey Logo](https://chocolatey.org/assets/images/global-shared/logo-square.svg)

### Method 4: Using Scoop Package Manager

#### Step 1: Install Scoop

Run PowerShell:

```powershell
# Install Scoop
iwr -useb get.scoop.sh | iex

# Or with custom directory
iex "& {$(irm get.scoop.sh)} -ScoopDir 'C:\Applications\Scoop' -ScoopGlobalDir 'C:\GlobalScoopApps'"
```

#### Step 2: Install Java using Scoop

```powershell
# Add Java bucket
scoop bucket add java

# Install OpenJDK
scoop install openjdk17
scoop install openjdk21

# Install Oracle JDK
scoop install oraclejdk17

# Install Temurin
scoop install temurin17-jdk
```

### Method 5: Using SDKMAN! on Windows (via Git Bash/WSL)

#### For Git Bash

1. Install [Git for Windows](https://git-scm.com/download/win)
2. Open Git Bash
3. Install SDKMAN!:

```bash
# Install SDKMAN! in Git Bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# Install Java
sdk install java 17.0.9-tem
sdk install java 21.0.1-oracle
```

#### For WSL (Windows Subsystem for Linux)

```bash
# In WSL terminal
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 17.0.9-tem
```

## Environment Variables Configuration

### Method 1: Using System Properties GUI

1. **Open System Properties**:

   - Right-click "This PC" → Properties → Advanced system settings
   - Or press `Win + X` → System → Advanced system settings
   - Or run `sysdm.cpl` → Advanced tab

2. **Click "Environment Variables"**

3. **Set JAVA_HOME**:

   - Click "New" under System variables
   - Variable name: `JAVA_HOME`
   - Variable value: `C:\Program Files\Java\jdk-17` (your Java installation path)

4. **Update PATH**:
   - Find "Path" in System variables
   - Click "Edit"
   - Click "New"
   - Add: `%JAVA_HOME%\bin`

![Environment Variables Windows](https://miro.medium.com/max/1400/1*9uxqFii0QdmtkmTSCp4aBA.png)

### Method 2: Using Command Line

Run Command Prompt as Administrator:

```cmd
# Set JAVA_HOME
setx JAVA_HOME "C:\Program Files\Java\jdk-17" /M

# Add to PATH
setx PATH "%PATH%;%JAVA_HOME%\bin" /M

# Verify (restart Command Prompt first)
echo %JAVA_HOME%
echo %PATH%
```

### Method 3: Using PowerShell

Run PowerShell as Administrator:

```powershell
# Set JAVA_HOME permanently
[System.Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\Program Files\Java\jdk-17", "Machine")

# Add to PATH permanently
$currentPath = [System.Environment]::GetEnvironmentVariable("Path", "Machine")
$newPath = $currentPath + ";%JAVA_HOME%\bin"
[System.Environment]::SetEnvironmentVariable("Path", $newPath, "Machine")

# Refresh environment variables in current session
$env:JAVA_HOME = [System.Environment]::GetEnvironmentVariable("JAVA_HOME", "Machine")
$env:Path = [System.Environment]::GetEnvironmentVariable("Path", "Machine")
```

## Managing Multiple Java Versions

### Method 1: Using jenv-for-windows

1. Download jenv for Windows from GitHub
2. Extract to a directory (e.g., `C:\tools\jenv`)
3. Add to PATH
4. Configure:

```cmd
# Add Java versions
jenv add "C:\Program Files\Java\jdk-11"
jenv add "C:\Program Files\Java\jdk-17"
jenv add "C:\Program Files\Java\jdk-21"

# List versions
jenv list

# Switch versions
jenv use 17
```

### Method 2: Using Batch Scripts

Create switching scripts in a folder (e.g., `C:\JavaSwitcher\`):

**switch-java-11.bat:**

```batch
@echo off
set JAVA_HOME=C:\Program Files\Java\jdk-11
set PATH=%JAVA_HOME%\bin;%PATH%
echo Switched to Java 11
java -version
```

**switch-java-17.bat:**

```batch
@echo off
set JAVA_HOME=C:\Program Files\Java\jdk-17
set PATH=%JAVA_HOME%\bin;%PATH%
echo Switched to Java 17
java -version
```

### Method 3: Using PowerShell Functions

Add to PowerShell profile (`$PROFILE`):

```powershell
# Open PowerShell profile
notepad $PROFILE

# Add these functions
function Use-Java11 {
    $env:JAVA_HOME = "C:\Program Files\Java\jdk-11"
    $env:Path = "$env:JAVA_HOME\bin;" + ($env:Path -split ';' | Where-Object { $_ -notlike '*\Java\jdk*' }) -join ';'
    java -version
}

function Use-Java17 {
    $env:JAVA_HOME = "C:\Program Files\Java\jdk-17"
    $env:Path = "$env:JAVA_HOME\bin;" + ($env:Path -split ';' | Where-Object { $_ -notlike '*\Java\jdk*' }) -join ';'
    java -version
}

function Use-Java21 {
    $env:JAVA_HOME = "C:\Program Files\Java\jdk-21"
    $env:Path = "$env:JAVA_HOME\bin;" + ($env:Path -split ';' | Where-Object { $_ -notlike '*\Java\jdk*' }) -join ';'
    java -version
}
```

## Verification

After installation, verify your Java setup:

```cmd
# Open new Command Prompt or PowerShell

# Check Java version
java -version

# Check Java compiler
javac -version

# Check JAVA_HOME
echo %JAVA_HOME%

# In PowerShell
echo $env:JAVA_HOME

# Check Java location
where java

# Run a test program
echo public class Test { public static void main(String[] args) { System.out.println("Java works on Windows!"); } } > Test.java
javac Test.java
java Test
```

Expected output:

```
openjdk version "17.0.9" 2023-10-17
OpenJDK Runtime Environment Temurin-17.0.9+9 (build 17.0.9+9)
OpenJDK 64-Bit Server VM Temurin-17.0.9+9 (build 17.0.9+9, mixed mode, sharing)
```

## Installing Java IDEs

### IntelliJ IDEA

```powershell
# Using Chocolatey
choco install intellijidea-community

# Using Scoop
scoop bucket add extras
scoop install idea

# Or download from JetBrains
# https://www.jetbrains.com/idea/download/
```

![IntelliJ IDEA](https://resources.jetbrains.com/storage/products/company/brand/logos/IntelliJ_IDEA_icon.png)

### Eclipse

```powershell
# Using Chocolatey
choco install eclipse

# Using Scoop
scoop install eclipse-java

# Or download installer
# https://www.eclipse.org/downloads/
```

### Visual Studio Code

```powershell
# Using Chocolatey
choco install vscode

# Using Scoop
scoop install vscode

# Install Java Extension Pack
code --install-extension vscjava.vscode-java-pack
```

### NetBeans

```powershell
# Using Chocolatey
choco install netbeans

# Or download from Apache
# https://netbeans.apache.org/
```

## Build Tools Installation

### Maven

```powershell
# Using Chocolatey
choco install maven

# Using Scoop
scoop install maven

# Verify
mvn -version
```

### Gradle

```powershell
# Using Chocolatey
choco install gradle

# Using Scoop
scoop install gradle

# Verify
gradle -version
```

## Windows Terminal Configuration

For better development experience, configure Windows Terminal:

```json
{
  "profiles": {
    "list": [
      {
        "name": "Java Development",
        "commandline": "cmd.exe",
        "startingDirectory": "C:\\JavaProjects",
        "icon": "https://raw.githubusercontent.com/github/explore/5b3600551e122a3277c2c5368af2ad5725ffa9a1/topics/java/java.png",
        "environmentVariables": {
          "JAVA_HOME": "C:\\Program Files\\Java\\jdk-17"
        }
      }
    ]
  }
}
```

## Troubleshooting

### Common Issues and Solutions

#### 1. 'java' is not recognized as internal or external command

```cmd
# Check if Java is in PATH
echo %PATH%

# Add Java to PATH manually
set PATH=%PATH%;C:\Program Files\Java\jdk-17\bin

# Make permanent
setx PATH "%PATH%;C:\Program Files\Java\jdk-17\bin" /M
```

#### 2. JAVA_HOME is not set

```cmd
# Set JAVA_HOME temporarily
set JAVA_HOME=C:\Program Files\Java\jdk-17

# Set permanently
setx JAVA_HOME "C:\Program Files\Java\jdk-17" /M
```

#### 3. Wrong Java Version Being Used

```powershell
# Check all Java installations
where java

# Check registry entries
reg query "HKLM\SOFTWARE\JavaSoft\Java Development Kit"

# Remove old Java from PATH
# Edit System Environment Variables manually
```

#### 4. Access Denied Errors

- Run installers as Administrator
- Check Windows Defender or antivirus settings
- Ensure proper permissions on Java directory

#### 5. PowerShell Execution Policy

```powershell
# Check current policy
Get-ExecutionPolicy

# Set to allow scripts
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

## Uninstalling Java

### Method 1: Using Control Panel

1. Open Control Panel → Programs and Features
2. Find Java in the list
3. Click Uninstall
4. Follow the uninstallation wizard

### Method 2: Using Windows Settings

1. Open Settings (Win + I)
2. Go to Apps → Apps & features
3. Search for "Java"
4. Click on Java and select Uninstall

### Method 3: Using Command Line

```powershell
# Using Chocolatey
choco uninstall openjdk17

# Using Scoop
scoop uninstall openjdk17

# Using Windows Package Manager
winget uninstall "Eclipse Temurin JDK with Hotspot 17"
```

### Method 4: Complete Manual Removal

```batch
@echo off
echo Removing Java installations...

REM Remove Java directories
rmdir /s /q "C:\Program Files\Java"
rmdir /s /q "C:\Program Files (x86)\Java"

REM Remove environment variables
setx JAVA_HOME "" /M
REG delete "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /F /V JAVA_HOME

REM Clean PATH variable (manual intervention needed)
echo Please manually remove Java entries from PATH variable

REM Remove registry entries
reg delete "HKLM\SOFTWARE\JavaSoft" /f

echo Java removal complete. Please restart your computer.
pause
```

## Windows-Specific Considerations

### Windows Defender and Antivirus

- Add Java installation directory to antivirus exceptions
- Windows Defender might scan JAR files, affecting performance

### File Path Length Limitations

- Windows has a 260-character path limit
- Use short paths or enable long path support:

```powershell
# Enable long paths (Windows 10+)
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" -Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
```

### Running as Administrator

Some Java applications may require administrator privileges:

```powershell
# Create a shortcut with admin privileges
$WshShell = New-Object -comObject WScript.Shell
$Shortcut = $WshShell.CreateShortcut("$Home\Desktop\JavaApp.lnk")
$Shortcut.TargetPath = "java"
$Shortcut.Arguments = "-jar C:\path\to\app.jar"
$Shortcut.Save()

# Then right-click → Properties → Advanced → Run as administrator
```

## Quick Installation Scripts

### PowerShell Installation Script

```powershell
# Quick Java Installation Script for Windows
# Save as Install-Java.ps1

param(
    [string]$Version = "17",
    [string]$Vendor = "Temurin"
)

Write-Host "Installing Java $Version ($Vendor) on Windows..." -ForegroundColor Green

# Check if running as Administrator
if (-NOT ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator"))
{
    Write-Host "This script requires Administrator privileges. Restarting..." -ForegroundColor Yellow
    Start-Process PowerShell -Verb RunAs "-File `"$PSCommandPath`" -Version $Version -Vendor $Vendor"
    exit
}

# Install Chocolatey if not present
if (!(Get-Command choco -ErrorAction SilentlyContinue)) {
    Write-Host "Installing Chocolatey..." -ForegroundColor Yellow
    Set-ExecutionPolicy Bypass -Scope Process -Force
    [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
    iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
}

# Install Java
Write-Host "Installing Java..." -ForegroundColor Yellow
switch ($Vendor.ToLower()) {
    "temurin" { choco install temurin$Version -y }
    "openjdk" { choco install openjdk$Version -y }
    "oracle" { choco install oraclejdk$Version -y }
    default { choco install temurin$Version -y }
}

# Set JAVA_HOME
$javaPath = (Get-ChildItem "C:\Program Files\*" -Filter "*jdk*$Version*" | Select-Object -First 1).FullName
[System.Environment]::SetEnvironmentVariable("JAVA_HOME", $javaPath, "Machine")

# Update PATH
$currentPath = [System.Environment]::GetEnvironmentVariable("Path", "Machine")
if ($currentPath -notlike "*JAVA_HOME*") {
    [System.Environment]::SetEnvironmentVariable("Path", "$currentPath;%JAVA_HOME%\bin", "Machine")
}

# Refresh environment
$env:JAVA_HOME = $javaPath
$env:Path = [System.Environment]::GetEnvironmentVariable("Path", "Machine")

Write-Host "Java installation completed!" -ForegroundColor Green
Write-Host "JAVA_HOME: $javaPath" -ForegroundColor Cyan

# Verify installation
java -version
```

Usage:

```powershell
# Run with defaults (Temurin 17)
.\Install-Java.ps1

# Install specific version
.\Install-Java.ps1 -Version 21 -Vendor Oracle
```

## Best Practices

1. **Always Set JAVA_HOME**: Essential for many Java applications
2. **Use LTS Versions**: Prefer versions 11, 17, or 21 for production
3. **Keep Java Updated**: Enable automatic updates or check regularly
4. **Use Package Managers**: Chocolatey or Scoop simplify management
5. **Document Versions**: Keep track of Java versions for each project
6. **Regular Cleanup**: Remove old unused Java versions
7. **Path Management**: Be careful with PATH variable modifications

## Conclusion

You now have Java successfully installed on your Windows system! Whether you're using Oracle JDK, OpenJDK, or managing multiple versions, you're ready to start developing Java applications.

### Next Steps

1. Install your preferred IDE
2. Set up build tools (Maven, Gradle)
3. Configure your development environment
4. Start coding Java applications!

### Useful Resources

- [Oracle Java Documentation](https://docs.oracle.com/en/java/)
- [OpenJDK Downloads](https://openjdk.org/)
- [Adoptium Downloads](https://adoptium.net/)
- [Chocolatey Java Packages](https://community.chocolatey.org/packages?q=java)
- [Microsoft Build of OpenJDK](https://www.microsoft.com/openjdk)

---

_Remember to restart your Command Prompt or PowerShell after installation to ensure all environment variables are loaded correctly!_
