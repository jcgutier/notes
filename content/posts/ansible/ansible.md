# Ansible

## Windows Ansible

### Administrative Rights

Taken from [Ansible Documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_privilege_escalation.html#administrative-rights)

Many tasks in Windows require administrative privileges to complete. When using the `runas` become method, Ansible will attempt to run the module with the full privileges that are available to the become user. If it fails to elevate the user token, it will continue to use the limited token during execution.

A user must have the SeDebugPrivilege to run a become process with elevated privileges. This privilege is assigned to Administrators by default. If the debug privilege is not available, the become process will run with a limited set of privileges and groups.

To determine the type of token that Ansible was able to get, run the following task:

```yaml
- name: Check my username
  ansible.windows.win_whoami:
  become: true
```

Under the label key, the account_name entry determines whether the user has Administrative rights. Here are the labels that can be returned and what they represent:

- Medium: Ansible failed to get an elevated token and ran under a limited token. Only a subset of the privileges assigned to the user are available during the module execution and the user does not have administrative rights.
- High: An elevated token was used and all the privileges assigned to the user are available during the module execution.
- System: The NT AUTHORITY\System account is used and has the highest level of privileges available.

The output will also show the list of privileges that have been granted to the user. When the privilege value is disabled, the privilege is assigned to the logon token but has not been enabled. In most scenarios, these privileges are automatically enabled when required.

Since release of Ansible 2.5, three service accounts that can be set under become_user are:

- System
- NetworkService
- LocalService

As of Ansible 2.8, become can be used to become a Windows local or domain account without requiring a password for that account. For this method to work, the following requirements must be met:

- The connection user has the SeDebugPrivilege privilege assigned
- The connection user is part of the BUILTIN\Administrators group
- The become_user has either the SeBatchLogonRight or SeNetworkLogonRight user right (this can be get from ansible.windows.win_whoami)
