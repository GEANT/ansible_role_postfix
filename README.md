Role Name
=========

Install and configure the postfix mailer

Example playbook
================

    hosts: mailers
    
    vars:
      postfix_main:
        relayhost: "[relay.unilely.nl]:587"
        inet_protocols: ipv4
       postfix_maps:
        hash:
          /etc/aliases:
            postmaster: root
            root: john.doe@unilely.nl
    roles:
      - postfix


In case you need to use PCRE lookup tables, these can be defined as part of the `postfix_main` var, using a `path` and a `content` key. The file name will be created, using the `content`.

    hosts: mailers
    
    vars:
      postfix_main:
        relayhost: "[relay.unilely.nl]:587"
        smtp_header_checks:
          - path: 'pcre:{{ postfix_config_directory}}/pcre_headers'
            content: '^From:\s+.*/ REPLACE From: noreply@unilely.nl'
      postfix_maps:
        hash:
          /etc/aliases:
            postmaster: root
            root: john.doe@unilely.nl

    roles:
      - postfix
    
    
  