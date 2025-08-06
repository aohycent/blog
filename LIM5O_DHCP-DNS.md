# LIM5O: DHCP & DNS

- TASKS
  - HCP Breakdown
  - DNS Breakdown
  - Mapping a Custom Domain to a Local Path

## 1. **Category**
 - [Networking](Networking)
 - [Web Infrastructure](Web#Infrastructure)

### 2. **Subcategories**  
- DHCP (Dynamic Host Configuration Protocol)  
- DNS (Domain Name System)  
- Domain Mapping & Routing  
- Custom TLD (Top-Level Domain) Setup  
- Local Path Resolution

---

### 3. **LIM5O Explanation**

#### 🧩 **DHCP: Giving Computers Their Names (IP Addresses)**  
Imagine a classroom where every kid needs a name tag. DHCP is the teacher who gives each kid a name tag (IP address) when they walk in. The teacher has a box of name tags and hands one out when asked. If a kid leaves, the tag goes back in the box for someone else to use later.

#### 🧩 **DNS: Finding Friends by Their Nicknames**  
Now, instead of calling your friend by their long number (IP), you call them by their nickname (domain name). DNS is like a magic phonebook that tells you the number when you say the nickname. Some DNS servers are “authoritative,” meaning they’re the boss of that nickname and know exactly where it should go.

#### 🧩 **Authoritative Zone: Who’s the Boss of the Nickname?**  
The authoritative DNS zone is like the teacher who knows which kid owns which nickname. If someone asks, “Who is aohycent.bow?” the teacher checks the list and says, “That’s the kid sitting at /usr/bow/bns/aohycent/www .”

#### 🧩 **Mapping a Domain to a Local Path**  
To make aohycent.bow point to a folder like `/usr/bow/bns/aohycent/www`, you need to:
- Own or simulate the `.bow` TLD (hard in real life, but possible locally)
- Set up a DNS server that says “aohycent.bow = your computer’s IP”
- Configure your web server (like Apache or Nginx) to serve files from that folder when someone visits aohycent.bow

---

### 4. **Extra Nuggets**

- 🛠️ **DHCP Lease**: IP addresses are borrowed, not owned. Computers ask for renewal before the lease expires.
- 🌐 **DNS Zone File**: It’s like a list that says “nickname = number” and “who’s the boss of this nickname.”
- 🧪 **Local TLD Simulation**: You can fake a TLD like `.bow` using your own DNS server and `/etc/hosts` file for testing.
- 🗂️ **Web Server Mapping**: Use `VirtualHost` in Apache or `server_name` in Nginx to link domain to folder.

---

**up next**
- [setting up a unique TLD (step-by-step guide)](TLD_.bow)
  
Or `dive deeper into DNS` >>>

- [zone file structure](DNS_zone)
