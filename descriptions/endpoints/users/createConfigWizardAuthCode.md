Creates an authorization code that is used to configure <a href="https://tray.io/documentation/embedded/building-integrations/the-config-wizard/#introduction" target="_blank">config wizard URL</a> or <a href="https://tray.io/documentation/embedded/core-topics/authentications/auth-only-dialog/#using-auth-only-dialog" target="_blank">auth-only dialog URL</a>. Refer this page on how it's used.

**Note:** This is a one-time use code which expires after 5 minutes

| Required Token | Notes                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following as **inputs**:

| Input            | Required | Notes                                                                                                              |
| ---------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| userId           | Yes      | obtained when creating a user (**Mutations/Users/Create New User**) or getting users (**Queries/Users/Get Users**) |
| clientMutationId | No       | Only relevant if using the Relay GraphQL client                                                                    |

Here is an example mutation:

<div class="accordion-button">Create Config Wizard Auth Code</div>
<div class="accordion-body">
<pre>
mutation {
  generateAuthorizationCode( input: {
    userId: "d869ec65-XXXX-XXXX-XXXX-ac5c1a3958b6"
  }) {
    authorizationCode
  }
}
</pre>
</div>
<div class="accordion-button">Create Config Wizard Auth Code with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
  generateAuthorizationCode( input: {
    userId: "d869ec65-XXXX-XXXX-XXXX-ac5c1a3958b6",
    clientMutationId: "my-mutation-id" #OPTIONAL - only needed for legacy Relay & Apollo clients
  }) {
    authorizationCode
    clientMutationId #OPTIONAL
  }
}
</pre>
</div>

It can return the following data:

| Returned Data     | Notes                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| authorizationCode | this is required to activate the [Configuration Wizard](https://tray.io/documentation/embedded/building-integrations/the-config-wizard/) |
| clientMutationId  | Only relevant if using the Relay GraphQL client                                                                                          |
