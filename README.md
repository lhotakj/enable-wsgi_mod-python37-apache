# enable-wsgi_mod-python37-apache
## A simple Ansible script compiling Python 3.7.3 with mod_wsgi and configuring it in Apache
Big thanks to [Graham Dumpleton](https://github.com/GrahamDumpleton) and his project https://github.com/GrahamDumpleton/mod_wsgi.
Feel free to share or modify it as you need. You might want to update Python version or wsgi_module variable to newer version once they become available.

### Requirements 
- Centos / RedHat distro with sudo rights
- [Ansible](https://www.ansible.com/)
```
sudo yum install epel-release
sudo yum install ansible
```

### Installation
Simply run ansible playbook `install.yaml`. 
Please note the installation stops if Python version 3.7.3 is installed already.  
```
ansible-playbook ./install.yaml
```

### Uninstall
Remove all softlinks, folders and files created, restart Apache

### Post-install check
To make sure the mod_wsgi is loaded, check the HTTP header `Server`. Assuming your webserver runs at port 80
```
curl -s -I -X GET http://localhost | grep "Server:"
```
the output should contain `wsgi_mod/` and `Python/` with proper versions.
```
Server: Apache/2.4.6 (CentOS) mod_wsgi/4.6.5 Python/3.7 PHP/7.2.20
```


### TO DO List
1. Pre install check validates only if Python 3.7.3 is installed, but does not check `mod_wsgi` version
2. Limited OS support. PR welcomed :) 
3. No ansible playbook for uninstall

