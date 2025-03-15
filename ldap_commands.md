## LDAP Enumeration Commands

## Use -H to specify LDAP server
## Use -D for the bind DN (User name)
## Use -w to supply password directly
## Use -b to provide the base DN for the search
## Use "*" to specify the type of search

## Basic User Enumeration
```bash

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "*"

## List only users

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "(objectClass=user)" sAMAccountName

## List all groups

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "(objectClass=group)" cn

## Find potential password-containing files

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "(objectClass=user)" sAMAccountName info description

## Search for non-default users

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "(&(objectClass=user)(!(sAMAccountName=krbtgt))(!(sAMAccountName=guest)))" sAMAccountName


## Find user with specific privileges like remote access
ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "(&(objectClass=user)(memberOf=*))" sAMAccountName memberOf

## List Domain computers

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" dNSHostName operatingSystem

## View domain policies

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" ms-DS-MachineAccountQuota lockoutThreshold
