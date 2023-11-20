The **exportProject** mutation can be used to export the projects from your embedded account. This is handy when you want to import project to your 'production' account from 'staging'.

| Required token | Notes                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following arguments:

| Argument         | Required | Note                                                                                                                    |
| ---------------- | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| projectId        | Yes      | obtained from the url of the Project page: `https://app.tray.io/workspaces/{workspaceId}/projects/{projectId}`          |
| exportSolution   | Yes      | Boolean value. <br>If set to true, the solution associated with the workflow is exported as part of the JSON structure. |
| clientMutationId | No       | Only relevant if using the [Relay GraphQL client](https://relay.dev/)                                                   |

Here is an example mutation:

<div class="accordion-button">Export Project</div>
<div class="accordion-body">
<pre>
mutation {
  exportProject (input: {
    projectId: "944dxxx-xxx-xxx-xxx-xxx222eb99",
    exportSolution: true
  }) {
    exportedProjectJson
  }
}
</pre>
</div>

It can return the following data:

| Returned Data       | Notes                           |
| ------------------- | ------------------------------- |
| exportedProjectJson | Stringified JSON of the project |
