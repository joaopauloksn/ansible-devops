suite_db2_setup_for_manage
==========================

This role shouldn't need to exist, it should be part of the Manage operator, but is not so we have to do it as a seperate step in the install flow for now.  The role will perform some initial setup on the Db2 instance that is needed to prepare it for use with the Manage application and supports both CP4D version 3.5 and 4.0.

The role will copy a bash script (setupdb.sh) into the Db2 pod and execute it inside the container, this script will perform a number of configuration changes to the database as well as configuring the tablespaces for Maximo Manage because the operator is not yet able to do this itself.

Role Variables
--------------
### db2_instance_name
The name of the db2 instance to execute the setup in.

- **Required**
- Environment Variable: `DB2_INSTANCE_NAME`
- Default Value: None

### db2_namespace
The namespace where the Db2 instance is running.

- Optional
- Environment Variable: `DB2_NAMESPACE`
- Default Value: `db2u`

### db2_username
The username that will be used to connect to the database specified by `db2_dbname`.

- Optional
- Environment Variable: None
- Default Value: `db2inst1`

### db2_dbname
The name of the database in the instance to connect to when executing the setup script.

- Optional
- Environment Variable: None
- Default Value: `BLUDB`

### db2_schema
The name of the Manage schema where the hack should be targeted in.

- Optional
- Environment Variable: None
- Default Value: `maximo`


Example Playbook
----------------

```yaml
- hosts: localhost
  any_errors_fatal: true
  vars:
    db2_instancename: mydb2
  roles:
    - ibm.mas_devops.suite_db2_setup_for_manage
```


License
-------

EPL-2.0
