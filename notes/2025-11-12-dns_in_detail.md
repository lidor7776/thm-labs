# Room: DNS in Detail
**Path:** PreSecurity / Module 3 - How The Web Works  
**Date:** 2025-11-12  

## Key Concepts
- DNS ממפה שמות דומיין לכתובות IP.
- תהליך הפניה כולל: Resolver → Root → TLD → Authoritative server.
- רשומות נפוצות: A, AAAA, CNAME, MX, PTR.
- DNS עובד לרוב על UDP port 53, אך יכול להשתמש ב-TCP לשאילתות גדולות.
- Caching מקצר זמני תגובה (local & recursive resolver cache).

## Practical Commands
**Windows**
```powershell
nslookup google.com
ipconfig /displaydns
