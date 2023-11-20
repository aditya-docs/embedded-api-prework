Create a new external user of your Embedded application.

To exclude users from billing you can mark them as test users (see our [Billing page](https://tray.io/documentation/embedded/getting-started/billing/) for more info).

| Required Token | Notes                                                                                                |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following as **inputs**:

| Input            | Required | Note                                                                                                                                                                                                                                                                                                                                             |
| ---------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name             | Yes      |                                                                                                                                                                                                                                                                                                                                                  |
| externalUserId   | Yes      | can be used to link the End User to an ID you already have for them in your external database. <br>It's important to be able to access key info, such as contact email, you may have stored in your external system. Example: dealing with [Expired Auths](https://tray.io/documentation/embedded/core-topics/authentications/managing-expired-auths/) |
| isTestUser       | No       | Boolean value that defaults to `true` (billable user) if you don't pass it. A test user allows you to create Solution Instances and run test data for a user without incurring any charges. This is useful for end to end testing. Please read our billing page <a href="https://tray.io/documentation/embedded/getting-started/billing/#creating-test-users" target="_blank">here</a>.                                                                                                                                                                                                                   |
| clientMutationId | No       | Only relevant if using the Relay GraphQL client                                                                                                                                                                                                                                                                                                  |

Here is an example mutation:

<div class="accordion-button">Create new user</div>
<div class="accordion-body">
<pre>
mutation {
  createExternalUser(input: { 
    name: "Dwight Schrute",
    externalUserId: "my-apps-user-id-for-dwight"
  }) {
    userId
  }
}
</pre>
</div>
<div class="accordion-button">Create new user with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
  createExternalUser(input: { 
    name: "Dwight Schrute",
    externalUserId: "my-apps-user-id-for-dwight",
    clientMutationId: "some-mutation-id" #OPTIONAL - only needed for legacy Relay & Apollo clients
  }) {
    userId
    clientMutationId #OPTIONAL
  }
}
</pre>
</div>

It can return the following data:

| Returned Data    | Notes                                           |
| ---------------- | ----------------------------------------------- |
| userId           | Tray Id of the user                             |
| clientMutationId | Only relevant if using the Relay GraphQL client |
