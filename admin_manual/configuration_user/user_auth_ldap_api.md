LDAP Configuration API
======================

Any used method requires the a header "OCS-APIREQUEST" set to "true".
And any method takes an optional "format" parameter, which accepts "xml"
(default) or "json".

Methods
-------

### Creating a configuration

Creates a new and empty LDAP configuration. It returns its ID.
Authentication is done by sending a basic HTTP authentication header.

**Syntax: ocs/v2.php/apps/user\_ldap/api/v1/config**

-   HTTP method: POST

#### Example

-   POST
    `https://admin:secret@example.com/ocs/v2.php/apps/user_ldap/api/v1/config`
    -H "OCS-APIREQUEST: true"
-   Creates a new, empty configuration

#### XML Output

``` {.sourceCode .xml}
<?xml version="1.0"?>
<ocs>
 <meta>
  <status>ok</status>
  <statuscode>200</statuscode>
  <message>OK</message>
 </meta>
 <data>
  <configID>s01</configID>
 </data>
</ocs>
```

### Deleting a configuration

Deletes a given LDAP configuration. Authentication is done by sending a
basic HTTP authentication header.

**Syntax: ocs/v2.php/apps/user\_ldap/api/v1/config/{configID}**

-   HTTP method: DELETE

#### Example

-   DELETE
    `https://admin:secret@example.com/ocs/v2.php/apps/user_ldap/api/v1/config/s02 -H "OCS-APIREQUEST: true"`
-   deletes the LDAP configuration

#### XML Output

``` {.sourceCode .xml}
<?xml version="1.0"?>
<ocs>
 <meta>
  <status>ok</status>
  <statuscode>200</statuscode>
  <message>OK</message>
 </meta>
 <data/>
</ocs>
```

### Reading a configuration

Returns all keys and values of the specified LDAP configuration.
Authentication is done by sending a basic HTTP authentication header.

**Syntax: ocs/v2.php/apps/user\_ldap/api/v1/config/{configID}**

-   HTTP method: GET
-   url argument: showPassword - int, optional, default 0, whether to
    return the password in clear text

#### Example

-   GET
    `https://admin:secret@example.com/ocs/v2.php/apps/user_ldap/api/v1/config/s02?showPassword=1 -H "OCS-APIREQUEST: true"`
-   fetches the LDAP configuration

#### XML Output

