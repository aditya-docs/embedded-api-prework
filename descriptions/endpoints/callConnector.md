This mutation can be used to call a specific connector operation.

This powerful feature is used in combination with a User Token and Authentication Id, to pull data from a particular service connector operation and display it in your app.

As an example, for a particular End User of your Embedded application, you could use it to display all of the 'Warm' Salesforce Leads assigned to them, or display all the customers with overdue payments.

<div class="information-note">
Check out the <a href="https://docs-explorer.tray.io/" target="_blank">Operations explorer</a> app which will help you to figure out the input for any connector/any operation.

The tool also gives insight into the output schema for those operations, which will help you process the result.

</div>

Please see full instructions for using this endpoint at [https://tray.io/documentation/embedded/advanced-topics/call-connector/](https://tray.io/documentation/embedded/adva nced-topics/call-connector/)

| Required token         | Notes                                                                                                                                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **User** or **Master** | Obtained after using [Users/Mutations/Create User Token](#operation/create-user-token). <br>The User Token is a persistent token that should be securely stored in your application for future use (expires after 2 days) |

The mutation accepts the following arguments:

| Input            | Required | Note                                                                                                                                                                                                                                                                 |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| connector        | Yes      | The programatic connector name. Obtained from the workflow builder, see example below                                                                                                                                                                                |
| version          | Yes      | The version of the connector being used. Obtained from inspecting the Advanced settings of the input panel in the workflow builder, see example below                                                                                                                |
| operation        | Yes      | The programmatic name of the operation. This is usually the name of the operation visible in the workflow builder input panel, converted to snake case. Please reach out to support@tray.io if you get the error message `The connector operation ### was not found` |
| authId           | Yes      | see prerequisites below on obtaining an authId                                                                                                                                                                                                                       |
| input            | Yes      | The stringified JSON body representing the input parameters to the operation. You can explore the input schema for all connectors and their operations' in the <a href="https://docs-explorer.tray.io/" target="_blank">Operations explorer</a> app.                 |
| clientMutationId | No       | Only relevant if using the Relay GraphQL client                                                                                                                                                                                                                      |

Here is a sample mutation:

<div class="accordion-button">Call connector - Get all leads in Salesforce</div>
<div class="accordion-body">
<pre>
mutation {
    callConnector(input: {
        connector: "salesforce",
        version: "8.1",
        operation: "get_records",
        authId: "########-####-####-####-############",
        input: "{\\"limit\\":10,\\"conditions_type\\":\\"Match all conditions\\",\\"fields\\":[\\"Id\\",\\"Name\\"],\\"object\\":\\"Lead\\"}"
        }) 
    {
        output
    }
}
</pre>
</div>

It returns the following data:

| Returned Data    | Notes                                                                       |
| ---------------- | --------------------------------------------------------------------------- |
| output           | The stringified JSON body representing the data returned from the connector |
| clientMutationId | Only relevant if using the Relay GraphQL client                             |

### Named requests (Aliases)

GraphQL provides the capability to send multiple mutations at once. If you need to use the same mutation multiple times, you can use aliases (avoid any duplicate names).

Here is an example mutation with two mutations merged into one using aliases `listAllLeads` and `listWarmLeads`.

<div class="accordion-button">Multiple connector calls in one</div>
<div class="accordion-body">
<pre>
mutation callSalesforce {
    listAllLeads: callConnector(input: {
        connector: "salesforce",
        version: "4.0",
        operation: "find_records",
        authId: "########-####-####-####-############",
        input: "{\\"limit\\":10,\\"conditions_type\\":\\"Match all conditions\\",\\"fields\\":[\\"Id\\",\\"Name\\"],\\"object\\":\\"Lead\\"}"
        }) {
        output
    },
    listWarmLeads: callConnector(input: {
        connector: "salesforce",
        version: "4.0",
        operation: "find_records",
        authId: "########-####-####-####-############",
        input: "{\\"conditions_type\\":\\"Match all conditions\\",\\"fields\\":[\\"Id\\",\\"Name\\"],\\"conditions\\":[{\\"field\\":\\"Rating\\",\\"operator\\":\\"Equal to\\",\\"value\\":\\"Warm\\"}],\\"object\\":\\"Lead\\"}"
        }) {
        output
    }
}
</pre>
</div>
