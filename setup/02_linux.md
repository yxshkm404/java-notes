# Installing Java on Linux

## Overview

This guide covers the installation of Java (JDK/JRE) on various Linux distributions. We'll explore multiple installation methods and help you set up Java for development.

![Java on Linux](https://raw.githubusercontent.com/github/explore/5b3600551e122a3277c2c5368af2ad5725ffa9a1/topics/java/java.png)

## Prerequisites

Before installing Java, ensure your system is up to date:

```bash
# For Ubuntu/Debian
sudo apt update && sudo apt upgrade

# For Fedora
sudo dnf update

# For CentOS/RHEL
sudo yum update

# For Arch Linux
sudo pacman -Syu
```

## Checking Existing Java Installation

First, check if Java is already installed:

```bash
# Check Java version
java -version

# Check Java compiler version
javac -version

# Find Java location
which java
```

![Terminal Check Java](https://www.fosslinux.com/wp-content/uploads/2020/12/Check-Java-version.png)

## Installation Methods

### Method 1: Installing OpenJDK from Default Repositories

OpenJDK is the open-source implementation of Java and is available in most Linux distribution repositories.

#### Ubuntu/Debian/Linux Mint

```bash
# Install OpenJDK 11 (LTS)
sudo apt install openjdk-11-jdk

# Install OpenJDK 17 (LTS)
sudo apt install openjdk-17-jdk

# Install OpenJDK 21 (Latest LTS)
sudo apt install openjdk-21-jdk

# Install only JRE (if you don't need development tools)
sudo apt install openjdk-17-jre
```

#### Fedora

```bash
# Install OpenJDK 11
sudo dnf install java-11-openjdk-devel

# Install OpenJDK 17
sudo dnf install java-17-openjdk-devel

# Install OpenJDK 21
sudo dnf install java-21-openjdk-devel

# Install only JRE
sudo dnf install java-17-openjdk
```

#### CentOS/RHEL/Rocky Linux

```bash
# Install OpenJDK 11
sudo yum install java-11-openjdk-devel

# Install OpenJDK 17
sudo yum install java-17-openjdk-devel

# Install only JRE
sudo yum install java-17-openjdk
```

#### Arch Linux/Manjaro

```bash
# Install OpenJDK 11
sudo pacman -S jdk11-openjdk

# Install OpenJDK 17
sudo pacman -S jdk17-openjdk

# Install OpenJDK 21
sudo pacman -S jdk21-openjdk

# Install only JRE
sudo pacman -S jre17-openjdk
```

### Method 2: Installing Oracle JDK

Oracle JDK requires manual download and installation.

#### Step 1: Download Oracle JDK

Visit [Oracle's Java Downloads](https://www.oracle.com/java/technologies/downloads/) and download the appropriate package for your system.

![Oracle JDK Download](https://www.oracle.com/a/ocom/img/cb71-java-logo.png)

#### Step 2: Install Downloaded Package

**For .deb package (Ubuntu/Debian):**

```bash
# Navigate to download directory
cd ~/Downloads

# Install the package
sudo dpkg -i jdk-21_linux-x64_bin.deb

# Fix any dependency issues
sudo apt-get install -f
```

**For .rpm package (Fedora/CentOS/RHEL):**

```bash
# Navigate to download directory
cd ~/Downloads

# Install the package
sudo rpm -ivh jdk-21_linux-x64_bin.rpm
```

**For .tar.gz package (Universal):**

```bash
# Create directory for Java
sudo mkdir -p /opt/java

# Extract the archive
sudo tar -xzf jdk-21_linux-x64_bin.tar.gz -C /opt/java

# Set up environment variables (see Configuration section)
```

### Method 3: Using SDKMAN! (Recommended for Developers)

SDKMAN! is a tool for managing multiple Java versions.

#### Install SDKMAN!

```bash
# Install SDKMAN!
curl -s "https://get.sdkman.io" | bash

# Source the initialization script
source "$HOME/.sdkman/bin/sdkman-init.sh"

# Verify installation
sdk version
```

#### Install Java using SDKMAN!

```bash
# List available Java versions
sdk list java

# Install specific version
sdk install java 17.0.8-tem
sdk install java 11.0.20-tem
sdk install java 21.0.1-oracle

# Use a specific version
sdk use java 17.0.8-tem

# Set default version
sdk default java 17.0.8-tem
```

![SDKMAN Interface](https://sdkman.io/assets/img/sdk-man-small-pattern.svg)

### Method 4: Using Adoptium (Eclipse Temurin)

Adoptium provides prebuilt OpenJDK binaries.

```bash
# Add Adoptium repository
wget -q -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo apt-key add -
sudo add-apt-repository --yes https://packages.adoptium.net/artifactory/deb/

# Update package index
sudo apt update

# Install Temurin 17
sudo apt install temurin-17-jdk

# Install Temurin 21
sudo apt install temurin-21-jdk
```

## Configuration

### Setting JAVA_HOME Environment Variable

#### Method 1: System-wide Configuration

Edit `/etc/environment`:

```bash
sudo nano /etc/environment
```

Add the following line:

```bash
JAVA_HOME="/usr/lib/jvm/java-17-openjdk-amd64"
```

#### Method 2: User-specific Configuration

Edit `~/.bashrc` or `~/.bash_profile`:

```bash
nano ~/.bashrc
```

Add the following lines:

```bash
# Java Environment Variables
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
```

Apply changes:

```bash
source ~/.bashrc
```

### For ZSH Users

Edit `~/.zshrc`:

```bash
nano ~/.zshrc
```

Add the same environment variables and reload:

```bash
source ~/.zshrc
```

## Managing Multiple Java Versions

### Using update-alternatives (Debian/Ubuntu)

```bash
# Configure java command
sudo update-alternatives --config java

# Configure javac command
sudo update-alternatives --config javac

# Install new alternative
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-17-openjdk-amd64/bin/java 1
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/java-17-openjdk-amd64/bin/javac 1
```

![Update Alternatives](https://linuxize.com/post/install-java-on-ubuntu-18-04/featured_huf697aea935bbf852e8d03e1bb56c7f2f_45408_768x0_resize_q75_lanczos.jpg)

### Using alternatives (Fedora/CentOS/RHEL)

```bash
# List Java installations
sudo alternatives --config java

# Select default version (enter selection number)
sudo alternatives --config java
```

## Verification

After installation, verify your Java setup:

```bash
# Check Java version
java -version

# Check Java compiler
javac -version

# Check JAVA_HOME
echo $JAVA_HOME

# Compile and run a test program
echo 'public class Test { public static void main(String[] args) { System.out.println("Java is working!"); } }' > Test.java
javac Test.java
java Test
```

Expected output:
```
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Ubuntu-122.04)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Ubuntu-122.04, mixed mode, sharing)
```

## Installing Java IDEs

### IntelliJ IDEA

```bash
# Using Snap (Ubuntu/Debian)
sudo snap install intellij-idea-community --classic

# Using Flatpak
flatpak install flathub com.jetbrains.IntelliJ-IDEA-Community

# Using SDKMAN!
sdk install idea
```

### Eclipse

```bash
# Using Snap
sudo snap install eclipse --classic

# Using package manager (Ubuntu/Debian)
sudo apt install eclipse

# Download from website
wget https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2023-09/R/eclipse-java-2023-09-R-linux-gtk-x86_64.tar.gz
```

### Visual Studio Code with Java Extensions

```bash
# Install VS Code
sudo snap install code --classic

# Install Java Extension Pack
code --install-extension vscjava.vscode-java-pack
```

## Troubleshooting

### Common Issues and Solutions

#### 1. Java Command Not Found

```bash
# Add Java to PATH
export PATH=$PATH:/usr/lib/jvm/java-17-openjdk-amd64/bin

# Make permanent
echo 'export PATH=$PATH:/usr/lib/jvm/java-17-openjdk-amd64/bin' >> ~/.bashrc
source ~/.bashrc
```

#### 2. Wrong Java Version Being Used

```bash
# Check which Java is being used
which java
ls -la /usr/bin/java

# Update alternatives
sudo update-alternatives --config java
```

#### 3. JAVA_HOME Not Set

```bash
# Find Java installation
sudo find /usr -name java -type f 2>/dev/null | grep bin/java

# Set JAVA_HOME
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
```

#### 4. Permission Denied

```bash
# Fix permissions
sudo chmod +x /usr/lib/jvm/java-17-openjdk-amd64/bin/java
sudo chmod +x /usr/lib/jvm/java-17-openjdk-amd64/bin/javac
```

## Uninstalling Java

### Ubuntu/Debian

```bash
# Remove OpenJDK
sudo apt remove openjdk-17-jdk
sudo apt autoremove

# Purge configuration
sudo apt purge openjdk-17-jdk
```

### Fedora

```bash
# Remove OpenJDK
sudo dnf remove java-17-openjdk-devel
```

### Using SDKMAN!

```bash
# Uninstall specific version
sdk uninstall java 17.0.8-tem
```

## Best Practices

1. **Use LTS Versions**: Prefer Long Term Support versions (11, 17, 21) for production
2. **Keep Updated**: Regularly update Java for security patches
3. **Use Version Managers**: SDKMAN! or jenv for managing multiple versions
4. **Set JAVA_HOME**: Always set JAVA_HOME for development tools
5. **Document Version**: Keep track of Java version used in projects

## Quick Installation Scripts

### Ubuntu/Debian Quick Install

```bash
#!/bin/bash
# Quick Java 17 installation script for Ubuntu/Debian

# Update system
sudo apt update

# Install OpenJDK 17
sudo apt install -y openjdk-17-jdk

# Set JAVA_HOME
echo "export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64" >> ~/.bashrc
echo "export PATH=\$PATH:\$JAVA_HOME/bin" >> ~/.bashrc

# Apply changes
source ~/.bashrc

# Verify installation
java -version
javac -version
echo "JAVA_HOME: $JAVA_HOME"
```

Save this as `install-java.sh` and run:

```bash
chmod +x install-java.sh
./install-java.sh
```

## Conclusion

You now have Java successfully installed on your Linux system! Whether you're using OpenJDK, Oracle JDK, or managing multiple versions with SDKMAN!, you're ready to start developing Java applications.

### Next Steps

1. Install an IDE or text editor
2. Set up build tools (Maven, Gradle)
3. Configure your development environment
4. Start coding!

### Useful Resources

- [OpenJDK Documentation](https://openjdk.org/)
- [Oracle Java Documentation](https://docs.oracle.com/en/java/)
- [SDKMAN! Documentation](https://sdkman.io/usage)
- [Adoptium Downloads](https://adoptium.net/)

---

*Remember to keep your Java installation updated for the latest features and security patches!*