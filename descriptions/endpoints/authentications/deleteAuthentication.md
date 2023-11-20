Delete a user authentication

| Required token | Notes                                                                                                                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **User**       | obtained after creating a user token ([Users/Mutations/Create User Token](#operation/create-user-token)) <br> the user token is a persistent token (valid for 2 days) that should be securely stored in your application |

The mutation accepts the following as **inputs**:

| Input            | Required | Notes                                                                                                                                                                                                     |
| ---------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| authenticationId | Yes      | obtained with **Queries/Users/Get User Authentications** <br>also see our guide to [Mapping and Editing Auths](https://tray.io/documentation/embedded/core-topics/authentications/mapping-editing-auths/) |
| clientMutationId | No       | Only relevant if using the Relay GraphQL client                                                                                                                                                           |

Here is an example mutation:

<div class="accordion-button">Delete Authentication</div>
<div class="accordion-body">
<pre>
mutation {
  removeAuthentication(input: { 
    authenticationId: "dd36c246-XXXX-XXXX-XXXX-a600be2b39fe"
  }) {
    clientMutationId # REQUIRED - must specify as return field, it will be returned as NULL as it's not passed
  }
}
</pre>
</div>
<div class="accordion-button">Delete Authentication with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
  removeAuthentication(input: { 
    authenticationId: "dd36c246-XXXX-XXXX-XXXX-a600be2b39fe", 
    clientMutationId: "some-mutaion-id"
  }) {
    clientMutationId # REQUIRED - must specify as return field
  }
}
</pre>
</div>

It can return the following data:

| Returned Data    | Notes                                                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| clientMutationId | while this data is only relevant if using the Relay GraphQL client, it is actually <u>required</u> here as currently this mutation does not return any other data |
