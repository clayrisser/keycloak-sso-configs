## Configure Keycloak

## Configure Rancher

```sh
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout myservice.key -out myservice.cert
```

**Global** -> **Security** -> **Authentication** -> **SAML Keycloak**

| Key                | Value                                                                                                      |
| ------------------ | ---------------------------------------------------------------------------------------------------------- |
| Display Name Field | `DisplayName`                                                                                              |
| User Name Field    | `Username`                                                                                                 |
| UID Field          | `Username`                                                                                                 |
| Groups Field       | `Groups`                                                                                                   |
| Rancher API Host   | `https://orch.example.com`                                                                                 |
| Private Key        | contents of following command `cat myservice.key`                                                          |
| CA Certificate     | contents of following command `cat myservice.cert`                                                         |
| Metadata XML       | contents of following command `curl https://iam.codejam.ninja/auth/realms/master/protocol/saml/descriptor` |

> For **Metadata XML** only copy the `<EntityDescriptor>` section. You will also need to move
> the props from `<EntitiesDescriptor>` to `<EntityDescriptor>`.
