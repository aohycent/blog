## 🛠️ **Bind9 Zone File & Config Automation Script**

This script sets up a `.bow` domain with Bind9 as the authoritative DNS server.

### 🔧 Script: `setup_bind9_bow.sh`

```bash
#!/bin/bash

# Variables
DOMAIN="bow"
ZONE_FILE="/etc/bind/zones/db.bow"
ZONE_DIR="/etc/bind/zones"
NAMED_CONF="/etc/bind/named.conf.local"

# Step 1: Create zone directory
sudo mkdir -p "$ZONE_DIR"

# Step 2: Create zone file
sudo bash -c "cat > $ZONE_FILE" <<EOF
\$TTL 86400
@   IN  SOA ns1.$DOMAIN. admin.$DOMAIN. (
        2025080701 ; Serial
        3600       ; Refresh
        1800       ; Retry
        604800     ; Expire
        86400 )    ; Minimum

    IN  NS  ns1.$DOMAIN.
ns1 IN  A   127.0.0.1
aohycent IN A   127.0.0.1
EOF

# Step 3: Add zone to named.conf.local
sudo bash -c "cat >> $NAMED_CONF" <<EOF

zone "$DOMAIN" {
    type master;
    file "$ZONE_FILE";
};
EOF

# Step 4: Restart Bind9
sudo systemctl restart bind9

echo "✅ Bind9 zone for .$DOMAIN configured and running!"
```

---

## 🔍 **Testing DNS Queries with `dig` and `nslookup`**

| Tool      | Command Example                          | Purpose                                 |
|-----------|-------------------------------------------|-----------------------------------------|
| `dig`     | `dig aohycent.bow`                        | Basic DNS lookup                        |
|           | `dig aohycent.bow A`                      | Query A record                          |
|           | `dig @127.0.0.1 aohycent.bow`             | Use local DNS server                    |
|           | `dig +trace aohycent.bow`                 | Trace DNS resolution path               |
| `nslookup`| `nslookup aohycent.bow`                   | Basic lookup                            |
|           | `nslookup -type=A aohycent.bow`           | Query A record                          |
|           | `nslookup aohycent.bow 127.0.0.1`         | Use specific DNS server                 |

---

## 🧰 **Common & Advanced Network Issues + Debug Scripts**

| Issue                        | Symptom                          | Debug Command                          | Fix Script Snippet |
|-----------------------------|----------------------------------|----------------------------------------|--------------------|
| DNS not resolving           | “Server not found”               | `dig` / `nslookup`                     | Check zone file, restart Bind9 |
| IP conflict                 | “Network unreachable”            | `ip addr` / `arp -a`                   | Reassign static IP |
| No internet                 | “Ping fails”                     | `ping 8.8.8.8` / `traceroute`          | Restart network service |
| Firewall blocking           | “Connection refused”             | `ufw status` / `iptables -L`           | Allow port via `ufw allow` |
| Port not listening          | “Connection timeout”             | `netstat -tulpn` / `ss -tuln`          | Start service or fix config |
| Slow network                | “Lag or delay”                   | `iperf` / `ping`                       | Check bandwidth, QoS settings |
| MAC/IP mismatch             | “No route to host”               | `arp` / `ip neigh`                     | Clear ARP cache |
| DNS cache stale             | “Wrong IP returned”              | `systemd-resolve --flush-caches`       | Flush DNS cache |

---

**up next**

bundle a master 
`for`  >>>

> [diagnostic toolkit script](toolkit-script.md) 
next?

`Or`  >>>

> [building a dashboard-style CLI](CLI_dashboard-build.md) 

`for` >>>

> [local dev environment](#dev-env)
