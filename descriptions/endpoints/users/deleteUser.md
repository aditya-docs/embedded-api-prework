This mutation is used to delete a user from your Embedded application.

**Note:** Deleting a user will also disable and delete all Solution Instances associated with that user.

| Required Token | Notes                                                                                                |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following as **inputs**:

| Input            | Required | Notes                                                                 |
| ---------------- | -------- | --------------------------------------------------------------------- |
| userId           | Yes      | obtained with **Queries/Users/Get Users**                             |
| clientMutationId | No       | Only relevant if using the [Relay GraphQL client](https://relay.dev/) |

Here is an example mutation:

<div class="accordion-button">Delete user</div>
<div class="accordion-body">
<pre>
mutation {
  removeExternalUser(input: {
      userId: "53824943-XXXX-XXXX-XXXX-088aee14038e"
    }) {
      clientMutationId # REQUIRED - must specify as return field, not required to provide this in mutation function
  }
}
</pre>
</div>
<div class="accordion-button">Delete user with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
  removeExternalUser(input: {
      userId: "53824943-XXXX-XXXX-XXXX-088aee14038e", 
      clientMutationId: "someClientMutationId"
  }) {
      clientMutationId # REQUIRED - must specify as return field
  }
}
</pre>
</div>

It can return the following data:

| Returned Data    | Notes                                                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| clientMutationId | while this data is only relevant if using the Relay GraphQL client, it is actually required here as currently this mutation does not return any other data |
