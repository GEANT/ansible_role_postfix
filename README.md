# ansible_role_postfix

Install and configure the `postfix` mailer on Debian


# Example playbooks

Install postfix

```yaml
- hosts: mailers
  become: true

  tasks:
    - import_role:
        name: ansible_role_postfix
```


Same as previous example, but use a smarthost without authentication

```yaml
- hosts: mailers
  become: true

  vars:
    postfix_main:
      relayhost: "[relay.unilely.nl]:587"

  tasks:
    - import_role:
        name: ansible_role_postfix
```

Same as previous example, but use a pcre lookup table, and an aliases file

```yaml
- hosts: mailers
  become: true

    vars:
      postfix_main:
        relayhost: "[relay.unilely.nl]:587"
        smtp_header_checks:
          - path: 'pcre:{{ postfix_config_directory}}/pcre_headers'
            content: '/^From:\s+.*/ REPLACE From: noreply@unilely.nl'
      postfix_maps:
        hash:
          /etc/aliases:
            postmaster: root
            root: john.doe@unilely.nl

  tasks:
    - import_role:
        name: ansible_role_postfix
```

Same as before, but now use authentication on the smarthost


```yaml
- hosts: mailers
  become: true

    vars:
      smtp_username: foobar
      smtp_password: hackme

      postfix_main:
        relayhost: "[relay.unilely.nl]:587"
        smtp_sasl_auth_enable: "yes"
        smtp_sasl_security_options: noanonymous
        smtp_sasl_password_maps: "hash:{{ postfix_config_directory }}/sasl_passwords"
        smtp_header_checks:
          - path: 'pcre:{{ postfix_config_directory}}/pcre_headers'
            content: '/^From:\s+.*/ REPLACE From: noreply@unilely.nl'
      postfix_maps:
        sasl_passwords: "{{ dict([postfix_main.relayhost]|product([smtp_username~':'~smtp_password])) }}"
        hash:
          /etc/aliases:
            postmaster: root
            root: john.doe@unilely.nl

  tasks:
    - import_role:
        name: ansible_role_postfix
```