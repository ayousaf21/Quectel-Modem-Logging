# 🎛️ **Quectel Modem Logging**
This repository provides scripts and configurations to facilitate the logging of Quectel Modem EG21 using the QLog tool. It's designed to assist in debugging cellular disconnections and related issues on Quectel modems, particularly when integrated with *i.MX Yocto* platforms.

![QLog](https://github.com/user-attachments/assets/a34bb16e-1f6a-4461-aa14-8a340638422e)

## ⚙️ **Features**
- Bash Script to automate the process of starting and stopping QLog, managing log files, and handling modem interfaces.
- Configuration Files and predefined settings for QLog to filter and capture relevant log data.
- Guidelines for setting up and using the logging system effectively.

## 📢 **Integration with i.MX EVK**
For users working with i.MX EVK platforms, the provided bash script is utilized to automate the logging process. The script handle the initialization of the modem interface, start QLog with the appropriate configurations, and manage log file storage.

Ensure that the modem is properly connected to the EVK and recognized by the system before executing the scripts. 

*I am using Quectel EG21 that has its DM Port at /dev/ttyUSB0. Make sure to configure it with your own modem.*
  
## 🚀 **Installation**
### 1. Build QLog
Clone the QLog repository and build the tool. In my case, I am making executable for my I.MX6 EVK running Yocto on ARM architecture:
```
git clone https://github.com/quectel-official/QLog.git
cd QLog
make CROSS_COMPILE=aarch64-gnu-linux-
```
This will generate the qlog executable. Place the Qlog executable file in your I.MX6 EVK /data path.

### 2. Start Logging
Run the bash script from your Linux environment. Make sure the bash script has executable permission. Bash script will run the Qlog via SSH:
```
chmod +x modemLogs
./modemLogs
```
### 3. Stop Logging
- Script is set to run for 20 minutes and will stop automatically to avoid filling up the flash memory of I.MX6 EVK
- The log files will then be transmitted to your system via SCP.
- Disk Usage is limit to 80GB, after that logs will start to overwrite with the latest ones.
