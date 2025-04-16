Check Chrome Update 🚀
  
Welcome to the Check Chrome Update script repository! This Bash script automates checking and updating Google Chrome to the latest stable version on Ubuntu systems. It compares your locally installed Chrome version with the latest version available from Google's repository, prompts for updates if a newer version exists, and handles installation via apt-get or direct .deb package download. 📌
📌 Features

Version Comparison 🔍: Compares the installed Google Chrome version with the latest stable version from Google's repository.
Automatic Updates ⚙️: Updates Chrome using apt-get or falls back to direct .deb package download if needed.
Beta Version Handling 🛠️: Detects and removes google-chrome-beta to prevent conflicts with the stable version.
User-Friendly Prompts 💬: Asks for confirmation before installing or updating Chrome.
Error Handling 🚨: Robust checks for network issues, repository failures, and installation errors.
Cross-Version Support 🌐: Works with Ubuntu systems supporting apt package management.

📋 Prerequisites
Before running the script, ensure the following requirements are met:

Operating System: Ubuntu 20.04 LTS or later (or any Debian-based distribution with apt).
Packages:
curl: For fetching version metadata from Google's repository.
gnupg: For handling Google's repository signing key.
wget: For downloading .deb packages (optional, used in fallback).
Install these packages with:sudo apt-get update
sudo apt-get install -y curl gnupg wget




Permissions: The script requires sudo privileges to:
Add the Google Chrome repository.
Install or update packages.
Remove conflicting google-chrome-beta packages.


Internet Connection: Required to fetch metadata and download packages.
Google Chrome: The script checks for google-chrome-stable or google-chrome. If neither is installed, it prompts to install Chrome.

📖 Installation Guide
Follow these steps to set up and run the check_chrome_update.sh script:

Clone the Repository 📥:
git clone https://github.com/Lalatenduswain/check_chrome_update.git
cd check_chrome_update


Make the Script Executable 🔐:
chmod +x check_chrome_update.sh


Run the Script 🚀:
./check_chrome_update.sh


Follow Prompts 💬:

If Chrome is not installed, the script will ask if you want to install the latest version.
If a newer version is available, it will prompt to update.
Enter y to proceed or n to cancel.



🛠️ How the Script Works
The check_chrome_update.sh script automates the process of keeping Google Chrome up to date on Ubuntu. Here’s a detailed explanation of its functionality:

Version Detection 🔍:

Local Version: Checks the installed version of google-chrome-stable (or google-chrome if the former is not found) using the --version flag.
Latest Version: Fetches the latest google-chrome-stable version from https://dl.google.com/linux/chrome/deb/dists/stable/main/binary-amd64/Packages using curl.
Compares versions using sort -V to determine if an update is needed.


Beta Version Check 🛡️:

Detects if google-chrome-beta is installed and removes it to prevent conflicts with the stable version.


Repository Setup 📦:

Adds Google’s official Chrome repository to /etc/apt/sources.list.d/google-chrome.list if not already present.
Imports Google’s signing key to /usr/share/keyrings/google-chrome-archive-keyring.gpg for secure package verification.


Update Process ⚙️:

Apt Method: Attempts to update Chrome using sudo apt-get install --only-upgrade -y google-chrome-stable.
Direct Download Fallback: If apt-get fails to install the latest version, downloads the .deb package for google-chrome-stable (e.g., google-chrome-stable_136.0.7103.25-1_amd64.deb) and installs it using dpkg.
Fixes dependencies with sudo apt-get install -f if needed.


User Interaction 💬:

Prompts the user to confirm installation or updates.
Displays clear messages about the current and latest versions, update progress, and any errors.


Error Handling 🚨:

Checks for network failures, empty metadata, and installation errors.
Exits with meaningful error messages if critical steps fail.



🖥️ Example Usage
$ ./check_chrome_update.sh
Checking for Google Chrome updates...
Removing google-chrome-beta to avoid conflicts...
Current installed version: 135.0.7049.95
Latest available version: 136.0.7103.25
A newer version of Google Chrome is available.
Would you like to update to version 136.0.7103.25? (y/n): y
Adding Google Chrome repository...
Attempting to update Google Chrome via apt...
Apt update did not install the latest version (expected 136.0.7103.25, got 135.0.7049.95).
Falling back to direct download of Google Chrome 136.0.7103.25...
Downloading from https://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_136.0.7103.25-1_amd64.deb...
Google Chrome has been successfully updated to version 136.0.7103.25

🐞 Troubleshooting
If you encounter issues, try these steps:

Check Prerequisites:Ensure curl, gnupg, and wget are installed:
sudo apt-get install -y curl gnupg wget


Verify Repository:Check the Google Chrome repository:
cat /etc/apt/sources.list.d/google-chrome.list

Expected output:
deb [arch=amd64 signed-by=/usr/share/keyrings/google-chrome-archive-keyring.gpg] http://dl.google.com/linux/chrome/deb/ stable dummy main

If missing or incorrect, re-add it:
sudo rm /etc/apt/sources.list.d/google-chrome.list
curl -fsSL https://dl.google.com/linux/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/google-chrome-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/google-chrome-archive-keyring.gpg] http://dl.google.com/linux/chrome/deb/ stable main" | sudo tee /etc/apt/sources.list.d/google-chrome.list
sudo apt-get update


Check Beta Version:Verify if google-chrome-beta is installed:
dpkg -l | grep google-chrome-beta

Remove it if present:
sudo apt-get remove -y google-chrome-beta


Test Direct Download:Verify the .deb file URL:
curl -s https://dl.google.com/linux/chrome/deb/dists/stable/main/binary-amd64/Packages | grep -A 10 "Package: google-chrome-stable" | grep -m1 "Filename:"

Test the download:
curl -I https://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_136.0.7103.25-1_amd64.deb


Manual Installation:If the script fails, manually install:
wget https://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_136.0.7103.25-1_amd64.deb
sudo dpkg -i google-chrome-stable_136.0.7103.25-1_amd64.deb
sudo apt-get install -f
rm google-chrome-stable_136.0.7103.25-1_amd64.deb


Check Installed Version:
google-chrome-stable --version



⚠️ Disclaimer | Running the Script
Author: Lalatendu Swain | GitHub | Website
This script is provided as-is and may require modifications or updates based on your specific environment and requirements. Use it at your own risk. The authors of the script are not liable for any damages or issues caused by its usage.
Important Notes:

The script requires sudo privileges, which may prompt for your password.
Ensure you have a stable internet connection to fetch metadata and packages.
Back up critical data before running system-level updates.

💖 Support & Donations
Encountering issues? Don't hesitate to submit an issue on our GitHub Issues page.
If you find this script useful and want to show your appreciation, you can donate via Buy Me a Coffee. Your support helps keep this project maintained and improved! ☕
📜 License
This project is licensed under the MIT License. See the LICENSE file for details.
🌟 Contributing
Contributions are welcome! To contribute:

Fork the repository.
Create a new branch (git checkout -b feature/your-feature).
Make your changes and commit (git commit -m "Add your feature").
Push to the branch (git push origin feature/your-feature).
Open a Pull Request.

Please ensure your code follows the script’s style and includes appropriate comments.

Happy updating! 🎉 Keep your Chrome browser shiny and up to date with check_chrome_update.sh!
