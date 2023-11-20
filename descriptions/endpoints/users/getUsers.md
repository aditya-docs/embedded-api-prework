Get all users including their name, id, and externalUserId.

| Required Token | Notes                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The query accepts a filter key `criteria` which can take in following fields:

| field          | Notes                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------ |
| id             | This is generated by Tray when you create a end user using [Mutations/Users/Create New User](#operation/create-user) |
| externalUserId | This will be provided by you upon the time of creation. It is the unique Id of the user in your own app and hence a mapping is created between your end user and their corresponding Tray user |
| name           | This will be provided by you upon the time of creation. It is the name of the end user in your own app |
| isTestUser     | This will be provided by you upon the time of creation. This is  a boolean flag that tells whether the user is billable or not |

Here are some sample queries:

<div class="accordion-button">Get all users</div>
<div class="accordion-body">
<pre>
query {
    users {
        edges {
            node {
                name
                id
                externalUserId
                isTestUser
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>
<div class="accordion-button">Get user by ID</div>
<div class="accordion-body">
<pre>
query {
    users (criteria: {userId: "13b3ab9c-XXXX-XXXX-XXXX-c4dd07fbbfa4"}){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>
<div class="accordion-button">Get user by externalID</div>
<div class="accordion-body">
<pre>
query {
    users ( criteria: { externalUserId: "my-external-user-id" } ){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>
<div class="accordion-button">Get user by name</div>
<div class="accordion-body">
<pre>
query {
    users ( criteria: { name: "Billy Bluehat" } ){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>
<div class="accordion-button">Get test users</div>
<div class="accordion-body">
<pre>
query {
    users ( criteria: { isTestUser: true } ){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>
<div class="accordion-button">Get test user by name</div>
<div class="accordion-body">
<pre>
query {
    users ( criteria: { isTestUser: true, name: "Billy Bluehat" } ){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>

The query also accepts following pagination parameters:

| parameter | Notes                                                   |
| --------- | ------------------------------------------------------- |
| first     | number to filter the first `n` users from response      |
| last      | number to filter the last `n` users from response       |
| before    | pagination parameter to go to previous page of response |
| after     | pagination parameter to go to next page of repsonse     |

Here are some sample queries:

<div class="accordion-button">Get users after cursor</div>
<div class="accordion-body">
<pre>
query {
    users (after: "MTNiM2FiOWMtZTIyMi00NzM5LWE2OWItYzRkZDA3ZmJiZmE0"){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>
<div class="accordion-button">Get first 2 users</div>
<div class="accordion-body">
<pre>
query {
    users (first: 2){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>
<div class="accordion-button">Get first 5 users after cursor</div>
<div class="accordion-body">
<pre>
query {
    users (first: 5, after: "MTNiM2FiOWMtZTIyMi00NzM5LWE2OWItYzRkZDA3ZmJiZmE0"){
        edges {
            node {
                name
                id
                externalUserId
            }
            cursor
        }
        pageInfo {
          hasNextPage
          endCursor
          hasPreviousPage
          startCursor
        }
    }
}
</pre>
</div>

It can return the following data:

| Returned Data  | subfields                                            | Notes                                                                                                     |
| -------------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| name           |                                                      |                                                                                                           |
| id             |                                                      | Tray ID of the user                                                                                       |
| externalUserId |                                                      | unique id for the user in your database                                                                   |
| cursor         |                                                      | used for [pagination](#tag/pagination) |
| pageinfo       | hasNextPage, endCursor, hasPreviousPage, startCursor | used for [pagination](#tag/pagination) |