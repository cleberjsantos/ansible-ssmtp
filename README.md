Ansible SSMTP Role
==================

[![Build Status](https://travis-ci.org/cleberjsantos/ansible-ssmtp.svg?branch=master)](https://travis-ci.org/cleberjsantos/ansible-ssmtp)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-cleberjsantos.ssmtp-blue.svg)](https://galaxy.ansible.com/cleberjsantos/ansible-ssmtp/)
[![Tag](https://img.shields.io/github/tag/cleberjsantos/ansible-ssmtp.svg)]()
[![Travis CI](https://img.shields.io/travis/cleberjsantos/ansible-ssmtp/master.svg)](http://travis-ci.org/cleberjsantos/ansible-ssmtp)

Installs and configures `ssmtp`.

* installs ssmtp
* configures ssmtp
* manages
* configures service

Requirements
------------

* This role requires Ansible 1.9 or higher.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml).

    
    # The person who gets all mail for userids (UID < 1000, usually the admin)
    # Make this empty to disable rewriting.
    # root=postmaster
    # root=yourmail@mail.com
    ssmtp_root: postmaster

    # The authorization method to use.  If unset, plain text is used.
    # May also be set to “cram-md5”.
    # PLAIN
    # LOGIN -> Using sSMTP with Gmail
    # CRAM-MD5
    ssmtp_auth_method: PLAIN 

    # Email 'From header's can override the default domain?
    # YES - Allow the user to specify their own From: address
    # NO - Use the system generated From: address
    ssmtp_from_override: true

    # Use SSL/TLS before starting negotiation
    ssmtp_start_tls: true 
    ssmtp_tls: true
    
    # The place where the mail goes. The actual machine name is required no
    # MX records are consulted. Commonly mailhosts are named mail.domain.com
    # The mail server (where the mail is sent to), both port 465 or 587 should be acceptable
    # See also http://mail.google.com/support/bin/answer.py?answer=78799
    ssmtp_server: mail

    # The full hostname
    ssmtp_hostname:
    
    # The address where the mail appears to come from for user authentication.
    # rewriteDomain=gmail.com
    ssmtp_rewrite_domain:

    # Username/Password
    ssmtp_auth_user:
    ssmtp_auth_pass:

Installation
------------

Using `ansible-galaxy`:

```
$ ansible-galaxy install cleberjsantos.ssmtp
```

Using `requirements.yml`:

```
- src: cleberjsantos.ssmtp
```

Using `git`:

```
$ git clone https://github.com/cleberjsantos/ansible-ssmtp.git cleberjsantos.ssmtp
```


Example playbook using Gmail
----------------------------

```
- hosts: all
  roles:
    - cleberjsantos.ssmtp
  vars:
    ssmtp_root: username@gmail.com
    ssmtp_mailhub: smtp.gmail.com:587
    ssmtp_rewrite_domain: gmail.com
    ssmtp_auth_user: user@gmail.com
    ssmtp_auth_pass: password
  tags:
    - mail
    - gmail
    - ssmtp
    - sendmail
```

or

```
- hosts: all
  roles:
  - { role: ansible-ssmtp, ssmtp_root: "username@gmail.com",
      ssmtp_server: "smtp.gmail.com:587", ssmtp_rewrite_domain: "gmail.com", 
      ssmtp_auth_user: "user@gmail.com", ssmtp_auth_pass: "password", tags: [mail,gmail,ssmtp,sendmail] }
```

Example playbook using Mandrill 
-------------------------------

```
- hosts: all
  roles:
    - cleberjsantos.ssmtp
  vars:
    ssmtp_root: admin_email@example.com
    ssmtp_auth_method: LOGIN
    ssmtp_mailhub: smtp.mandrillapp.com:587
    ssmtp_auth_user: your_mandrill_email@example.com
    ssmtp_auth_pass: mandrill_api_key
  tags:
    - mail
    - mandrill
    - ssmtp
    - sendmail
```

or

```
- hosts: all
  roles:
  - { role: ansible-ssmtp, ssmtp_root: "admin_email@example.com",
      ssmtp_server: "smtp.mandrillapp.com:587", ssmtp_auth_method: "LOGIN", 
      ssmtp_auth_user: "your_mandrill_email@example.com", ssmtp_auth_pass: "mandrill_api_key", tags: [mail,mandrill,ssmtp,sendmail] }
```

License
-------
GPLv2

Author Information
------------------

Cleber J Santos
