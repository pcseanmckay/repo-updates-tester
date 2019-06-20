Repo Updates Tester
=========

This role is for testing repository updates for various operating systems (OS).
Currently supported OS' are: CentOS 7, Fedora 27 - 30, and Ubuntu 14.04, 16.04, 18.04, 18.10, and 19.04.

This role utilizes molecule to automate the testing.

Requirements
------------

This role requires the molecule python module to be installed and currently either python 2.7 or python 3.7+.
This role also requires the selinux and docker-py python modules to be installed.

NOTE: If using a virtualenv to execute molecule in, selinux currently needs to be installed globally.

Role Variables
--------------

This role currently uses the following default variables:
* ### **_rut_ius_baseurl_**
  rut_ius_baseurl should be set to a url that is hosting the IUS repository you want to use.

  #### Default Value
      rut_ius_baseurl: "https://repo.ius.io/7/$basearch/"

  
* ### **_rut_epel_baseurl_**
  rut_epel_baseurl should should be set to a url that is hosting the EPEL repository you want to use.

  #### Default Value
      rut_epel_baseurl: "http://download.fedoraproject.org/pub/epel/7/$basearch"


* ### **_rut_pypi_index_site_**
  rut_pypi_index_site should should be set to a simple based url that is hosting the pypi index you want to use.

  #### Default Value
      rut_pypi_index_site: "https://pypi.org/simple"


* ### **_rut_pypi_trusted_host_**
  rut_pypi_trusted_host should be set to the dns hostname of the site that is hosting the pypi index you want to use.

  #### Default Value
      rut_pypi_trusted_host: "pypi.org"


* ### **_rut_pip_modules_**
  rut_pip_modules should be set to a list of pypi modules you want to test installing.

  #### Default Value  
      rut_pip_modules:
        - ansible
        - ansible-lint
        - yamllint
        - python-openstackclient


* ### **_rut_private_cert_**
  rut_private_cert should be set to true if you need to install a private CA root or intermediary certificate you use on your network.

  #### Default Value
      rut_private_cert: false


* ### **_rut_private_cert_file_**
  rut_private_cert_file should be set to the name of the private CA root or intermediary cerficate you want to install and should be placed under the files directory for the role.

  #### Default Value
      rut_private_cert_file: "cert.crt"


* ### **_rut_ca_cert_file_**
  rut_ca_cert_file should be set to the tls ca certificate bundle that is used by the OS.

  #### Default Value
      rut_ca_cert_file: "/etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem"


NOTE 1: When using molecule for testing a specific OS, set any default variables you want to overide in the scenario playbook for that OS.

NOTE 2: Each different OS you want to test using molecule should have its own scenario (see molecule documentation) which includes a playbook for that scenario.

Dependencies
------------

None.

Example Playbook
----------------

Example playbook for using the role:
```
- hosts: servers
  roles:
      - { role: repo-updates-tester}
```

Example molecule playbook for testing the role:
```
- name: Converge
  hosts: all
  vars:
    rut_private_cert: true
    rut_private_cert_file: "mydomain.crt"
  roles:
    - role: repo-updates-tester
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a
website (HTML is not allowed).
