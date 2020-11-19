## Are you still using CMD? Let me introduce you to WSL

If you are new to web development and your PC is Windows, surely you have watched several courses or tutorials in which their instructors had a terminal that looked something like this: 🤩

![Terminal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603748720519/yfPQtr-1W.png)

Or ran commands such as clear or ls, which you tried to run in your terminal, but they did not work and printed an error. Well, if you have those issues, let me tell you that you're using the wrong terminal. 😅

![Cmd.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603748851899/qS9v7N5il.png)

You may think these are just unimportant details, but there is nothing further from reality.

>As a very popular saying says: **The terminal is a developer's best friend. 💙**

Hi! I'm Ernesto, and in this post, I am going to teach you how to get all the power 💪 of a **Linux terminal inside Windows (without disk partitions)**. 

---
# Table of content
1. [¿What is WSL?](#what-is-wsl)
2. [Installation of WSL](#installation-of-wsl)
  1. [Enable WSL](#enable-wsl)
  2. [Install a Linux distro](#install-a-linux-distro)
  3. [Update to WSL2](#update-to-wsl2)
    1. [Enable VMP (Virtual Machine Plataform)](#enable-vmp-virtual-machine-plataform)
    2. [Install the Linux kernel](#install-the-linux-kernel)
    3. [Set WSL 2 as the default version](#set-wsl-2-as-the-default-version)
3. [Install Windows Terminal](#install-windows-terminal)
4. [Next steps](#next-steps)
---


# ¿What is WSL?
Before we begin, we should talk about what WSL (Windows Subsystem for Linux) is.


WSL is a compatibility layer developed by Microsoft for running Linux binary executables natively on Windows 10. In simpler words, it allows us to install real Linux distros, like Ubuntu, all inside Windows. This means we can use tools like bash or zsh to manage our Windows files. 🤯

>With WSL, we can run Adobe Photoshop or Microsoft Word in a window and Ubuntu in another. All at the same time!


# Installation of WSL
To install WSL, you must match these requirements:

* Have Windows 10 installed
* Have, at least, 1607 version for WSL 1 and 1903 for WSL 2.
 * *To see your Windows version, follow these steps:*
   1. Press `Windows + R`.
   2. Write "winver" and press enter
* Also, for WSL 2, it is necessary to enable virtualization
 * *To enable it, watch [this video](https://www.youtube.com/watch?v=B1oCkcOHXPA&list=LL&index=12&ab_channel=%EA%A7%81Tut%E2%9C%BFsVicky34%EA%A7%82).*

### Enable WSL
Open PowerShell as administrator and run this command.
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
*When the process finishes, restart your computer.*

### Install a Linux distro
Open Microsoft Store and search "Linux". You can install the distro of your preference, but if you're not sure, I recommend you choose Ubuntu.

![Ubuntu-microsoft-store.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603759079236/WWDXckXTv.png)

When the installation finishes, open Ubuntu and wait until the installation ends. After that, write a new UNIX **username and password**.

![Installing-Ubuntu.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603751635842/kyk9uQSJX.png)

***Don't forget to save your information in a secure place.***

### Update to WSL2
It is the second version of WSL. It increases file system performance and supports full system call compatibility.

*If you want to read a full comparison between versions 1 and 2, read [this blog](https://docs.microsoft.com/en-us/windows/wsl/compare-versions) from Microsoft.*

>For this step, it is mandatory to match all requirements for WSL 2 I mentioned at the [beginning of the installation](#installation-of-wsl). If you don't match the requirements skip this step and [go to the next one](#install-windows-terminal).

Before updating, check your current version by running the following command in PowerShell:

```powershell
wsl -l -v
```

This command will show all distros we have installed and the version of WSL they are running in.

![WSL-version.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1603753788729/tqP7rgcj9.jpeg)

#### Enable VMP (Virtual Machine Plataform)
Now, to enable VMP, you have to run this command in PowerShell:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

*Once the process finishes, restart your computer*

#### Install the Linux kernel
Download the kernel from [this link](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi), execute the installer, and accept all permissions.

#### Set WSL 2 as the default version
Run the following command in PowerShell:

```powershell
wsl --set-default-version 2
```

With this configuration, all distros you install are going to run in WSL 2.

*If you already had a distro installed, you must update it manually with this command:*

```powershell
wsl --set-version Ubuntu 2
```

# Install Windows Terminal
It is an application developed by Microsoft that makes working with multiple terminals easier.

![Windows-terminal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603754651476/ECEFKMVG9.png)

In the Microsoft Store search for "terminal" and install it. Once the installation finishes, open the Windows Terminal app and select the Ubuntu (you can select PowerShell, CMD, or Azure too).

And there you have it! You have, now, WSL installed on your computer. 😎

![Windows-terminal-installed.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1603756300419/51SkhpkK-.jpeg)


# Next steps
Congrats! ⭐ You can now use all the power the terminal has to offer inside your Windows computer without the need for a disk partition. 🤩 However, we still have a problem. The terminal looks kind of ugly. 😥

Well, no worries! In [this post](https://ernestoangulo.hashnode.dev/zsh-oh-my-zsh-una-terminal-hermosa-y-poderosa), I teach you how to make your terminal look awesome. All thanks to Zsh and Oh-My-Zsh. 😉

If this post helped you, please give it a reaction. And If you have any contribution, comment, or recommendation, write it down in the comments section. It helps me a lot to improve my content. 😃 See you in the next post. 👋

---
# Resources

* [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* [https://docs.microsoft.com/en-us/windows/wsl/about](https://docs.microsoft.com/en-us/windows/wsl/about)
---

*If you want to read the Spanish version of this post, you can find it [here](https://netosym.medium.com/sigues-usando-cmd-en-2020-te-presento-a-wsl-f33089c5c791).*