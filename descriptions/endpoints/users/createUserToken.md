Create an **accessToken** for a given **userId**

A user token allows access to the APIs which require a user token (Create Solution Instance, Get Solution Instances, Create User Auth etc.) and should be passed as a Bearer in the Authorization header when calling those APIs.

**Note**: This access token expires after 2 days

| Required Token | Notes                                                                                                |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following as **inputs**:

| Input            | Required | Notes                                                                                                              |
| ---------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| userId           | Yes      | obtained when creating a user (**Mutations/Users/Create New User**) or getting users (**Queries/Users/Get Users**) |
| clientMutationId | No       | Only relevant if using the Relay GraphQL client                                                                    |

Here is an example mutation:

<div class="accordion-button">Create user token</div>
<div class="accordion-body">
<pre>
mutation {
  authorize(input: {
      userId: "d869ec65-XXXX-XXXX-XXXX-ac5c1a3958b6"
  }) {
    accessToken
  }
}
</pre>
</div>
<div class="accordion-button">Create user token with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
  authorize(input: {
      userId: "d869ec65-XXXX-XXXX-XXXX-ac5c1a3958b6",
      clientMutationId: "my-mutation-id" #OPTIONAL - only needed for legacy Relay & Apollo clients
  }) {
    accessToken
    clientMutationId #OPTIONAL
  }
}
</pre>
</div>

It can return the following data:

| Returned Data    | Notes                                                                                                                                                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| accessToken      | a persistent token (<u>valid for 2 days</u>) that should be securely stored in your application. <br>Allows access to the APIs which require a user token (e.g. createSolutionInstance) |
| clientMutationId | Only relevant if using the Relay GraphQL client                                                                                                                                         |
