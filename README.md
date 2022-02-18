# SJ Coins LDAP server 

SJ Coins LDAP server helps to test SJ_COINS Auth Server

This server base on the https://github.com/spring-guides/gs-authenticating-ldap


## Configuration
### Setup environment variables.
```
SJ_COINS_TEST_SERVER_PORT=9999
SJ_COINS_TEST_LDAP_LDIF=classpath:test-server.ldif
SJ_COINS_TEST_LDAP_PORT=8389
```
Or with export:
```
export SJ_COINS_TEST_SERVER_PORT=9999
export SJ_COINS_TEST_LDAP_LDIF=classpath:test-server.ldif
export SJ_COINS_TEST_LDAP_PORT=8389
```
## Create custom ldif file
By default, the LDAP registered two users: admin and jdoe. To add new user uou should update the
/src/main/resources/test-server.ldif or crete custom. 

```bash
$ touch /path/to/custom-ldap.ldif
```

```ldif
#### Start requred section
dn: dc=softjourn,dc=com
objectclass: top
objectclass: domain
objectclass: extensibleObject
dc: softjourn

dn: ou=people,dc=softjourn,dc=com
objectclass: top
objectclass: organizationalUnit
ou: people

dn: uid=admin,ou=people,dc=softjourn,dc=com
objectclass: top
objectclass: person
objectclass: organizationalPerson
objectclass: inetOrgPerson
cn: Admin
sn: Admin
uid: admin
userPassword: admin1234

#### End requred section

#### Custom section
dn: uid=test1,ou=people,dc=softjourn,dc=com
objectclass: top
objectclass: person
objectclass: organizationalPerson
objectclass: inetOrgPerson
cn: Test1 Test1
sn: Test1
mail: test1@softjourn.com
uid: test1
userPassword: test1_1234

dn: uid=test2,ou=people,dc=softjourn,dc=com
objectclass: top
objectclass: person
objectclass: organizationalPerson
objectclass: inetOrgPerson
cn: Test2 Test2
sn: Test2
mail: test2@softjourn.com
uid: test2
userPassword: test2_1234
```

Update environment variable:

```
 SJ_COINS_TEST_LDAP_LDIF=file:/path/to/custom-ldap.ldif
```

```
 export SJ_COINS_TEST_LDAP_LDIF=file:/path/to/custom-ldap.ldif
```

### Build and run LDAP server

```bash
$ ./mvnw package
$ java -jar target/authenticating-ldap-0.0.1-SNAPSHOT.jar 
```
Or

```bash
$ ./mvnw spring-boot:run
```

### Access LDAP Server

The LDAP server is available by URL: ldap://localhost:8389

