# Game Server Hosting — From Legacy Hardware to a Home Lab

## Overview

This project documents my early experience hosting dedicated game servers on personal hardware. It began with an older Intel-based system running Minecraft Java Edition and evolved through hardware changes and additional multiplayer game servers.

These early experiments introduced me to server administration, managing Java-based applications, starting and maintaining server processes, and troubleshooting issues in a self-hosted environment.

## Stage 1 — Initial Game Server on Intel Core i5-650

### Hardware

| Component | Specification |
|---|---|
| Motherboard | ASUS P7P55 LX |
| CPU | Intel Core i5-650 |
| RAM | 16 GB DDR3 |
| Primary Storage | Toshiba OCZ TR150 240 GB SSD |
| Backup Storage | Kingston A400 240 GB SATA III SSD |
| GPU | NVIDIA GeForce GTX 750 Ti or GTX 1060 6GB, used in different configurations over time |
| Operating System | Windows Server 2022 |

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

### Lessons Learned

- Hosting Minecraft Java Edition and other dedicated game servers on Windows Server.
- Managing Java versions and modded Minecraft server configurations.
- Using Windows batch scripts to launch server processes.
- Configuring port forwarding and dynamic DNS for external player access.
- Automating routine maintenance and backups with scripts and scheduled tasks.
- Troubleshooting inconsistent shutdowns and boot failures through hardware testing.
- Recognizing the limitations of temporary workarounds and the importance of investigating underlying hardware faults.

### Troubleshooting and Transition to Stage 2

Although the Intel Core i5-650 server had served me for quite some time, it eventually began experiencing intermittent shutdowns and boot failures.

As a temporary workaround, I enabled the **Wake Up After Power Down** BIOS setting to help the machine recover after losing power. I also configured a scheduled task to reboot the server every day at 4:00 AM. However, neither measure resolved the underlying issue.

I began troubleshooting the hardware by testing and swapping different RAM sticks and graphics cards, and eventually testing a different CPU. I later reused the same RAM sticks in the Intel Core i3 system, where they worked normally. This made a fault with the RAM sticks themselves less likely.

The shutdowns and boot failures remained inconsistent on the i5-650 system: it could operate for several days without issues, then shut down unexpectedly and sometimes fail to boot. In some cases, removing and reinserting a RAM stick allowed it to start again, although this did not work consistently.

After extensive testing, I suspected that the motherboard, an **ASUS P7P55 LX**, was faulty. Although I could not conclusively identify the defective component, the inconsistent behaviour and unsuccessful troubleshooting suggested a possible motherboard failure, potentially related to the system's age.

When a more capable Intel Core i3 system became available, I decided to retire the i5-650 machine and move my server workloads to the newer system rather than continue troubleshooting unreliable hardware.

This experience taught me the importance of systematic hardware troubleshooting, distinguishing temporary workarounds from root-cause resolution, and knowing when replacing unreliable hardware is the more practical option.

## Stage 2 — Hardware Transition and Troubleshooting

### Background

Stage 2 involved transitioning from my original Intel Core i5-650 server to a newer system based on an Intel Core i3-4170. The newer machine had previously been abandoned due to a network issue and was given to me.

I formatted the PC and installed Windows Server 2022. During setup, I also tested different Windows Server versions while investigating intermittent problems involving the network, drivers, software conflicts and potentially faulty hardware.

The main purpose of this transition was to move to a newer CPU and platform, providing more performance headroom for existing workloads and greater flexibility for future configurations.

### Hardware Configuration

| Component | Specification |
|---|---|
| CPU | Intel Core i3-4170 @ 3.70 GHz |
| Motherboard | ASUSTeK COMPUTER INC. A_F_K31ADE |
| RAM | 16 GB DDR3 1600 MHz (2 × 8 GB Patriot) |
| Storage | Kingston A400 240 GB SATA SSD |
| Graphics | Intel 4th Generation Core Processor Family Integrated Graphics Controller |
| Onboard Ethernet | Intel Ethernet Connection I217-V (non-functional) |
| PCIe Ethernet Adapter | Realtek RTL8125, advertised up to 2.5 Gbps |
| USB Ethernet Adapter | Amazon Basics USB 2.0 10/100 Mbps Ethernet adapter |
| Operating system | Windows Server 2022 |

### Memory Configuration

The PC originally came with 8 GB of RAM (2 × 4 GB). I replaced these modules with two 8 GB Patriot DDR3 1600 MHz modules, restoring the 16 GB capacity I had in my previous i5-650 system.

Although the i3 system had only two RAM slots, its motherboard supported up to 8 GB per slot. In comparison, the ASUS P7P55 LX motherboard in my previous i5 system supported a maximum of 4 GB per slot. This allowed me to retain the same total memory capacity using fewer RAM slots.

### Network Troubleshooting

During the initial setup, the network connection was limited to approximately 100 Mbps, even when using the PCIe Realtek RTL8125 adapter, which was advertised to support speeds of up to 2.5 Gbps.

To investigate the speed limitation, I:

- Replaced Ethernet cables and tested a self-made Ethernet cable.
- Tried using the motherboard's onboard Intel I217-V Ethernet connection, but it did not work.
- Checked BIOS settings and available Ethernet duplex configuration options.

