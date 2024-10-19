**Ansible Ad-Hoc commands to deploy**

**Prerequisites**
- Ansible installed on your control node
- SSH access to the target node(samplenode2).
- The index.html file must be created and saved in your working directory or you can create it later.
Steps
1. Install Apache
   ansible samplenode2 -m package -a "name=apache2 state=present"
2. Create/Edit index.html
   vi index.html
3. Copy index.html to the Apache Directory
   ansible samplenode2 -m copy -a "src=index.html dest=/var/www/html" --become
The --become is used to execute the command with elevated privilages.
4. Start the Apache service
   ansible samplenode2 -m service -a "name=apache2 state=started"
