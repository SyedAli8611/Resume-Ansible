**Ansible Ad-Hoc commands to deploy**

**Prerequisites**
- Ansible installed on your control node.
- SSH access to the target node(samplenode2).
- The index.html file must be created and saved in your working directory.

Steps:
1. First, ensure that the target node is reachable by running the ping module.
   ansible samplenode2 -m ping
2. Install Apache
   ansible samplenode2 -m package -a "name=apache2 state=present"
3. Create/Edit index.html
   vi index.html
4. Copy index.html to the Apache Directory
   ansible samplenode2 -m copy -a "src=index.html dest=/var/www/html" --become
The --become is used to execute the command with elevated privilages.
5. Start the Apache service
   ansible samplenode2 -m service -a "name=apache2 state=started"



**Ansible Playbook for Web Server Deployment**

**Prerequisites**
- Ansible installed on your control node.
- SSH access to the target node (samplenode2).
- The index.html file must be created or saved in your working directory

Steps:
1. First, ensure that the target node is reachable by running the ping module.
   ansible samplenode2 -m ping
2. Create/Edit index.html
   vi index.html
3. Create the Ansible Playbook
   vi web.yaml
---
- name: Web Deployment
  hosts: samplenode2
  tasks:
    - name: Install Apache
      package:
        name: apache2
        state: present

    - name: Copy index.html to web server
      copy:
        src: index.html
        dest: /var/www/html/index.html
      become: true

    - name: Start Apache service
      service:
        name: apache2
        state: started
4. Run the Ansible Playbook
   ansible-playbook web.yaml
