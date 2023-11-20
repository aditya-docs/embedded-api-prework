This query can be used to retrieve the authentications for a particular user.

Please also see our guide to [Mapping and Editing Auths](https://tray.io/documentation/embedded/core-topics/authentications/mapping-editing-auths/)

| Required Token | Notes                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **User**       | obtained after creating a user token ([Users/Mutations/Create User Token](#operation/create-user-token)) <br> the user token is a persistent token (valid for 2 days) that should be securely stored in your application <br> If **Master token** is used will return all the authentications from the Embedded Organization including all the auths created by owner/admin/contributors and NOT including your end user auths. |

Here is an example query:

<div class="accordion-button">Get Authentications</div>
<div class="accordion-body">
<pre>
query {
  viewer {
    authentications {
      edges {
        node {
          id
          name
          customFields
          service {
            id,
            name,
            icon,
            title,
            version
          }
          serviceEnvironment {
              id
              title
          }
        }
      }
      pageInfo{
        hasNextPage
        hasPreviousPage
      }
    }
  }
}
</pre>
</div>

| Returned Data      | Subfields                      | Notes                                                                                                                          |
| ------------------ | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| id                 |                                | the authentication **id**                                                                                                      |
| name               |                                | the arbitrary name the end user has given to the authentication                                                                |
| service            | id, name, icon, title, version | details of the service the authentication is for                                                                               |
| serviceEnvironment | id, title                      | relevant when [Importing Authentications](https://tray.io/documentation/embedded/core-topics/authentications/importing-auths/) |
| pageInfo           | hasNextPage, hasPreviousPage   | can be used for [pagination](#tag/pagination)                                                                                  |
