This mutation is used to create a Solution Instance for an End User who has chosen to activate a particular Solution for their own use.

The steps involved in activating a Solution Instance for an End User are:

1. Use this mutation to create a Solution Instance which returns a **id**
2. Generate a Config Wizard authorization code with [Users/Mutations/Create Config Wizard Authorization Code](#operation/create-config-wizard-auth-code)
3. Use the id from step 1 and the auth code from step 2 to activate the pop-up Configuration Wizard for the End User with the following url:

   ```
    https://embedded.tray.io/external/solutions/${partnerId}/configure/${solutionInstanceId}?code=${authorizationCode}

   ```

4. Your app will receive a **tray.configPopup.finish** PostMessage as explained in [Dealing with the Config Wizard](https://tray.io/documentation/embedded/building-integrations/the-config-wizard/#subscribing-to-events-from-the-tray-configuration-wizard-from-your-application)
5. Once the Solution Instance is configured for the End User, use [Solution Instances/Mutations/Update Solution Instance](#operation/update-solution-instance) to set the **status** to 'enabled'

| Required token | Notes                                                                                                                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **User**       | obtained after creating a user token ([Users/Mutations/Create User Token](#operation/create-user-token)) <br> the user token is a persistent token (valid for 2 days) that should be securely stored in your application |

The mutation accepts the following arguments:

| Argument     | Required | Note                                                                                                                                                           |
| ------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| solutionId   | Yes      | obtained with [Solutions/Queries/Get Solutions](#operation/get-solutions)                                                                                      |
| instanceName | Yes      |                                                                                                                                                                |
| authValues   | No       | can be used to import end user authentications. <br>see [Importing Auths](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/) |
| configValues | No       | can be used to import external data <br>see [Importing External Data](https://tray.io/documentation/embedded/core-topics/config-data/importing-external-data/) |

Here is an example mutation:

<div class="accordion-button">Create Solution Instance</div>
<div class="accordion-body">
<pre>
mutation {
   createSolutionInstance(input: {
       solutionId: "b3422397-XXXX-XXXX-XXXX-57e7e66771b3"
       instanceName: "PetersGraphQLInstance"
   }) {
     solutionInstance {
       id
       name
       enabled
       created
       authValues {
           authId
           externalId
       }
       configValues {
           value
           externalId
       }
       solution {
           id
           title
           description
           tags
           customFields
           configSlots
       }
       workflows {
           edges {
               node {
                   id
                   sourceWorkflowId
                   sourceWorkflowName
                   triggerUrl
               }
           }
       }
       solutionVersionFlags {
           hasNewerVersion
           requiresUserInputToUpdateVersion
           requiresSystemInputToUpdateVersion
       }
     }
   }
}
</pre>
</div>

It can return the following data:

| Returned Data        | Subfields                                                                             | Notes                                                                                                                                                                                                                                                            |
| -------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                   |                                                                                       |                                                                                                                                                                                                                                                                  |
| name                 |                                                                                       |                                                                                                                                                                                                                                                                  |
| created              |                                                                                       |                                                                                                                                                                                                                                                                  |
| enabled              |                                                                                       | defaults to False so must be set to True with **Mutations/Solution Instances/Update Solution Instance - Enable**                                                                                                                                                 |
| solution             | id, title, description, tags, customFields, configSlots                               | details of the parent solution                                                                                                                                                                                                                                   |
| workflows            | id, sourceWorkflowId, sourceWorkflowName, triggerUrl                                  | details of the source workflows, including webhook url (triggerUrl)                                                                                                                                                                                              |
| authValues           | authId, externalId                                                                    | details of the auths associated with the instance                                                                                                                                                                                                                |
| configValues         | value, externalId                                                                     | details of config values associated with the user                                                                                                                                                                                                                |
| solutionVersionFlags | hasNewerVersion, requiresUserInputToUpdateVersion, requiresSystemInputToUpdateVersion | boolean flags used to indicate if an underlying Solution has a newer version which might need upgrading as explained in [Updating / Upgrading Solution Instances](https://tray.io/documentation/embedded/building-integrations/updating-vs-upgrading-instances/) |