``` {.sourceCode .xml}
<?xml version="1.0"?>
<ocs>
 <meta>
  <status>ok</status>
  <statuscode>200</statuscode>
  <message>OK</message>
 </meta>
 <data>
  <ldapHost>ldap://ldap.server.tld</ldapHost>
  <ldapPort>389</ldapPort>
  <ldapBackupHost></ldapBackupHost>
  <ldapBackupPort></ldapBackupPort>
  <ldapBase>ou=Department XLII,dc=example,dc=com</ldapBase>
  <ldapBaseUsers>ou=users,ou=Department XLII,dc=example,dc=com</ldapBaseUsers>
  <ldapBaseGroups>ou=Department XLII,dc=example,dc=com</ldapBaseGroups>
  <ldapAgentName>cn=root,dc=example,dc=com</ldapAgentName>
  <ldapAgentPassword>Secret</ldapAgentPassword>
  <ldapTLS>1</ldapTLS>
  <turnOffCertCheck>0</turnOffCertCheck>
  <ldapIgnoreNamingRules/>
  <ldapUserDisplayName>displayname</ldapUserDisplayName>
  <ldapUserDisplayName2>uid</ldapUserDisplayName2>
  <ldapGidNumber>gidNumber</ldapGidNumber>
  <ldapUserFilterObjectclass>inetOrgPerson</ldapUserFilterObjectclass>
  <ldapUserFilterGroups></ldapUserFilterGroups>
  <ldapUserFilter>(&amp;(objectclass=nextcloudUser)(nextcloudEnabled=TRUE))</ldapUserFilter>
  <ldapUserFilterMode>1</ldapUserFilterMode>
  <ldapGroupFilter>(&amp;(|(objectclass=nextcloudGroup)))</ldapGroupFilter>
  <ldapGroupFilterMode>0</ldapGroupFilterMode>
  <ldapGroupFilterObjectclass>nextcloudGroup</ldapGroupFilterObjectclass>
  <ldapGroupFilterGroups></ldapGroupFilterGroups>
  <ldapGroupMemberAssocAttr>memberUid</ldapGroupMemberAssocAttr>
  <ldapGroupDisplayName>cn</ldapGroupDisplayName>
  <ldapLoginFilter>(&amp;(|(objectclass=inetOrgPerson))(uid=%uid))</ldapLoginFilter>
  <ldapLoginFilterMode>0</ldapLoginFilterMode>
  <ldapLoginFilterEmail>0</ldapLoginFilterEmail>
  <ldapLoginFilterUsername>1</ldapLoginFilterUsername>
  <ldapLoginFilterAttributes></ldapLoginFilterAttributes>
  <ldapQuotaAttribute></ldapQuotaAttribute>
  <ldapQuotaDefault>20 MB</ldapQuotaDefault>
  <ldapEmailAttribute>mail</ldapEmailAttribute>
  <ldapCacheTTL>600</ldapCacheTTL>
  <ldapUuidUserAttribute>auto</ldapUuidUserAttribute>
  <ldapUuidGroupAttribute>auto</ldapUuidGroupAttribute>
  <ldapOverrideMainServer></ldapOverrideMainServer>
  <ldapConfigurationActive>1</ldapConfigurationActive>
  <ldapAttributesForUserSearch>uid;sn;givenname</ldapAttributesForUserSearch>
  <ldapAttributesForGroupSearch></ldapAttributesForGroupSearch>
  <ldapExperiencedAdmin>0</ldapExperiencedAdmin>
  <homeFolderNamingRule>attr:mail</homeFolderNamingRule>
  <hasPagedResultSupport></hasPagedResultSupport>
  <hasMemberOfFilterSupport>1</hasMemberOfFilterSupport>
  <useMemberOfToDetectMembership>1</useMemberOfToDetectMembership>
  <ldapExpertUsernameAttr></ldapExpertUsernameAttr>
  <ldapExpertUUIDUserAttr></ldapExpertUUIDUserAttr>
  <ldapExpertUUIDGroupAttr></ldapExpertUUIDGroupAttr>
  <lastJpegPhotoLookup>0</lastJpegPhotoLookup>
  <ldapNestedGroups>0</ldapNestedGroups>
  <ldapPagingSize>500</ldapPagingSize>
  <turnOnPasswordChange>1</turnOnPasswordChange>
  <ldapDynamicGroupMemberURL></ldapDynamicGroupMemberURL>
  <ldapDefaultPPolicyDN></ldapDefaultPPolicyDN>
 </data>
</ocs>
```

### Modifying a configuration

Updates a configuration with the provided values. Authentication is done
by sending a basic HTTP authentication header.

**Syntax: ocs/v2.php/apps/user\_ldap/api/v1/config/{configID}**

-   HTTP method: PUT
-   url argument: configData - array, see table below for the fields.
    All fields are optional. The values must be url-encoded.

#### Example

-   PUT
    `https://admin:secret@example.com/ocs/v2.php/apps/user_ldap/api/v1/config/s01 -H "OCS-APIREQUEST: true" -d "configData[ldapHost]=ldap%3A%2F%2Fldap.server.tld &configData[ldapPort]=389"`
-   fetches the LDAP configuration

#### XML Output

``` {.sourceCode .xml}
<?xml version="1.0"?>
<ocs>
 <meta>
  <status>ok</status>
  <statuscode>200</statuscode>
  <message>OK</message>
 </meta>
 <data/>
</ocs>
```

