This mutation is used when a new version of a Solution has been published which contains new Config Data (which doesn't require user input) and you wish to upgrade an End User's Instance with the new Config Data, without asking them to use the Configuration Wizard again.

Please see our page on [Updating / Upgrading Solution Instances](https://tray.io/documentation/embedded/building-integrations/updating-vs-upgrading-instances/) for a full explanation of how to manage changes to your Workflows and Solutions.

| Required token | Notes                                                                                                                                                                                                                     |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **User**       | Obtained after using [Users/Mutations/Create User Token](#operation/create-user-token). <br>The User Token is a persistent token that should be securely stored in your application for future use (expires after 2 days) |

The mutation accepts the following arguments:

| Argument           | Required | Note                                                                                                                                                        |
| ------------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| solutionInstanceId | Yes      | obtained with [Solution Instances/Queries/Get Solution Instances](#operation/get-solution-instances)                                                        |
| instanceName       | No       |                                                                                                                                                             |
| authValues         | No       | Can be used to import End User authentications. See [Importing Auths](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/)  |
| configValues       | No       | Can be used to import external data. See [Importing External Data](https://tray.io/documentation/embedded/core-topics/config-data/importing-external-data/) |
| clientMutationId   | No       | Only relevant if using the Relay GraphQL client                                                                                                             |

Here is an example mutation:

<div class="accordion-button">Update Solution Instance - Enable</div>
<div class="accordion-body">
<pre>
mutation {
  upgradeSolutionInstance (input: {
    solutionInstanceId: "5f85b697-XXXX-XXXX-XXXX-5d7dabe22634", 
    configValues: [
      { 
        "externalId": "external_support-email", 
        "value": "support@example.com"  
      }
	  ],
    authValues: [
      { 
        "externalId": "external_slack_authentication", 
        "authId": "aaa67786-XXXX-XXXX-XXXX-97dedd1519b3"
      }
	  ]
  }) { 
    solutionInstance  {
      id
      configValues{
        externalId
        value
      }
      authValues{
        authId
        externalId
      }
      enabled
      owner
      created
    }
  }
}
</pre>
</div>
