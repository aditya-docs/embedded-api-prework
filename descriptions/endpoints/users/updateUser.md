Can be used to mark a user as a test user allowing you to create Solution Instances and run test data for a user without incurring any charges (see our [Billing page](https://tray.io/documentation/embedded/getting-started/billing/) for more info)

| Required Token | Notes                                                                                                |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following as **inputs**:

| Input      | Required | Note                                                                                                                          |
| ---------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| id         | Yes      |                                                                                                                               |
| isTestUser | Yes      | Booelan value. A test user allows you to create Solution Instances and run test data for a user without incurring any charges |

Here is an example mutation:

<div class="accordion-button">Update to test user</div>
<div class="accordion-body">
<pre>
mutation {
   updateExternalUser(input: {
      userId: "53824943-XXXX-XXXX-XXXX-088aee14038e",
      isTestUser: true
  }) {
    user{
			name
			id
			externalUserId
			isTestUser
		}
  }
}
</pre>
</div>
<div class="accordion-button">Update to test user with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
   updateExternalUser(input: {
      userId: "53824943-XXXX-XXXX-XXXX-088aee14038e",
      isTestUser: "true",
      clientMutationId: "some-mutation-id" #OPTIONAL - only needed for legacy Relay & Apollo clients
  }) {
    user{
			name
			id
			externalUserId
			isTestUser
      clientMutationId #OPTIONAL
		}
  }
}
</pre>
</div>

It can return the following data:

| Returned Data  | Notes |
| -------------- | ----- |
| name           |       |
| id             |       |
| externalUserId |       |
| isTestUser     |       |
