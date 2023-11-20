The **importProject** mutation can be used to import and overwrite an existing project in your embedded account. This is handy when you want to import projects to your 'production' account from 'staging'.

<div class="information-note">
If the project you are importing has a solution associated with it, the solution will be imported as draft

That means before you start creating instances for this solution, it has to be <a href="https://tray.io/documentation/embedded/building-integrations/solution-building-basics/#saving-and-publishing-a-solution" target="_blank">published</a> manually through UI.

</div>

| Required token | Notes                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following arguments:

| Argument            | Required | Note                                                                                                                                                                                                                                                                        |
| ------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| exportedProjectJson | Yes      | Can be obtained either by [exporting project json from UI](https://tray.io/documentation/platform/version-control/importing-exporting-workflows/#import--export-projects-manually) or using the exportProject mutation (refer below) <br> **The JSON must be stringified.** |
| targetProjectId     | Yes      | obtained from the url of target Project page: `https://app.tray.io/workspaces/{workspaceId}/projects/{projectId}`                                                                                                                                                           |
| clientMutationId    | No       | Only relevant if using the [Relay GraphQL client](https://relay.dev/)                                                                                                                                                                                                       |

Here is an example mutation:

<div class="accordion-button">Import Project</div>
<div class="accordion-body">
<pre>
mutation {
  importProject (input: {
    exportedProjectJson: "{}",
    targetProjectId: "944dxxx-xxx-xxx-xxx-xxx222eb99"
  }) {
    clientMutationId
  }
}
</pre>
</div>
<div class="accordion-button">Import Project with clientMutationId</div>
<div class="accordion-body">
<pre>
mutation {
  importProject (input: {
    exportedProjectJson: "{}",
    targetProjectId: "944dxxx-xxx-xxx-xxx-xxx222eb99",
    clientMutationId: "some-mutation-id"
  }) {
    clientMutationId
  }
}
</pre>
</div>

It can return the following data:

| Returned Data    | Notes                                                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| clientMutationId | while this data is only relevant if using the Relay GraphQL client, it is actually required here as currently this mutation does not return any other data |
