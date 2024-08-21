playbooks


Requirements:

- SSH key
- Set up each one of these as a separate partition:
{ mount_point: "/tmp" }
{ mount_point: "/var" }
{ mount_point: "/var/tmp" }
{ mount_point: "/home" }
{ mount_point: "/var/log/audit" }
{ mount_point: "/var/log" }

- Set up Environment Variables for:
sudo password
grub username (bootloader)
grub password (bootloader)