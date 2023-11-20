Create a user authentication for a service (e.g. Dropbox or Airtable) that is used in your Embedded application.

For full instructions on using this mutation please see [Importing Authentications](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/)

To generate the inputs needed, navigate to your Tray and scroll down to the section titled 'Authentication import generator'

| Required Token | Notes                                                                                                                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **User**       | obtained after creating a user token ([Users/Mutations/Create User Token](#operation/create-user-token)) <br> the user token is a persistent token (valid for 2 days) that should be securely stored in your application |

| Argument             | Required | Note                                                                                                                                                             |
| -------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name                 | Yes      | Arbitrary. Can help you categorize authentications according to service and End User                                                                             |
| serviceId            | Yes      | See [Importing Authentications](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/)                                             |
| serviceEnvironmentId | Yes      | See [Importing Authentications](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/)                                             |
| data                 | Yes      | Used to specify auth data such as api key and domain. See [Importing Auths](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/) |
| formData             | No       | Data that may be seen in the authentication dialog in the workflow builder, e.g. 'subdomain'                                                                     |
| scopes               | Yes      | Can be empty array as below example. For setting scopes of access (read/write access to components)                                                              |
| hidden               | no       | Controls if authentication should be hidden in UI. Default is False                                                                                              |

Here is an example mutation:

<div class="accordion-button">Create Authentication</div>
<div class="accordion-body">
<pre>
mutation { 
  createUserAuthentication (input:{
    name: "my-test-sqs-authentication-1",
    serviceId: "e73d8e91-XXXX-XXXX-XXXX-37df289242",
    serviceEnvironmentId: "a84eu2880-XXXX-XXXX-XXXX-7edd82904d",
    data: "{\"region\":\"us-east-1\",\"account_id\":\"1234\",\"access_key\":\"accesskey\",\"secret_key\":\"secretkey\"}",
    scopes: [],
    hidden: true
  }) {
    authenticationId
  }
}
</pre>
</div>
<div class="accordion-button">Create Authentication with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation { 
  createUserAuthentication (input:{
    name: "my-test-sqs-authentication-1",
    serviceId: "e73d8e91-XXXX-XXXX-XXXX-37df289242",
    serviceEnvironmentId: "a84eu2880-XXXX-XXXX-XXXX-7edd82904d",
    data: "{\"region\":\"us-east-1\",\"account_id\":\"1234\",\"access_key\":\"accesskey\",\"secret_key\":\"secretkey\"}",
    scopes: [],
    hidden: true,
    clientMutationId: "some-mutation-id" #OPTIONAL - only needed for legacy Relay & Apollo clients
  }) {
    authenticationId
    clientMutationId #OPTIONAL
  }
}
</pre>
</div>

| Returned Data    | Notes                                                                                                                                                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| authenticationId | This will be needed when using `createSolutionInstance` as detailed in [Importing Authentications](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/) |
| clientMutationId | Only relevant if using the Relay GraphQL client                                                                                                                                         |
