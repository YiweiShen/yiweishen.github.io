---
title: Access Files on the Steam Deck via SSH using VS Code
date: 2024-07-21 00:20:55
tags:
---

Accessing the Steam Deck's file system remotely can be incredibly useful. Imagine using Raycast to quickly open a recent VS Code project, and one of them is a folder on the Steam Deck via an SSH connection. With just one click, you're connected and ready to go.

## Prerequisites

Before getting started, make sure you have the following:

- Steam Deck: Ensure your Steam Deck is powered on and connected to the same Wi-Fi network as your laptop.
- Computer: A Mac (or possibly a PC) with Visual Studio Code installed.
- SSH Enabled on Steam Deck: SSH is not enabled by default. You will need to enable it through the Steam Deck's desktop mode.
- VS Code Extensions: Install the "Remote - SSH" extension on your VS Code.

## Step 1: Enable SSH on the Steam Deck

Press the Steam button, navigate to Power, and switch to Desktop mode. Once in desktop mode, open the KDE application launcher and search for Konsole (terminal).

- Start the SSH server with:
  ```bash
  sudo systemctl start sshd
  ```
- Additionally, enable SSH to start on boot:
  ```bash
  sudo systemctl enable sshd
  ```
- Verify Your IP Address, in the terminal, type:
  ```bash
  ip a
  ```
  Note the IP address (e.g., 192.168.1.xxx or 10.0.0.xxx) that corresponds to your Wi-Fi connection.

## Step 2: Create SSH Key Pairs (Recommended and not optional if you want to have a smooth flow with Raycast)

Creating SSH key pairs can enhance the security of your SSH connection by using public-key cryptography instead of a password.

- Generate SSH Key Pair on the Steam Deck:
  ```bash
  ssh-keygen -t rsa -b 4096 -f ~/.ssh/sd_rsa
  ```
  This command will save the key pair in the specified folder (~/.ssh/sd_rsa).

This process will create two files:

- "sd_rsa": This is your private key. Keep this file secure and find a way to copy it to the Mac. Be creative; for example, you can use GoodReader to set up a quick WiFi Server.
- "sd_rsa.pub": This is your public key. This file can be shared and will stay on the Steam Deck.

For added security, you can:

- Disable password authentication on the Steam Deck:
  ```bash
  sudo vim /etc/ssh/sshd_config
  ```
- Find the line that says "#PasswordAuthentication" and change it to:
  ```bash
  PasswordAuthentication no
  PubkeyAuthentication yes
  ```
- Save the file (:wq) and restart the SSH service:
  ```bash
  sudo systemctl restart sshd
  ```
- Ensure your public key is added to the "authorized_keys" file:
  ```bash
  cat ~/.ssh/sd_rsa.pub >> ~/.ssh/authorized_keys
  ```

## Step 3: Configure SSH Access in VS Code

Ensure you have the Remote - SSH extension installed. If not, you can find it in the VS Code Marketplace. Copy the "sd_rsa" private key to your Mac and set the correct permissions (chmod 600 if necessary).

- Press "Cmd+Shift+P" on Mac to open the command palette.
- Type "Remote-SSH: Open SSH Configuration File..." and select it.
- Choose the SSH configuration file you want to edit (usually "~/.ssh/config").
- Add a new entry to the configuration file in the following format:
  ```bash
  Host steamdeck
      HostName 192.168.1.xxx
      User deck
      IdentityFile ~/.ssh/sd_rsa
  ```
- Replace "192.168.1.xxx" with the actual IP address of your Steam Deck.
- Save and close the configuration file.

## Step 4: Connect to SSH in VS Code

- Again, open the command palette ("Cmd+Shift+P").
- Type "Remote-SSH: Connect to Host..." and select the entry you just added.
- The first time only, you may be prompted to accept the host's fingerprint.

By following the above steps, you can conveniently access and manage your Steam Deck’s file system using the powerful toolset provided by VS Code over an SSH connection.

## Step 5: Shortcut Using Raycast and VS Code Extension

If you haven't already, download and install Raycast from [Raycast's official website](https://www.raycast.com/). Open Raycast and go to the "Extensions Store" and search for "Visual Studio Code" and install the extension.

- Open Raycast "Option+Space"
- Type "VS Code" and you will see the shortcut in VS Code Recent Projects.
- Select "deck" or another name for your SSH connection from the list to quickly open it in the VS Code.

A big thanks to the developers who created these amazing tools!
