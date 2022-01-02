# Windows XP x86
- install os
- install virtualbox guest additions
- set up a shared folder with host
- install software
- take a screenshot

## Software
- [wireshark](https://www.wireshark.org/)
  - on windows xp, install wireshark 1.10
- [Sysinternals](https://download.sysinternals.com/files/SysinternalsSuite.zip)
- [PEiD](http://www.softpedia.com/get/Programming/Packers-Crypters-Protectors/PEiD-updated.shtml)
- [Dependency walker](http://www.dependencywalker.com/)
- [PEview](http://wjradburn.com/software/)
- [Resource Hacker](http://www.angusj.com/resourcehacker/)
- [OllyDbg](http://www.ollydbg.de/download.htm)
- [x64dbg](https://x64dbg.com/)
- [Regshot](https://sourceforge.net/projects/regshot/)
- [ApateDNS](https://www.fireeye.com/services/freeware/apatedns.html)
  - on Windows XP you have to install .Net framework separately
  - no luck with .Net 4 but working ok with .Net 3.5
  - download links at https://www.microsoft.com/net/download/all
- [PE-bear](https://hshrzd.wordpress.com/pe-bear/)
  - The Windows build requires Visual Studio 2010 Redistributable [package](https://github.com/hasherezade/releases/files/1868613/vcredist_x86.zip).

# Making a Win10 malware analysis machine
You *have* to disable Windows Security Real-time protection. However via the Windows Security settings you can only do that temporarily. To deactivate it permanently you have to do the following:
1. Disable Tamper Protection (*important:* do that before changing Group Policy settings)
  - Open Windows Security (type Windows Security in the search box)
  - Virus & threat protection > Virus & threat protection settings > Manage settings
  - Switch Tamper Protection to Off
2. Open Local Group Policy Editor (type gpedit in the search box)
  - Computer Configuration > Administrative Templates > Windows Components > Microsoft Defender Antivirus > Real-time Protection
  - Enable Turn off real-time protection
  - Computer Configuration > Administrative Templates > Windows Components > Microsoft Defender Antivirus
  - Enable Turn off Microsoft Defender Antivirus
3. Reboot
