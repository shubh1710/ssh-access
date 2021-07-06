# ssh-access
Grant or Revoke SSH instructions :

### To add a new user and grant user SSH access
ansible-playbook -i inv -e "action=grant" ssh.yml
```
 [WARNING]: Found variable using reserved name: action


PLAY [servers] ******************************************************************************************************************************************************

TASK [ssh-access : Add new user] ************************************************************************************************************************************
changed: [server1]
changed: [server2]

TASK [ssh-access : Grant user SSH access] ***************************************************************************************************************************
changed: [server1]
changed: [server2]

TASK [ssh-access : Revoke user's SSH access] ************************************************************************************************************************
skipping: [server1]
skipping: [server2]

TASK [ssh-access : Remove the user] *********************************************************************************************************************************
skipping: [server1]
skipping: [server2]

PLAY RECAP **********************************************************************************************************************************************************
server1                    : ok=2    changed=2    unreachable=0    failed=0
server2                    : ok=2    changed=2    unreachable=0    failed=0

```

### To grant SSH access to an existing user (skip adding the user part)
ansible-playbook -i inv -e "action=grant" ssh.yml --skip-tags=add

### To revoke SSH access from an existing user (skip removing the user part)
ansible-playbook -i inv -e "action=revoke" ssh.yml --skip-tags=remove

### To remove user, and thereby revoking the SSH access as well
ansible-playbook -i inv -e "action=revoke" ssh.yml
```
 [WARNING]: Found variable using reserved name: action


PLAY [servers] ******************************************************************************************************************************************************

TASK [ssh-access : Add new user] ************************************************************************************************************************************
skipping: [server1]
skipping: [server2]

TASK [ssh-access : Grant user SSH access] ***************************************************************************************************************************
skipping: [server1]
skipping: [server2]

TASK [ssh-access : Revoke user's SSH access] ************************************************************************************************************************
changed: [server1]
changed: [server2]

TASK [ssh-access : Remove the user] *********************************************************************************************************************************
changed: [server1]
changed: [server2]

PLAY RECAP **********************************************************************************************************************************************************
server1                    : ok=2    changed=2    unreachable=0    failed=0
server2                    : ok=2    changed=2    unreachable=0    failed=0

```

### To check the results login into your "user_name" account and ssh into one of your servers
```
root@ubuntu-sg:~/ansible-projects/ssh-access# ssh -i ./keys/dev/id_rsa dev@10.52.10.148
Web console: https://centos-sg:9090/ or https://10.52.10.148:9090/

Last failed login: Mon Jul  5 19:25:23 UTC 2021 from 10.52.10.221 on ssh:notty
There were 2 failed login attempts since the last successful login.
[dev@centos-sg ~]$
 
```

## P.S.
1. Please make sure to add IPs or DNS of target servers in inv file.
2. Update the inv file with the host ssh_user and private key file generated with ssh-keygen and public key copied to the servers with ssh-copy-id.
3. Update the variable "user_name" and "user_des" in inv file.
4. Create a directory under "keys" directory having the same name as "user_name" and put its SSH public key in it.