Configuration Keys
------------------

  ------------------------------------------------------------------------
  Key           Mo Requ Description
                de ired 
  ------------- -- ---- --------------------------------------------------
  ldapHost      rw yes  LDAP server host, supports protocol

  ldapPort      rw yes  LDAP server port

  ldapBackupHos rw no   LDAP replica host
  t                     

  ldapBackupPor rw no   LDAP replica port
  t                     

  ldapOverrideM rw no   Whether replica should be used instead
  ainServer             

  ldapBase      rw yes  Base

  ldapBaseUsers rw no   Base for users, defaults to general base if not
                        specified

  ldapBaseGroup rw no   Base for groups, defaults to general base if not
  s                     specified

  ldapAgentName rw no   DN for the (service) user to connect to LDAP

  ldapAgentPass rw no   Password for the service user
  word                  

  ldapTLS       rw no   Whether to use StartTLS

  turnOffCertCh rw no   Turns off certificate validation for TLS
  eck                   connections

  ldapIgnoreNam rw no   Backwards compatibility, do not set it.
  ingRules              

  ldapUserDispl rw yes  Attribute used as display name for users
  ayName                

  ldapUserDispl rw no   Additional attribute, if set show on brackets next
  ayName2               to the main attribute

  ldapGidNumber rw no   group ID attribute, needed for primary groups on
                        OpenLDAP (and compatible)

  ldapUserFilte rw no   set by the Settings Wizard (web UI)
  rObjectclass          

  ldapUserFilte rw no   set by the Settings Wizard (web UI)
  rGroups               

  ldapUserFilte rw yes  LDAP Filter used to retrieve user
  r                     

  ldapUserFilte rw no   used by the Settings Wizard, set to 1 for manual
  rMode                 editing

  ldapAttribute rw no   attributes to be matched when searching for users.
  sForUserSearc         separate by ;
  h                     

  ldapGroupFilt rw no   LDAP Filter used to retrieve groups
  er                    

  ldapGroupFilt rw no   used by the Settings Wizard, set to 1 for manual
  erMode                editing

  ldapGroupFilt rw no   set by the Settings Wizard (web UI)
  erObjectclass         

  ldapGroupFilt rw no   set by the Settings Wizard (web UI)
  erGroups              

  ldapGroupMemb rw no   attribute that indicates group members, one of:
  erAssocAttr           member, memberUid, uniqueMember, gidNumber

  ldapGroupDisp rw no   Attribute used as display name for groups,
  layName               required if groups are used

  ldapAttribute rw no   attributes to be matched when searching for
  sForGroupSear         groups. separate by ;
  ch                    

  ldapLoginFilt rw yes  LDAP Filter used to authenticate users
  er                    

  ldapLoginFilt rw no   used by the Settings Wizard, set to 1 for manual
  erMode                editing

  ldapLoginFilt rw no   set by the Settings Wizard (web UI)
  erEmail               

  ldapLoginFilt rw no   set by the Settings Wizard (web UI)
  erUsername            

  ldapLoginFilt rw no   set by the Settings Wizard (web UI)
  erAttributes          

  ldapQuotaAttr rw no   LDAP attribute containing the quote value (per
  ibute                 user)

  ldapQuotaDefa rw no   Default Quota, if specified quota attribute is
  ult                   empty

  ldapEmailAttr rw no   LDAP attribute containing the email address (takes
  ibute                 first if multiple are stored)

  ldapCacheTTL  rw no   How long results from LDAP are cached, defaults to
                        10min

  ldapUuidUserA r  no   set in runtime
  ttribute              

  ldapUuidGroup r  no   set in runtime
  Attribute             

  ldapConfigura rw no   whether this configuration is active. 1 is on, 0
  tionActive            is off.

  ldapExperienc rw no   used by the Settings Wizard, set to 1 for manual
  edAdmin               editing

  homeFolderNam rw no   LDAP attribute to use a user folder name
  ingRule               

  hasPagedResul r  no   set in runtime
  tSupport              

  hasMemberOfFi r  no   set in runtime
  lterSupport           

  useMemberOfTo rw no   Whether to use memberOf to detect group
  DetectMembers         memberships
  hip                   

  ldapExpertUse rw no   LDAP attribute to use as internal username. Might
  rnameAttr             be modified (e.g. to avoid name collisions,
                        character restrictions)

  ldapExpertUUI rw no   override the LDAP servers UUID attribute to
  DUserAttr             identify LDAP user records

  ldapExpertUUI rw no   override the LDAP servers UUID attribute to
  DGroupAttr            identify LDAP group records

  lastJpegPhoto r  no   set in runtime
  Lookup                

  ldapNestedGro rw no   Whether LDAP supports nested groups
  ups                   

  ldapPagingSiz rw no   Number of results to return per page
  e                     

  turnOnPasswor rw no   Whether users are allowed to change passwords
  dChange               (hashing must happen on LDAP!)

  ldapDynamicGr rw no   URL for dynamic groups
  oupMemberURL          

  ldapDefaultPP rw no   PPolicy DN for password rules
  olicyDN               
  ------------------------------------------------------------------------


