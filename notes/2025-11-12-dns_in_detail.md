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
## 🌐 DNS Lookup Process
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
| **Step** | **Description** |
|-----------|----------------|
| **1. Local Cache Check** | When you request a domain name, your computer first checks its local cache to see if the IP address is already stored. If not, it sends a request to the **Recursive DNS Server**. |
| **2. Recursive DNS Server** | This server is usually provided by your ISP, but you can also choose your own. It checks its own local cache for the requested domain. If found, it returns the result to your computer. If not, it begins the lookup process starting with the **Root DNS Servers**. |
| **3. Root DNS Server** | Acts as the backbone of the DNS system. Its job is to identify the domain’s top-level extension (like `.com` or `.org`) and refer the request to the corresponding **TLD (Top Level Domain) Server**. For example, a request for `www.tryhackme.com` is directed to the TLD server that manages `.com` domains. |
| **4. TLD (Top Level Domain) Server** | This server stores information about where to find the **Authoritative DNS Server** for the requested domain. For example, the nameservers for `tryhackme.com` are `kip.ns.cloudflare.com` and `uma.ns.cloudflare.com`. Multiple nameservers exist for redundancy. |
| **5. Authoritative DNS Server** | The authoritative server stores the domain’s official DNS records and returns the result to the Recursive DNS Server. The result is cached based on the **TTL (Time To Live)** value, which defines how long it can be stored locally before it must be refreshed. This final step resolves the domain name to its IP address. |

---

✅ **Summary:**  
The DNS lookup process converts a human-readable domain (like `tryhackme.com`) into a machine-readable IP address through a chain of servers — from your local cache to the authoritative DNS server — ensuring accurate and efficient communication across the internet.
**תרגום לעברית**
| **שלב**                           | **תיאור**                                                                                                                                                                                                              |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. בדיקת המטמון המקומי**        | כאשר אתה מבקש שם דומיין, המחשב שלך קודם כל בודק את המטמון המקומי (Local Cache) כדי לראות אם כתובת ה־IP כבר מאוחסנת אצלו. אם לא – הוא שולח בקשה לשרת ה־**Recursive DNS**.                                               |
| **2. שרת Recursive DNS**          | שרת זה מסופק בדרך כלל על־ידי ספק האינטרנט (ISP), אך ניתן לבחור גם שרת עצמאי. הוא בודק אם יש תוצאה במטמון שלו. אם כן – היא נשלחת למחשב שלך. אם לא – מתחיל חיפוש שמתחיל בשרתי ה־Root DNS של האינטרנט.                    |
| **3. שרת Root DNS**               | משמש כעמוד השדרה של מערכת ה־DNS. תפקידו לזהות את סיומת הדומיין (למשל .com או .org) ולהפנות לשרת ה־**TLD (Top Level Domain)** המתאים. לדוגמה, בקשה ל־`www.tryhackme.com` תופנה לשרתים שמנהלים דומיינים מסוג `.com`.     |
| **4. שרת TLD (Top Level Domain)** | שרת זה מחזיק רשומות שמציינות היכן נמצא השרת הסמכותי (Authoritative Server) עבור הדומיין. לדוגמה, ה־Name Servers של `tryhackme.com` הם `kip.ns.cloudflare.com` ו־`uma.ns.cloudflare.com`. לרוב קיימים כמה שרתים לגיבוי. |
| **5. שרת Authoritative DNS**      | השרת הסמכותי שומר את רשומות ה־DNS של הדומיין ומחזיר את התוצאה לשרת ה־Recursive. התשובה נשמרת במטמון לפי ערך ה־**TTL (Time To Live)**, כדי לחסוך שאילתות DNS חוזרות. כך מתבצע הפתרון הסופי של שם הדומיין לכתובת IP.     |
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
