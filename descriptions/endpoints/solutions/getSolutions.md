Retrive a list of solutions using various filters and pagination parameters.

Click 'Examples' to see different types of queries you can make when listing solutions

| Required Token | Notes                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Master**     | Obtained from the Tray app UI. Refer [this](https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/). |

The query accepts the following criteria:

| Criteria | Notes                                                                                                                                                                                                                                                                        |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tags     | If you have created tags in the <a href="https://tray.io/documentation/embedded/user-interface-guide/managing-solutions/making-a-solution/#the-solution-editor" target="_blank">Solution Editor</a>, this field can be used to filter Solutions in your external application |

Here are some example queries:

<div class="accordion-button">Get all solutions</div>
<div class="accordion-body">
<pre>
query {
  viewer {
    solutions {
      edges {
        node {
          id
          title
          description
          tags
          customFields {
            key
            value
          }
          configSlots {
            externalId
            title
            defaultValue
          }
          authSlots {
            externalId
            title
          }
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
}
</pre>
</div>
<div class="accordion-button">Get solutions by tag(s)</div>
<div class="accordion-body">
<pre>
query {
  viewer {
    solutions (criteria: { tags: [
		"marketing",
    "marketo"
	] }) {
      edges {
        node {
          id
          title
          description
          tags
          customFields {
            key
            value
          }
          configSlots {
            externalId
            title
            defaultValue
          }
          authSlots {
            externalId
            title
          }
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
}
</pre>
</div>
<div class="accordion-button">Get first 5 solutions</div>
<div class="accordion-body">
<pre>
query {
  viewer {
    solutions(first: 5) {
      edges {
        node {
          id
          title
          description
          tags
          customFields {
            key
            value
          }
          configSlots {
            externalId
            title
            defaultValue
          }
          authSlots {
            externalId
            title
          }
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
}
</pre>
</div>
<div class="accordion-button">Get first solution after cursor</div>
<div class="accordion-body">
<pre>
query {
  viewer {
    solutions(first: 1, after: "MTNiM2FiOWMtZTIyMi00NzM5LWE2OWItYzRkZDA3ZmJiZmE0") {
      edges {
        node {
          id
          title
          description
          tags
          customFields {
            key
            value
          }
          configSlots {
            externalId
            title
            defaultValue
          }
          authSlots {
            externalId
            title
          }
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
}
</pre>
</div>

| Returned Data | Subfields                             | Notes                                                                                                                                                                                                                                                                                     |
| ------------- | ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id            |                                       | The solution **id** which needs to be passed when using the [createSolutionInstance](#operation/create-solution-instance) mutation.                                                                                                                                                       |
| title         |                                       |                                                                                                                                                                                                                                                                                           |
| description   |                                       |                                                                                                                                                                                                                                                                                           |
| configSlots   | externalId <br>title <br>defaultValue | This can be used to expose the externalId of [Config Data](https://tray.io/documentation/embedded/core-topics/config-data/setting-config-data/) which is required when [Importing External Data](https://tray.io/documentation/embedded/core-topics/config-data/importing-external-data/) |
| authSlots     | externalId <br>title                  | Array of all the auths required by your solution                                                                                                                                                                                                                                          |
| tags          |                                       | If you have created tags in the Solution Editor, this field can be used to filter Solutions in your external application                                                                                                                                                                  |
| custom fields |                                       | You can set these on the [solution settings](https://tray.io/documentation/embedded/building-integrations/solution-building-basics/#tags-and-custom-fields) page.                                                                                                                         |

## Pagination

You can paginate the results of this query using the methods discussed in [Pagination](#tag/pagination)
