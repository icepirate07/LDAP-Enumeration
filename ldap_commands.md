# LDAP Enumeration Commands
ldapsearch: @(#) $OpenLDAP: ldapsearch 2.6.9+dfsg-1 (Jan 15 2025 02:30:51) $
        Debian OpenLDAP Maintainers <pkg-openldap-devel@lists.alioth.debian.org>
        (LDAP library: OpenLDAP 20609)


### Use -H to specify LDAP server
### Use -D for the bind DN (User name)
### Use -w to supply password directly
### Use -b to provide the base DN for the search
### Use " " to specify the type of search

```bash
## Format

ldapsearch -H ldap://server -D BindDN -w 'passwd' -b "Base DN" "Search Type"
```

```bash
## Basic User Enumeration

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "*"
```
```bash
## List Machine account quota (MAQ) for the domain

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "(objectClass=domain)" ms-DS-MachineAccountQuota
```
```bash
## List only users

ldapsearch -H ldap://support.htb -D ldap@support.htb -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "dc=support,dc=htb" "(objectClass=user)" sAMAccountName
```
```bash
## Just replace the last attribute
## List all groups

"(objectClass=group)" cn

## Find potential password-containing files

"(objectClass=user)" sAMAccountName info description

## Search for non-default users

"(&(objectClass=user)(!(sAMAccountName=krbtgt))(!(sAMAccountName=guest)))" sAMAccountName


## Find user with specific privileges like remote access

"(&(objectClass=user)(memberOf=*))" sAMAccountName memberOf

## List Domain computers

dNSHostName operatingSystem

## View domain policies

ms-DS-MachineAccountQuota lockoutThreshold
