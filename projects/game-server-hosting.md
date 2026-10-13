# Game Server Hosting — From Legacy Hardware to a Home Lab

## Overview

This project documents my early experience hosting dedicated game servers on personal hardware. It began with an older Intel-based system running Minecraft Java Edition and evolved through hardware changes and additional multiplayer game servers.

These early experiments introduced me to server administration, managing Java-based applications, starting and maintaining server processes, and troubleshooting issues in a self-hosted environment.

## Stage 1 — Initial Game Server on Intel Core i5-650

### Hardware

- **Motherboard:** ASUS P7P55 LX
- **Storage:**
  - Toshiba OCZ TR150 240GB SSD — primary server storage
  - Kingston A400 240GB SATA III SSD — backup destination
- **CPU:** Intel Core i5-650
- **RAM:** 16 GB DDR3
- **GPU:** NVIDIA GeForce GTX 750 Ti or GTX 1060 6GB, used in different configurations over time
- **Operating system:** Windows Server 2022

### Minecraft Java Edition Server

My first game-server hosting experience involved running a Minecraft Java Edition server directly on Windows Server.

The server files were stored in a dedicated directory, and I launched the server using a Windows batch script (`startserver.bat`). This allowed me to start the server process without using a container platform.

Over time, I experimented with different Minecraft server configurations, including modded servers using Forge and Fabric. I used Java 17 and Java 21, depending on the modpack version and its requirements.

### Don't Starve Together and Valheim Server

I also hosted dedicated servers for Don't Starve Together and Valheim. Both games used their respective dedicated server files provided through Steam, with the recommended configurations adjusted to suit performance and player requirements.

### Remote Player Access

I configured port forwarding on my router to allow players outside my local network to connect directly to the game server.

I also used DuckDNS to associate a hostname with my public IP address. This allowed players to connect using a memorable domain name, such as `example.duckdns.org`, instead of having to remember my public IP address. DuckDNS helped keep the hostname pointed at my current public IP address when it changed.

Before using direct port forwarding, I had experience with tools such as Hamachi and router features such as DMZ to enable remote connections. This helped me understand different approaches to allowing players to connect to services hosted on my home network.

### Server Management

Initially, I managed the server directly through its Windows Server desktop interface. Later, I transitioned to managing it remotely from my main PC using Windows Remote Desktop Protocol (RDP).

The server operated headlessly during normal operation, without requiring a dedicated monitor, keyboard, or mouse. I used RDP to access its desktop interface remotely, while keeping direct access available as a fallback whenever RDP was unavailable.

This setup allowed me to manage the server from my everyday computer while keeping it running independently.

### Automation and Backups

I used Windows scheduled tasks and scripts to automate routine server maintenance and protect server data.

Every Tuesday, a scheduled script created a backup copy of the server directory from the Toshiba OCZ TR150 SSD to the Kingston A400 SSD. To manage storage space, the script deleted the oldest backup when the number of stored backups reached a predefined limit.

### Key Skills and Experience

- Hosting a Minecraft Java Edition server on Windows Server.
- Managing Java-based server applications.
- Using batch scripts to launch server processes.
- Configuring router port forwarding for external connectivity.
- Running dedicated game servers on older hardware.
- Experimenting with different Minecraft server configurations.

### Troubleshooting and Transition to Stage 2

Although the Intel Core i5-650 server had served me for quite some time, it eventually began experiencing intermittent shutdowns and boot failures.

As a temporary workaround, I enabled the **Wake Up After Power Down** BIOS setting to help the machine recover after losing power. I also configured a scheduled task to reboot the server every day at 4:00 AM. However, neither measure resolved the underlying issue.

I began troubleshooting the hardware by testing and swapping different RAM sticks and graphics cards, and eventually testing a different CPU. I later reused the same RAM sticks in the Intel Core i3 system, where they worked normally. This made a fault with the RAM sticks themselves less likely.

The shutdowns and boot failures remained inconsistent on the i5-650 system: it could operate for several days without issues, then shut down unexpectedly and sometimes fail to boot. In some cases, removing and reinserting a RAM stick allowed it to start again, although this did not work consistently.

After extensive testing, I suspected that the motherboard, an **ASUS P7P55 LX**, was faulty. Although I could not conclusively identify the defective component, the inconsistent behaviour and unsuccessful troubleshooting suggested a possible motherboard failure, potentially related to the system's age.

When a more capable Intel Core i3 system became available, I decided to retire the i5-650 machine and move my server workloads to the newer system rather than continue troubleshooting unreliable hardware.

This experience taught me the importance of systematic hardware troubleshooting, distinguishing temporary workarounds from root-cause resolution, and knowing when replacing unreliable hardware is the more practical option.
