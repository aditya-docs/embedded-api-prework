The **importWorkflows** mutation can be used to import the workflow to your embedded account. This is handy when you want to import workflows to your 'production' account from 'staging'.

Note that it is possible to import multiple workflows (you would have to ensure that the workflows and workflowIds are listed in the exact same order in **exportedWorkflowsJson** and **targetWorkflowIds** - to make sure the correct workflow is imported to the correct target workflow)

However if you are working with multiple workflows, it is more likely that you will be importing a project.

| Required token | Notes                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following arguments:

| Argument              | Required | Note                                                                                                                                                                                                                                                                                |
| --------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| exportedWorkflowsJson | Yes      | Can be obtained either by [exporting workflow json from UI](https://tray.io/documentation/platform/version-control/importing-exporting-workflows/#import--export-workflows-manually) or using the **exportWorkflows** mutation (refer below) <br> **The JSON must be stringified.** |
| targetWorkflowIds     | Yes      | Array of workflow IDs <br> Workflow ID can be obtained from the url of target workflow page: `https://app.tray.io/workflow/{workflowId}`                                                                                                                                            |
| clientMutationId      | No       | Only relevant if using the [Relay GraphQL client](https://relay.dev/)                                                                                                                                                                                                               |

Here is an example mutation:

<div class="accordion-button">Import Project</div>
<div class="accordion-body">
<pre>
mutation {
	importWorkflows (input: {
        exportedWorkflowsJson: "{\"tray_export_version\":4,\"export_type\":\"workflow\",\"workflows\":[{\"id\":\"ea3c20f5-xxxx-xxxx-xxxx-0ce2b7bb9f29\",\"created\":\"2023-05-15T11:26:14.794686Z\",\"workspace_id\":\"6c595d5b-xxxx-xxxx-xxxx-959ceb938eae\",\"creator\":\"6a4e56d9-xxxx-xxxx-xxxx-2429f79b40ff\",\"version\":{\"id\":\"018cc858-xxxx-xxxx-xxxx-2c8cfe0a7886\",\"created\":\"2023-05-16T22:25:42.413825Z\"},\"title\":\"webhook slack\",\"enabled\":false,\"tags\":[],\"settings\":{\"config\":{},\"input_schema\":{},\"output_schema\":{}},\"steps_structure\":[{\"name\":\"trigger\",\"type\":\"normal\",\"content\":{}}],\"steps\":{\"trigger\":{\"title\":\"Webhook\",\"connector\":{\"name\":\"webhook\",\"version\":\"2.3\"},\"operation\":\"fire_and_forget\",\"output_schema\":{},\"error_handling\":{},\"properties\":{}}},\"dependencies\":[]}],\"projects\":[]}",
        targetWorkflowIds: ["e5dc0748-xxxx-xxxx-xxxx-dfcc33795f12"]
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
	importWorkflows (input: {
        exportedWorkflowsJson: "{\"tray_export_version\":4,\"export_type\":\"workflow\",\"workflows\":[{\"id\":\"ea3c20f5-xxxx-xxxx-xxxx-0ce2b7bb9f29\",\"created\":\"2023-05-15T11:26:14.794686Z\",\"workspace_id\":\"6c595d5b-xxxx-xxxx-xxxx-959ceb938eae\",\"creator\":\"6a4e56d9-xxxx-xxxx-xxxx-2429f79b40ff\",\"version\":{\"id\":\"018cc858-xxxx-xxxx-xxxx-2c8cfe0a7886\",\"created\":\"2023-05-16T22:25:42.413825Z\"},\"title\":\"webhook slack\",\"enabled\":false,\"tags\":[],\"settings\":{\"config\":{},\"input_schema\":{},\"output_schema\":{}},\"steps_structure\":[{\"name\":\"trigger\",\"type\":\"normal\",\"content\":{}}],\"steps\":{\"trigger\":{\"title\":\"Webhook\",\"connector\":{\"name\":\"webhook\",\"version\":\"2.3\"},\"operation\":\"fire_and_forget\",\"output_schema\":{},\"error_handling\":{},\"properties\":{}}},\"dependencies\":[]}],\"projects\":[]}",
        targetWorkflowIds: ["e5dc0748-xxxx-xxxx-xxxx-dfcc33795f12"],
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
