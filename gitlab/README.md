## Create SAML Client in Keycloak

Go to the Clients page and click the 'Create' button in the right upper corner.

| Key                  | Value                                                 |
| -------------------- | ----------------------------------------------------- |
| Client ID \*         | `gitlab.example.com`                                  |
| Client Protocol      | saml                                                  |
| Client SAML Endpoint | `https://gitlab.example.com/users/auth/saml/callback` |

## Configure SAML Client in Keycloak

### Settings Tab

The next screenshots contain the settings you need to set on your client.

| Key                                  | Value                                                 |
| ------------------------------------ | ----------------------------------------------------- |
| Client ID                            | `gitlab.example.com`                                  |
| Name                                 | `Example GItlab`                                      |
| Description                          | `some description`                                    |
| Enabled                              | ON                                                    |
| Consent Required                     | OFF                                                   |
| Login Theme                          | base                                                  |
| Client Protocol                      | saml                                                  |
| Include AuthnStatement               | ON                                                    |
| Include OneTimeUse Condition         | OFF                                                   |
| Sign Documents                       | ON                                                    |
| Optimize REDIRECT signing key lookup | OFF                                                   |
| Sign Assertions                      | ON                                                    |
| Signature Algorithm                  | RSA_SHA26                                             |
| SAML Signature Key Name              | KEY_ID                                                |
| Canonicalization Method              | EXCLUSIVE                                             |
| Encrypt Assertions                   | OFF                                                   |
| Client Signature Required            | ON                                                    |
| Force POST Binding                   | ON                                                    |
| Front Channel Logout                 | ON                                                    |
| Force Name ID Format                 | OFF                                                   |
| Name ID Format                       | persistant                                            |
| Root URL                             | `https://gitlab.example.com`                          |
| Valid Redirect URIs                  | `https://gitlab.example.com/users/auth/saml/callback` |
| Base URL                             | `/`                                                   |
| Master SAML Processing URL           | `https://gitlab.example.com/users/auth/saml/callback` |
| IDP Initiated SSO URL Name           |                                                       |
| IDP Initiated SSO Relay State        |                                                       |

####Fine Grain SAML Endpoint Configuration:

| Key                                             | Value                                                 |
| ----------------------------------------------- | ----------------------------------------------------- |
| Assertion Consumer Service POST Binding URL     | `https://gitlab.example.com/users/auth/saml/callback` |
| Assertion Consumer Service Redirect Binding URL |                                                       |
| Logout Service POST Binding URL                 |                                                       |
| Logout Service Redirect Binding URL             |                                                       |

### Roles Tab

Create New role using 'Add Role' button.
Add Roles as below and set the Composite to false for both.

| Role Name                   | Composite |
| --------------------------- | --------- |
| gitlab.example.com:access   | false     |
| gitlab.example.com:external | false     |

### Mappers Tab

The create mappers configuration as:

- Name: `name`

  - Mapper Type: `User Property`
  - Property: `Username`
  - Friendly Name: `Username`
  - SAML Attribute Name: `name`
  - SAML Attribute NameFormat: Basic

- Name: `email`

  - Mapper Type: `User Property`
  - Property: `Email`
  - Friendly Name: `Email`
  - SAML Attribute Name: `email`
  - SAML Attribute NameFormat: Basic

- Name: `first_name`

  - Mapper Type: `User Property`
  - Property: `FirstName`
  - Friendly Name: `First Name`
  - SAML Attribute Name: `first_name`
  - SAML Attribute NameFormat: Basic

- Name: `last_name`

  - Mapper Type: `User Property`
  - Property: `LastName`
  - Friendly Name: `Last Name`
  - SAML Attribute Name: `name`
  - SAML Attribute NameFormat: Basic

- Name: `roles`

  - Mapper Type: `Role list`
  - Role attribute name: `roles`
  - Friendly Name: `Roles`
  - SAML Attribute NameFormat: Basic
  - Single Role Attribute: On

- All of the mappers have “Consent Required” set to Off.

### Scope Tab

### Installation Tab

Select Format Option to `Keycloak SAML Adapter keycloak-saml.xml` and download the file using the download button.
Copy the content between `<certificatePem>` and `</certificatePem>` and save in your machine

## Configure gitlab

```
     {
         name: 'saml',
         label: '<LABEL>',
         groups_attribute: 'roles',
         external_groups: ['<CLIENT-ID-GIVEN-DURING-CREATION>:external'],
         args: {
           assertion_consumer_service_url: '{{ template "gitlab.gitlab-base-url" . }}/users/auth/saml/callback',
           idp_cert_fingerprint_algorithm: 'http://www.w3.org/2000/09/xmldsig#sha1',
           idp_cert: '-----BEGIN CERTIFICATE-----<SAVED-CERTIFICATE>-----END CERTIFICATE-----',
           idp_sso_target_url: '<KEYCLOAK-URL>/auth/realms/<CREATED-REALM-NAME>/protocol/saml/clients/<CLIENT-ID-GIVEN-DURING-CREATION>',
           issuer: '<CLIENT-ID-GIVEN-DURING-CREATION>',
           name_identifier_format: 'urn:oasis:names:tc:SAML:2.0:nameid-format:persistent',
           attribute_statements: {
             first_name: ['first_name'],
             last_name: ['last_name'],
             name: ['name'],
             username: ['name'],
             email: ['email']
           }
         }
      }
```
