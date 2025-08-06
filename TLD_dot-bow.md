### Setting up .bow [TLD](TLD.md)

Awesome! Let’s walk through how to set up your own custom top-level domain (TLD) like `.bow`—locally, for development or internal use. This won’t be globally recognized like `.com`, but it’ll work perfectly for your own network or machine.

---

#### 🛠️ Step-by-Step Guide: 
Setting Up `.bow` as a Custom TLD Locally

#### 🔧 **Step 1: Choose Your Domain Name**
Let’s say you want `aohycent.bow` to point to a folder like `/usr/bow/bns/aohycent/www`.

---

#### 🌐 **Step 2: Configure Your Local DNS**

#### Option A: 
Use `/etc/hosts` (Simple, for one machine)
Edit your hosts file:

```bash
sudo nano /etc/hosts
```

Add this line:

```
127.0.0.1 aohycent.bow
```

This tells your computer that `aohycent.bow` is hosted locally.

#### Option B: 
Run a Local DNS Server (Advanced, for multiple devices)
Use software like **dnsmasq** or **Bind9**(recommended) to create a local DNS zone for `.bow`.

Using `dnsmasq`:

1. Install it:
   ```bash
   sudo apt install dnsmasq
   ```

2. Add a config:
   ```bash
   echo "address=/aohycent.bow/127.0.0.1" | sudo tee /etc/dnsmasq.d/bow.conf
   ```

3. Restart:
   ```bash
   sudo systemctl restart dnsmasq
   ```

---

### 🖥️ **Step 3: Set Up Your Web Server**

Use **Apache** or **Nginx** to serve content from `/usr/bow/bns/aohycent/www`.

#### Apache Example:

1. Create a virtual host file:
   ```bash
   sudo nano /etc/apache2/sites-available/aohycent.bow.conf
   ```

2. Add this config:

```apache
<VirtualHost *:80>
    ServerName aohycent.bow
    DocumentRoot /usr/bow/bns/aohycent/www
    <Directory /usr/bow/bns/aohycent/www>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

3. Enable the site:
   ```bash
   sudo a2ensite aohycent.bow.conf
   sudo systemctl reload apache2
   ```

---

### 📁 **Step 4: Place Your Content**

Put your HTML, CSS, or app files in `/usr/bow/bns/aohycent/www`.

---

### ✅ **Step 5: Test It**

Open your browser and go to:

```
http://aohycent.bow
```

You should see your site served from the local folder!

---

### 🧠 Bonus Tip

If you want `.bow` to work across multiple devices on your network:
- Set up a local DNS server (like `dnsmasq`) on your router or a dedicated machine.
- Point other devices to use that DNS server.

---

**up next**

You may need help on scripting automated setup 
`for more` >>
> [automation setup script](DNS_setup-script.md)

Or `dive deeper` into DNS Zone files 
`how to` >>
>  [simulate authoritative responses](DNS_auth-responses.md)
