# Room: Packets & Frames
**Path:** PreSecurity / Module 2 - Network Fundamentals
**Date:** 2025-11-11 | **Time spent:** 60 min

## Key Concepts
- Frame = שכבת לינק (Layer 2). דוגמה: Ethernet frame עם MAC src/dst, EtherType, FCS.
- Packet = שכבת רשת (Layer 3). דוגמה: IPv4 packet עם header (src/dst IP, TTL, protocol).
- Encapsulation: Application → TCP/UDP → IP packet → Ethernet frame.
- MTU & Fragmentation: מה קורה כש-packet גדול מ-MTU של ה-link.
- כתובות: MAC (לינק) מול IP (רשת). ARP ממפה MAC ↔ IP ברשת מקומית.

## Practical Notes / תרגול מעשי
- תרגיל פשוט: הרץ `ping` מ-AttackBox או VM ותפוס חבילות ב-Wireshark/Tcpdump כדי לראות את ה-ICMP packet בתוך Ethernet frame.
- חפש בכותרת ה-Ethernet את שדות ה-src/dst MAC ו-EtherType (0x0800 = IPv4).

## Commands / פקודות לשימוש (AttackBox / Kali / Host)
```bash
# חיבור רשת / בדיקת ממשק ב-Linux
ip a

# חפיפה של חבילות (ריץ מהמכונה שאתה משתמש בה)
sudo tcpdump -i eth0 -w outputs/packets_frames_capture.pcap

# חיפוש ICMP ב-tcpdump (4 חבילות ping)
sudo tcpdump -i eth0 icmp -c 4 -vv

# צפייה בסריקה באמצעות tshark (CLI של wireshark)
tshark -r outputs/packets_frames_capture.pcap -Y "icmp" -V

# פקודת nmap דוגמתית (לא חובה היום)
nmap -sS -Pn <target>
