## Configure Keycloak

## Configure Flectra

https://odoo-community.org/shop/product/keycloak-auth-integration-4530

https://gitlab.com/flectra-hq/developer-tools

**General Settings** -> **Integrations** -> **OAuth Authentication**

| Key                | Value                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------ |
| Provider name      | `Keycloak`                                                                                 |
| Client ID          | `hq.siliconhills.dev`                                                                      |
| Client Secret      | `some-client-id`                                                                           |
| Allowed Body       | `Log in with Keycloak`                                                                     |
| Authentication URL | `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/auth`             |
| Scope              |                                                                                            |
| Validation URL     | `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/token/introspect` |
| Data URL           | `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/userinfo`         |
