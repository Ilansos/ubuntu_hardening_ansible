# Ubuntu 22.04 Server Hardening with Ansible

This project focuses on hardening an Ubuntu 22.04 server based on the CIS (Center for Internet Security) benchmark guidelines. The hardening is implemented using Ansible playbooks, which automate the configuration tasks to enhance the server's security posture.

## Prerequisites

Before running the Ansible playbooks, ensure that the target Ubuntu 22.04 server meets the following requirements:

1. **Ubuntu 22.04 Server:** The playbooks are designed for Ubuntu 22.04 LTS. Ensure the server is running this version.

2. **Partition Configuration:**
   - The server should be configured with the following partitions:
     - `/tmp`
     - `/var/tmp`
     - `/var/log/audit`
     - `/var/log`
     - `/var`
     - `/home`
   - These partitions should be separate from the root (`/`) partition to enhance security.

3. **SSH Keys**
    - Each server should be accessible using an SSH key. 
    - Recommendation: Use the same SSH key for all hosts and remove it after finishing with the automation to maintain security.

## Ansible

### What is Ansible?

Ansible is an open-source automation tool that automates configuration management, application deployment, and task execution. It uses simple, human-readable YAML files to define automation tasks and does not require agents or additional software to be installed on target systems.

### Installing Ansible

1. **On Ubuntu:**
   ```bash
   sudo apt update
   sudo apt install ansible


## Project Setup

**Inventory File**

The inventory.yml file is used to define the target servers and their connection details. Below is a template of the inventory file:

```yaml
servers:
  hosts:
    10.0.0.X:
      ansible_user: "{{ lookup('env', 'USER_HOST1') }}"
      ansible_become_pass: "{{ lookup('env', 'SUDO_PASS_HOST1') }}"
      root_password: "{{ lookup('env', 'ROOT_PASS_HOST1') }}"
      grub_password: "{{ lookup('env', 'GRUB_PASSWORD_HOST1') }}"
      grub_username: "{{ lookup('env', 'GRUB_USERNAME_HOST1') }}"
    10.0.0.Y:
      ansible_user: "{{ lookup('env', 'USER_HOST2') }}"
      ansible_become_pass: "{{ lookup('env', 'SUDO_PASS_HOST2') }}"
      root_password: "{{ lookup('env', 'ROOT_PASS_HOST2') }}"
      grub_password: "{{ lookup('env', 'GRUB_PASSWORD_HOST2') }}"
      grub_username: "{{ lookup('env', 'GRUB_USERNAME_HOST2') }}"
```

Note: Replace 10.0.0.X and 10.0.0.Y with your actual server IP addresses. Each user should add their hosts and export the necessary environment variables for each host.

**Set Environment Variables:** 

Export the required environment variables for each host. These variables are used for authentication and access control.

Recomendation: For a more secure deployment, use a secrets manager that injects the secrets as environment variables instead of exporting them

```bash
export USER_HOST1="your_username"
export SUDO_PASS_HOST1="your_sudo_password"
export ROOT_PASS_HOST1="your_root_password"
export GRUB_PASSWORD_HOST1="your_grub_password"
export GRUB_USERNAME_HOST1="your_grub_username"

export USER_HOST2="your_username"
export SUDO_PASS_HOST2="your_sudo_password"
export ROOT_PASS_HOST2="your_root_password"
export GRUB_PASSWORD_HOST2="your_grub_password"
export GRUB_USERNAME_HOST2="your_grub_username"
```

**Ansible Configuration File**

Modify the ansible.cfg file to specify the SSH key to use:

```ini
[defaults]
inventory = inventory.yml
private_key_file = /path/to/ssh/key
become_method = sudo
```

### Running the Playbooks

Prepare your environment:
    Ensure that Ansible is installed and configured.
    Set up the inventory file and Ansible configuration as described above.

Run the playbooks:

```bash
    ansible-playbook playbooks/playbook.yml
```

Replace playbook.yml with the actual playbook you wish to run.

### Conclusion

This project provides a framework to harden an Ubuntu 22.04 server using Ansible. By following the CIS benchmark guidelines, you can ensure that your server is configured securely and is less vulnerable to attacks.

For any issues or further customization, consult the Ansible documentation or the CIS Ubuntu Benchmark for additional guidance.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

## Acknowledgements

Special thanks to the Center for Internet Security for their comprehensive benchmark guidelines.