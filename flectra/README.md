## Configure Keycloak

## Configure Flectra

**General Settings** -> **Integrations** -> **OAuth Authentication**

| Key                | Value                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------ |
| Provider name      | `Keycloak`                                                                                 |
| Client ID          | `hq.siliconhills.dev`                                                                      |
| Client Secret      | `54eb3461-6e66-4c15-8a82-8b7520d4ea92`                                                     |
| Allowed Body       | `Log in with Keycloak`                                                                     |
| Authentication URL | `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/auth`             |
| Scope              |                                                                                            |
| Validation URL     | `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/token/introspect` |
| Data URL           | `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/userinfo`         |
