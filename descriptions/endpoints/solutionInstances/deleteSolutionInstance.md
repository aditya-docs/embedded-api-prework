Used to delete a Solution Instance.

Please also see our page on [Deleting Solutions and Projects](https://tray.io/documentation/embedded/core-topics/deleting-solutions-and-projects/)

| Required token | Notes                                                                                                                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **User**       | obtained after creating a user token ([Users/Mutations/Create User Token](#operation/create-user-token)) <br> the user token is a persistent token (valid for 2 days) that should be securely stored in your application |

The mutation accepts the following as **inputs**:

| Input              | Required | Notes                                                                                                |
| ------------------ | -------- | ---------------------------------------------------------------------------------------------------- |
| solutionInstanceId | Yes      | obtained with [Solution Instances/Queries/Get Solution Instances](#operation/get-solution-instances) |
| clientMutationId   | No       | Only relevant if using the Relay GraphQL client                                                      |

Here are some example mutations:

<div class="accordion-button">Delete Solution Instance</div>
<div class="accordion-body">
<pre>
mutation {
  removeSolutionInstance(input: {solutionInstanceId: "2d38b2ec-xxxx-xxx-xxxx-b4ec68084266"}) {
   clientMutationId
 }
}
</pre>
</div>
<div class="accordion-button">Delete Solution Instance with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
  removeSolutionInstance(input: {solutionInstanceId: "2d38b2ec-xxxx-xxx-xxxx-b4ec68084266", clientMutationId: "some-mutation-id"}) {
   clientMutationId
 }
}
</pre>
</div>

It can return the following data:

| Returned Data    | Notes                                                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| clientMutationId | while this data is Only relevant if using the Relay GraphQL client, it is actually required here as currently this mutation does not return any other data |
