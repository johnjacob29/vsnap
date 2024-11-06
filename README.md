Move to PROD
=========

Playbook to automate some tasks during move to prod of infra machines. Additionally it´s possible to run only dedicated role(s) via playbook ```role_picker.yml``` which expects ```picked_roles``` variable defined via extra variables or by survey. Playbook supports AIX, RHEL, CentOS and Debian operating systems. Some roles are skipped based on availability of solutions on given platforms.

Requirements
------------

- Requirements are described in roles themself.

Role Variables
--------------

- Playbook is created to follow current Infra security requirements so no special variables or customizations are needed.
- In case test machine is going into production without ITM6, it´s necessary to inform playbook about it with variable below. Some roles which are adding FS or agent updates also ITM6 configuration files. This is automatically disabled for Debian distros.

```
ITM6_used: True       #by default true, setup in extra vars to False if no monitoring is used
```
- As we have multiple "accounts" on infra it´s possible to specify correct trigram for gecos. This is later used when some account is created.
```
gecos_tri: IPX
```
- Playbook role picker allows to use multiple role(s). Best is setup variable ```picked_roles``` in template survey (multiple options) to pass list into playbook. 
- In addition to reflect changes on machines is added role ```modification_update``` which updates file ```/modifications```. Content of update is driven by variable below:
```
new_modification: '30/03/2023 czzz02tz : tenable.io installed (CH30575665)
```

Dependencies
------------

- Dependencies like rpm packages are handled by roles themself (usually), but it´s good to review notes in each role.

Example Playbook
----------------

- Roles are used without parameter as simple list
```
    - hosts: servers
      roles:
         - vsnap
```

Author Information
------------------

Frantisek Slimarik

