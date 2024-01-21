# Playbook - Ansible

## Ansible Playbook

1. Replace the <mark style="color:red;">`hosts:`</mark> option to <mark style="color:red;">**localhost**</mark> or other <mark style="color:red;">**host**</mark> of your choice.

```yaml
- name: Fail2ban Installation and Configuration
  hosts: localhost

  tasks:
    - name: System Update
      apt:
        update_cache: yes
      changed_when: false

    - name: Dist Upgrade
      apt:
        upgrade: dist
      register: upgrade_output
    
    - name: Install Fail2ban
      command: sudo apt install fail2ban -y
      become: yes
    
    - name: Copy fail2ban.conf Configuration File
      command: cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local
      become: yes

    - name: Copy jail.conf Configuration File
      command: cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
      become: yes

    - name: Change Bantime in the jail.conf Configuration File
      lineinfile:
        dest: /etc/fail2ban/jail.conf
        regexp: 'bantime  = 10m'
        line: 'bantime  = 60m'
      diff: yes

    - name: Change Maxretry in the jail.conf Configuration File
      lineinfile:
        dest: /etc/fail2ban/jail.conf
        regexp: 'maxretry = 5'
        line: 'maxretry = 3'
      diff: yes

    - name: Enabled Fail2ban Service
      systemd:
        name: fail2ban
        enabled: yes

    - name: Restart Fail2ban Service
      systemd:
        name: fail2ban
        state: restarted
```
