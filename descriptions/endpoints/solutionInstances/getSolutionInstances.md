Return the Solution Instances associated with a particular user.

Pay particular attention to **solutionVersionFlags** as a piece of returned data, which indicates if the Instance needs upgrading due to new information being required from the End User. For more information, refer the <a href="https://tray.io/documentation/embedded/building-integrations/updating-vs-upgrading-instances/#decision-table-for-solutionversionflags" target="_blank">decision table</a>.

| Required token | Notes                                                                                                                                                                                                                                                                                                                             |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). <br> If using a Master token it is possible to filter Solution Instances by the owner of the Solution Instance, or by the ID of the Solution which it came from                                |
| **User**       | obtained after creating a user token ([Users/Mutations/Create User Token](#operation/create-user-token)) <br> the user token is a persistent token (valid for 2 days) that should be securely stored in your application <br> If a User token is used, the Solution Instances displayed will only be those owned by that End User |

The query accepts the following filter criteria:

| Criteria   | Notes                                                                                                                                                |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| solutionId | Can be used to filter based on the Solution which the Instance came from. If used with a User Token it will only return instances owned by that user |
| owner      | This is the **userId** of an End User. Can only be used with a Master Token, in order to filter Solution Instances of a particular user              |

Note that it is possible to filter by both **owner** and **solutionId** at the same time.

| Returned Data        | Subfields                                                                                   | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------------------- | ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| totalCount           |                                                                                             | Note this is a **top-level** field, so is specified before 'edge' as per example query below <br>The results returned by the totalCount will depend on the filter criteria specified: <br>If **solutionId** is specified the total count will refer to the solution instances **for that particular solution** <br>If **owner** (**userId**) is specified (when using a Master Token) the total count will refer to the solution instances **for that end user** <br>If **owner** and **solutionId** are both specified the total count will refer to the solution instances **for that user and for that solution** |
| id                   |                                                                                             | the solutionInstance **id**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| name                 |                                                                                             | the name (derived from the parent Solution)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| enabled              |                                                                                             | boolean to indicate whether the solutionInstance has been activated using [Update Solution Instance](#operation/update-solution-instance)                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| created              |                                                                                             | the date and time the solutionInstance was created                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| solutionVersionFlags | hasNewerVersion <br>requiresUserInputToUpdateVersion <br>requiresSystemInputToUpdateVersion | boolean flags used to indicate if an underlying Solution has a newer version which might need upgrading as explained in [Updating / Upgrading Solution Instances](https://tray.io/documentation/embedded/building-integrations/updating-vs-upgrading-instances/)                                                                                                                                                                                                                                                                                                                                                     |
| solution             | id <br>title <br>description <br>customFields <br>configSlots <br>authSlots                 | details of the parent Solution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| workflows            | id <br>triggerUrl <br>sourceWorkflowId <br>sourceWorkflowName                               | **triggerUrl** is the webhook url for the End User's version of that workflow (see [Retrieving Webhook URLs](https://tray.io/documentation/embedded/core-topics/retrieving-webhook-urls/))                                                                                                                                                                                                                                                                                                                                                                                                                           |
| configValues         | externalId <br>value                                                                        | any [config data](https://tray.io/documentation/embedded/core-topics/config-data/setting-config-data/) that has been set for the End User of the solutionInstance                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| authValues           | externalId <br>authId                                                                       | authentications associated with this solutionInstance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## Pagination

You can paginate the results of this query using the methods discussed in [Pagination](#tag/pagination)

Here are some example queries:

<div class="accordion-button">Get solution instance(s) by owner - Master Token</div>
<div class="accordion-body">
<pre>
query {
	viewer {
		solutionInstances(criteria: { owner: "13b3ab9c-XXXX-XXXX-XXXX-c4dd07fbbfa4" }) {
			edges {
				node {
					id
					name
					enabled
					owner
					created
					solutionVersionFlags {
						hasNewerVersion
						requiresUserInputToUpdateVersion
						requiresSystemInputToUpdateVersion
					}
					workflows {
						edges {
							node {
								triggerUrl
								id
								sourceWorkflowId
                sourceWorkflowName
							}
						}
					}
					authValues {
						externalId
						authId
					}
					configValues {
						externalId
						value
					}
				}
				cursor
			}
			pageInfo {
				startCursor
				endCursor
				hasNextPage
				hasPreviousPage
			}
		}
	}
}
</pre>
</div>
<div class="accordion-button">Get solution instance(s) by owner and solution ID - Master Token</div>
<div class="accordion-body">
<pre>
query {
	viewer {
		solutionInstances(criteria: { 
				solutionId: "b73d4e07xxx-xxx-xxx-xxx-xxxafad23d94",
				owner: "13b3ab9c-XXXX-XXXX-XXXX-c4dd07fbbfa4" 
			}) {
			edges {
				node {
					id
					name
					enabled
					owner
					created
					solutionVersionFlags {
						hasNewerVersion
						requiresUserInputToUpdateVersion
						requiresSystemInputToUpdateVersion
					}
					workflows {
						edges {
							node {
								triggerUrl
								id
								sourceWorkflowId
                				sourceWorkflowName
							}
						}
					}
					authValues {
						externalId
						authId
					}
					configValues {
						externalId
						value
					}
				}
				cursor
			}
			pageInfo {
				startCursor
				endCursor
				hasNextPage
				hasPreviousPage
			}
		}
	}
}
</pre>
</div>
