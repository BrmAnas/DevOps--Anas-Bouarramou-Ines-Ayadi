Partie 1

2. Create a virtual machine

==> centos_server: Running provisioner: shell...
centos_server: Running: inline script
centos_server: Hello, World

Vagrant status :
The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.

Vagrant halt :
==> centos_server: Attempting graceful shutdown of VM...

Vagrant destroy :
==> centos_server: Destroying VM and associated drives...

3. Check that everything is ok by connecting to the VM via ssh
   ![alt text](image.png)

4. Play with different command for Shell Provisioner

Vagrant provision :
==> centos_server: Running provisioner: shell...
centos_server: Running: inline script

[vagrant@localhost ~]$ cat /etc/hosts
127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4
::1 localhost localhost.localdomain localhost6 localhost6.localdomain6
127.0.0.1 mydomain-1.local

2.  [vagrant@localhost ~]$ cat /etc/vagrant_provisioned_at
    Mon Feb 16 09:22:35 UTC 2026

Part 2. Declarative - GitLab installation using Vagrant and Ansible Provisioner

2. Create and provision a virtual machine (VM)
   PLAY RECAP **********************************\***********************************
   gitlab_server : ok=11 changed=2 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0

Part 3. Declarative - Configure a health check for GitLab

TASK [gitlab/healthchecks : Check GitLab health] **************\*\*\***************
ok: [gitlab_server]

TASK [gitlab/healthchecks : Print GitLab health] **************\*\*\***************
ok: [gitlab_server] => {
"msg": "GitLab OK"
}

5-6

TASK [gitlab/healthchecks : Check GitLab liveness] **************\***************
ok: [gitlab_server]

TASK [gitlab/healthchecks : Check GitLab readiness] ************\*\*\*\*************
ok: [gitlab_server]

TASK [gitlab/healthchecks : Print Liveness and Readiness results] ******\*\*******
ok: [gitlab_server] => {
"msg": [
"Liveness: {'status': 'ok'}",
"Readiness: {'db_check': [{'status': 'ok'}], 'redis_check': [{'status': 'ok'}], 'status': 'ok'}"
]
}

Bonus

TASK [gitlab/healthchecks : Bonus - Custom message for dysfunctional services] \*
ok: [gitlab_server] => {
"msg": "Services en panne : ['redis_check']"
}
