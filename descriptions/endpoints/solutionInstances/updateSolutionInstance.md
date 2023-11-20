The **primary use of this mutation is to 'enable' the solution instance**. This is a required step after creating and configuring the solution instance.

<div class="warning-note">
If you are auto enabling the instances for your end users after they complete the config wizard, your code should be configured to <strong>delay this enable mutation by least 2 seconds after <a href="#operation/create-solution-instance">createSolutionInstance</a></strong> is complete.
</div>

<div class="information-note">
This mutation can also be used to update existing auth and config values that were attached after the user ran the config wizard.

If you are dealing with new auth/config settings, the parent solution will be on a new version, and the instance must be upgraded by the end user re-running the Config Wizard or using [Solution Instances/Mutations/Upgrade Solution Instance](#operation/upgrade-solution-instance). This is explained in detail in [Updating/Upgrading Solution Instances](https://tray.io/documentation/embedded/building-integrations/updating-vs-upgrading-instances/)

</div>

| Required token | Notes                                                                                                                                                                                                                     |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **User**       | Obtained after using [Users/Mutations/Create User Token](#operation/create-user-token). <br>The User Token is a persistent token that should be securely stored in your application for future use (expires after 2 days) |

The mutation accepts the following arguments:

| Argument           | Required | Note                                                                                                                                                                                                                                                                      |
| ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| solutionInstanceId | Yes      | obtained with [Solution Instances/Queries/Get Solution Instances](#operation/get-solution-instances)                                                                                                                                                                      |
| instanceName       | No       |                                                                                                                                                                                                                                                                           |
| enabled            | No       | set to True to enable the Solution Instance after it is created                                                                                                                                                                                                           |
| authValues         | No       | accepts an array of objects. Each object has two keys: `externalId` and `authId`. Check an example mutation below to see how it will be passed                                                                                                                            |
| configValues       | No       | accepts an array of objects. Each object has two keys: `externalId` and `value`. Note that `value` is always a string. So it must be stringified if it is of any other type (object/array, boolean, number). Check an example mutation below to see how it will be passed |

Here is an example mutation:

<div class="accordion-button">Update Solution Instance - Enable</div>
<div class="accordion-body">
<pre>
mutation {
  updateSolutionInstance(input: {
      solutionInstanceId: "2d38b2ec-xxxx-xxx-xxxx-b4ec68084266",
      instanceName: "test-instance", 
      enabled: true
  }) {
    solutionInstance {
      id
      name
      enabled
      created
    }
  }
}
</pre>
</div>
<div class="accordion-button">Update Solution Instance - Update config and auth values</div>
<div class="accordion-body">
<pre>
mutation {
  updateSolutionInstance(input: {
      solutionInstanceId: "2d38b2ec-xxxx-xxx-xxxx-b4ec68084266",
      configValues: [
        {
          "externalId": "external_limit",
          "value": "10"
        },
        {
			    "externalId": "external_datamappings",
			    "value": "{\"location\":\"**********\",\"email\":\"**********\"}"
		    }
      ]
      authValues: [
        { 
          "externalId": "external_slack_authentication", 
          "authId": "aaa67786-XXXX-XXXX-XXXX-97dedd1519b3"
        }
	    ]
  }) {
    solutionInstance {
      id
      name
      enabled
      created
    }
  }
}
</pre>
</div>

| Returned Data        | Subfields                                                                             | Notes                                                                                                                                                                                                                                                            |
| -------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                   |                                                                                       |                                                                                                                                                                                                                                                                  |
| name                 |                                                                                       |                                                                                                                                                                                                                                                                  |
| created              |                                                                                       |                                                                                                                                                                                                                                                                  |
| enabled              |                                                                                       | defaults to False so must be set to True with this mutation                                                                                                                                                                                                      |
| solution             | id, title, description, tags, customFields, configSlots, authSlots                    | details of the parent solution                                                                                                                                                                                                                                   |
| workflows            | id, sourceWorkflowId, sourceWorkflowName, triggerUrl                                  | details of the source workflows, including webhook url (triggerUrl)                                                                                                                                                                                              |
| authValues           | authId, externalId                                                                    | details of the auths associated with the instance                                                                                                                                                                                                                |
| configValues         | value, externalId                                                                     | details of config values associated with the user                                                                                                                                                                                                                |
| solutionVersionFlags | hasNewerVersion, requiresUserInputToUpdateVersion, requiresSystemInputToUpdateVersion | boolean flags used to indicate if an underlying Solution has a newer version which might need upgrading as explained in [Updating / Upgrading Solution Instances](https://tray.io/documentation/embedded/building-integrations/updating-vs-upgrading-instances/) |
