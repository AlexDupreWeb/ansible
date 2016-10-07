# FIREWALL

Foreword: Stop OVH monitoring

- Connect in SSH mode
- Connect on PROXMOX interface

---

Test firewall is enabled

    pve-firewall status

---

Add CRON task to stop firewall  (every 10 minutes)

    */10 * * * * /etc/init.d/pve-firewall stop

---

From PROXMOX Interface

> Firewall > Options

1. Input Policy DROP => ACCEPT
2. Enabled Firewall => yes

---

Test firewall is enabled

    pve-firewall status

---

Add Group (optional)

- Office
- Alexandre
- OVH

> If you use Groups, add this next rules in Security Group (Button Rules), and add many groups to Firewall Rules.

Add Rules

| Direction | Action | Interface | Macro | Protocol | Source | Source port | Destination | Dest. Port | Comment |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| in | ACCEPT |  | SSH |  | **your_ip** |  |  |  | [Office] SSH Connect |
| in | ACCEPT |  |  | tcp | **your_ip** |  |  | 8006 | [Office] HTTPS Interface |
| in | ACCEPT |  | SSH |  | **your_ip** |  |  |  | [Alexandre] SSH Connect |
| in | ACCEPT |  |  | tcp | **your_ip** |  |  | 8006 | [Alexandre] HTTPS Interface |
| in | ACCEPT |  |  | icmp |  |  |  |  | [All] Accept Ping (OVH) |

> https://docs.ovh.com/pages/releaseview.action?pageId=9928706

---

If firewall run and if you have access to the interface and to the SSH, you can disabled CRON task

---

Don't forget to start OVH monitoring