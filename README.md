OEM Agent Clearstate
=========

It is simple, few tasks, role to perform clearstate for OEM agents.

Requirements
------------

Tested with OEM 12.1.0.4.


Dependencies
------------

dborysenko.oem-agent-get-home - required

dborysenko.get-fmw-domain-structure - optional


Example Playbook
----------------

Below example is to discover all hosts in a domain hosted by adminserver.example.com and perform clearstate action for each agent across domain hosts.

    site.yml
    
    - hosts: adminserver
      roles:
        - dborysenko.get-fmw-domain-structure

    - hosts: weblogic, adminsu, singlehosts
      gather_facts: False
      roles:
        - dborysenko.oem-agent-get-home
        - dborysenko.oem-agent-clearstate

hosts


    [adminserver]
    adminserver.example.com
    
    [singlehosts]
    
    [weblogic]
    
    [all]
    
    [all:children]
    adminserver
    singlehosts
    weblogic
    
    [all:vars]
    ansible_user=dborysenko
    ansible_become_method=su
    ansible_become_exe=dzdo
    ansible_become_flags="su -"
    
    [deleg]
    oms1.example.com
    
    [deleg:vars]
    ansible_user=oracle
    
Below example is to run clearstate for each host listed in "singlehosts" section. No dborysenko.get-fmw-domain-structure role is required.

    site.yml  
    

    - hosts: weblogic, adminsu, singlehosts
      gather_facts: False
      roles:
        - dborysenko.oem-agent-get-home
        - dborysenko.oem-agent-clearstate

hosts


    [adminserver]   
    
    [singlehosts]
    webserver01.example.com
    webserver02.example.com
    
    [weblogic]
    
    [all]
    
    [all:children]
    adminserver
    singlehosts
    weblogic
    
    [all:vars]
    ansible_user=dborysenko
    ansible_become_method=su
    ansible_become_exe=dzdo
    ansible_become_flags="su -"
    
    [deleg]
    oms1.example.com
    
    [deleg:vars]
    ansible_user=oracle

License
-------

BSD

Author Information
------------------

Dmytro Borysenko borysenus@gmail.com
