# Ubuntu Desktop Maintenance and Tools

This document provides essential command-line tools and procedures for maintaining and updating your Ubuntu desktop environment efficiently.

## 🧭 Table of Contents

1. [Core System Utilities](#core-system-utilities)

2. [Selective Application Updates](#selective-application-updates)

   * [How to Determine the Installation Method](#how-to-determine-the-installation-method)

   * [General Commands for Selective Updates](#general-commands-for-selective-updates)

   * [App-Specific Update Examples](#app-specific-update-examples)

## 💻 Core System Utilities

These commands are fundamental for general system health, file management, and diagnostics.

| Task | Command | Description | 
 | ----- | ----- | ----- | 
| **Full System Upgrade** | `sudo apt update && sudo apt upgrade -y` | Updates all package lists and upgrades all installed software (APT packages) automatically. | 
| **Remove Old Dependencies** | `sudo apt autoremove` | Removes packages that were installed automatically to satisfy dependencies but are no longer needed. | 
| **Check Disk Space (Free)** | `df -h` | Shows used and available disk space for all mounted filesystems in human-readable format. | 
| **Check Directory Size** | `du -sh /path/to/directory` | Shows the total disk usage (`-s` for summary) of a specified directory in human-readable format (`-h`). | 
| **List Running Processes** | `top` or `htop` | Opens an interactive monitor showing running tasks and system resource usage (install `htop` with `sudo apt install htop`). | 

## Selective Application Updates

This section details how to update individual applications (like Chrome, VS Code, and Brave) without running a full system upgrade every time. This is key when the application uses its own separate update channel (repository).

### 🔍 How to Determine the Installation Method

Before updating, you need to know if the application was installed using `apt` or `snap`, as the command is different for each.

| **Method** | **Command to Check** | **What to Look For** | 
 | ----- | ----- | ----- | 
| **APT** | `apt policy [package name]` | Check the **Installed** line. If it shows a version number and source, it's an APT package. | 
| **Snap** | `snap list [package name]` | If it returns an entry with a `Version` and `Rev` (revision number), it's a Snap package. | 

For example, to check the installation type for VS Code, you might run:

```
snap list code
# If nothing shows, try the APT check:
apt policy code
```

### ⚙️ General Commands for Selective Updates

You must **always** run the `update` command first to refresh your system's package list before upgrading any package. This fetches the latest version information from all your configured repositories (including those for Chrome, VS Code, and Brave).

#### 1. Update the Package Lists (Mandatory First Step)

```
sudo apt update
```

#### 2. Update a Specific APT Package (e.g., Chrome, Brave)

Use the `apt install` command along with the `--only-upgrade` flag and the package's specific name.

```
# General Syntax for an APT Package
sudo apt install --only-upgrade [package-name]
```

#### 3. Update a Specific Snap Package (e.g., VS Code Snap)

Use the `snap refresh` command followed by the snap's name.

```
# General Syntax for a Snap Package
sudo snap refresh [snap-name]
```

### 🚀 App-Specific Update Examples

Below are the commands to update the specific applications you mentioned.

| **Application** | **Likely Package Type** | **Command(s) to Update Only This App** | **Notes** | 
 | ----- | ----- | ----- | ----- | 
| **Google Chrome** | APT | `sudo apt install --only-upgrade google-chrome-stable` | The package name is typically `google-chrome-stable`. | 
| **Brave Browser** | APT | `sudo apt install --only-upgrade brave-browser` | The package name is typically `brave-browser`. | 
| **Visual Studio Code** | APT | `sudo apt install --only-upgrade code` | Use this if installed via a `.deb` file. | 
| **Visual Studio Code** | Snap | `sudo snap refresh code` | Use this if installed via the Ubuntu Software Center (Snap). | 

**Full Example for updating all three (assuming APT for Brave/Chrome, and Snap for VS Code):**

```
# 1. Update all package lists
sudo apt update

# 2. Update Google Chrome (APT)
sudo apt install --only-upgrade google-chrome-stable

# 3. Update Brave Browser (APT)
sudo apt install --only-upgrade brave-browser

# 4. Update Visual Studio Code (Snap)
sudo snap refresh code
```
By using these targeted commands, you keep control over which applications get updated when, without having to fully reinstall them or update your entire system at once.
