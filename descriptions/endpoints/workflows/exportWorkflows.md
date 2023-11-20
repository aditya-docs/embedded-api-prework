The **exportWorkflows** mutation can be used to export the workflows from your embedded account. This is handy when you want to import workflows to your 'production' account from 'staging'.

Note that it is possible to export multiple workflows

| Required token | Notes                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The mutation accepts the following arguments:

| Argument    | Required | Note                                                                                                                                      |
| ----------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| workflowIds | Yes      | Array of workflow IDs. <br> Workflow ID can be obtained from the url of target workflow page: `https://app.tray.io/workflow/{workflowId}` |

Here is an example mutation:

<div class="accordion-button">Export Workflows</div>
<div class="accordion-body">
<pre>
mutation {
  exportWorkflows (input: {
    workflowIds: ["ea3c20f5-xxxx-xxxx-xxxx-0ce2b7bb9f29", "a6af4264-xxxx-xxxx-xxxx-70a1e59d72b2"]
  }) {
    exportedWorkflowsJson
  }
}
</pre>
</div>

It can return the following data:

| Returned Data         | Notes                                      |
| --------------------- | ------------------------------------------ |
| exportedWorkflowsJson | Stringified JSON of the array of workflows |