I also tested an Amazon Basics USB Ethernet adapter, which restored connectivity but was limited to 100 Mbps by its hardware specifications.

Eventually, the network connection stopped working completely. Only at this point did I test different router ports using another PC. These tests helped me identify a damaged router port.

After contacting my ISP, I obtained a replacement router. With the new router, the PCIe Realtek RTL8125 adapter worked correctly and reached approximately 1000 Mbps, matching my 1 Gbps internet connection.

The onboard Intel I217-V Ethernet connection remained unusable, and the cause of its failure was not confirmed.

This troubleshooting process highlighted the importance of investigating the entire network path rather than assuming that an adapter, cable or software configuration was responsible for a connectivity problem.

### Game Server Deployment

I hosted several game servers on the system, running one server at a time:

- Minecraft with the FTB Evolution modpack.
- Minecraft with the All the Mods 9 (ATM9) modpack.
- Minecraft with the All the Mods 10 (ATM10) modpack.
- Valheim.

These servers performed well even while the network connection was temporarily limited to approximately 100 Mbps.

The transition to the i3 system was intended to provide more performance headroom for existing workloads and greater flexibility for future configurations. It was not necessary to make these particular servers possible, as I had already hosted demanding game servers on the previous system.

### Unexpected Shutdowns and CPU Temperature Troubleshooting

While running an All the Mods 9 (ATM9) Minecraft server with 14 GB of RAM allocated and approximately 4–6 players connected, I began experiencing unexpected system shutdowns. This was a demanding workload for an older machine running a heavily modded Minecraft server.

The shutdowns occurred approximately three or four times while I was away from home and unable to investigate immediately. The PC automatically powered back on because the BIOS had the **Wake Up to the Last State** option enabled.

To investigate the problem, I followed these steps:

1. **Checked Windows Event Viewer:** Examined the system logs around the times of the unexpected shutdowns to gather more information about the incidents.
2. **Monitored CPU temperatures:** Suspecting overheating, I installed HWiNFO, which showed that the CPU temperatures were too high.
3. **Cleaned the system:** Removed the CPU cooler and cleaned dust and debris from the PC.
4. **Replaced the rear fan:** Installed a spare 140 mm fan in place of the existing rear fan.
5. **Reapplied thermal paste:** Applied new Mars Gaming thermal paste before reinstalling the CPU cooler.

The unexpected shutdowns were caused by CPU overheating. After cleaning the system, replacing the rear fan and applying fresh thermal paste, CPU temperatures improved and the shutdown problem was resolved. I do not recall experiencing further problems with this system afterward.

### Remote Management

I managed the server using Windows Remote Desktop Protocol (RDP), both from within the local network and remotely when needed.

This allowed me to configure and maintain the server without requiring direct access to its peripherals. I also used remote access during LAN parties, allowing me to manage the server from another PC while friends connected to the hosted game server.

### Lessons Learned

- **Network fault isolation:** Identifying a damaged router port through testing and confirming that replacing the router restored the PCIe Ethernet adapter's expected performance.
- **Hardware troubleshooting:** Using Windows Event Viewer and HWiNFO to investigate unexpected shutdowns and identify CPU overheating.
- **Preventative maintenance:** Cleaning the system, replacing a case fan and renewing thermal paste to resolve overheating.
- **Remote administration:** Managing game servers through RDP from both the local network and remote locations.
- **Hardware compatibility:** Comparing motherboard memory limitations and replacing RAM modules to maintain the previous system's 16 GB capacity.

## Skills Developed

Across both stages, I gained practical experience in the following areas:

- **Windows Server administration:** Installing and managing Windows Server, configuring server environments and maintaining dedicated game-server applications.
- **Game server hosting:** Deploying Minecraft Java Edition, modded Minecraft, Don't Starve Together and Valheim dedicated servers.
- **Application and runtime management:** Managing Java versions, configuring modded server environments and launching applications through batch scripts.
- **Networking:** Configuring router port forwarding, dynamic DNS and external player access; testing Ethernet adapters and cables; and diagnosing network connectivity and speed limitations.
- **Hardware troubleshooting and maintenance:** Testing RAM, graphics cards and CPUs; investigating suspected motherboard faults; monitoring CPU temperatures; cleaning hardware; replacing a case fan; and applying thermal paste.
- **Remote administration:** Using Windows Remote Desktop Protocol to manage servers without requiring direct physical access.
- **Automation and backups:** Using Windows scheduled tasks and scripts to automate maintenance, copy server data and rotate backups.
- **System monitoring and diagnostics:** Using Windows Event Viewer and HWiNFO to investigate unexpected shutdowns and hardware-related problems.
- **Problem-solving:** Isolating possible causes, testing individual components, distinguishing temporary workarounds from actual resolutions, and verifying whether corrective actions solve the problem.

This project documents my progression from experimenting with game servers on older consumer hardware to maintaining a more capable home-server system. It demonstrates practical experience in server administration, networking, hardware maintenance and troubleshooting, while providing a foundation for further development in systems administration and IT infrastructure.
