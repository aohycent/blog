## 🧰 Master Diagnostic Toolkit Script: 

`bowbyter_diag.sh`

- TASK
  - Bundle a **Master Diagnostic Toolkit Script**
  - Build a **Dashboard-style CLI** for your local dev environment.

This will give us a powerful command-line interface to monitor, debug, and manage your `.bow` domain setup, DNS, Apache, and network health.


```bash
#!/bin/bash

# Colors
GREEN='\033[0;32m'
NC='\033[0m' # No Color

echo -e "${GREEN}BowByter Diagnostic Toolkit Starting...${NC}"

# 1. Check Apache Status
echo -e "\n${GREEN}Apache Status:${NC}"
sudo systemctl status apache2 | head -n 10

# 2. Check Bind9 Status
echo -e "\n${GREEN}Bind9 DNS Status:${NC}"
sudo systemctl status bind9 | head -n 10

# 3. Check DNS Resolution
echo -e "\n${GREEN}DNS Resolution for aohycent.bow:${NC}"
dig aohycent.bow
nslookup aohycent.bow

# 4. Check Port Listening
echo -e "\n${GREEN}Listening Ports:${NC}"
sudo netstat -tuln | grep ':80'

# 5. Check /etc/hosts Entry
echo -e "\n${GREEN}/etc/hosts Entry:${NC}"
grep aohycent.bow /etc/hosts

# 6. Check Apache VirtualHost
echo -e "\n${GREEN}Apache VirtualHost Config:${NC}"
cat /etc/apache2/sites-available/aohycent.bow.conf

# 7. Ping Test
echo -e "\n${GREEN}Ping Test to Localhost:${NC}"
ping -c 4 127.0.0.1

# 8. DNS Zone File Check
echo -e "\n${GREEN}DNS Zone File Content:${NC}"
cat /etc/bind/zones/db.bow

echo -e "\n${GREEN}BowByter Diagnostics Complete!${NC}"
```

> 💡 Save as `bowbyter_diag.sh`, then run:

```bash
chmod +x bowbyter_diag.sh
./bowbyter_diag.sh
```

---

## 🖥️ Dashboard-Style CLI: `bowbyter-cli.sh`

This CLI lets you interactively choose diagnostics or actions.

```bash
#!/bin/bash

while true; do
    clear
    echo "⋈🧠 BowByter CLI Dashboard"
    echo "--------------------------"
    echo "1. Check Apache Status"
    echo "2. Check Bind9 Status"
    echo "3. Test DNS Resolution"
    echo "4. View Apache VirtualHost"
    echo "5. View DNS Zone File"
    echo "6. Run Full Diagnostics"
    echo "7. Exit"
    read -p "Choose an option: " choice

    case $choice in
        1) sudo systemctl status apache2 | head -n 10 ;;
        2) sudo systemctl status bind9 | head -n 10 ;;
        3) dig aohycent.bow && nslookup aohycent.bow ;;
        4) cat /etc/apache2/sites-available/aohycent.bow.conf ;;
        5) cat /etc/bind/zones/db.bow ;;
        6) ./bowbyter_diag.sh ;;
        7) echo "Goodbye, BowByter out!" && exit ;;
        *) echo "Invalid option!" ;;
    esac

    read -p "Press Enter to continue..."
done
```

> 💡 Save as `bowbyter-cli.sh`, then run:
```bash
chmod +x bowbyter-cli.sh
./bowbyter-cli.sh
```

---
**up next**

Add logging, export to JSON, 
AND
[web-based dashboard](web-based_dashboard.md)

next?

[integrate with tools](web-based_dashboard.md) like `htop`, `iftop`, or `tcpdump` for deeper diagnostics.
