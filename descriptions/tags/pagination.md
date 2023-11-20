<p>The Tray Embedded APIs use standard conventions for pagination, compatible with the <a
        href="https://facebook.github.io/relay/graphql/connections.htm" target="_blank" rel="noopener noreferrer">Relay
        Pagination Container</a>
    specification . Note that in our demo app all mutations make use of clientMutationId - if this parameter is
    specified in
    the input to the mutation, it will be returned unchanged in the payload. It is not necessary to use clientMutationId
    but
    it is used in Relay and Apollo.</p>

<p>Two very helpful articles on pagination with GraphQL can be found at
    <a href="https://www.howtographql.com/react-relay/8-pagination"
        target="_blank">https://www.howtographql.com/react-relay/8-pagination</a> and <a
        href="https://blog.apollographql.com/tutorial-pagination-d1c3b3ee2823"
        target="_blank">https://blog.apollographql.com/tutorial-pagination-d1c3b3ee2823</a>
</p>
<p>Using a query such as <a href="#operation/get-users">Get Users</a> it is possible to
    specify the cursor and page information that you need for pagination of results:</p>

<pre>
query {
    users(first: 2, after:"OGRiNDY2YzAtYTA0MS00OTM0LWFmMzUtMTU4YzcwNGM1OWRl") {
    edges {
        node {
            id
            name
            externalUserId
        }
            cursor
        }
        pageInfo {
            hasPreviousPage
            hasNextPage
            startCursor
            endCursor
        }
    }
}
</pre>

<p><strong>pageInfo</strong> is what GraphQL calls a <strong>connection</strong>. A connection stores additional data
    about the context
    of each item
    (edge/node), i.e. about the position of the item in the list as well as the items in the list that come directly
    before
    and after it.</p>

<p>Note that <strong>after</strong> in the above query specifies a particular <strong>cursor</strong> to begin
    the list from.</p>

<p>From the results you can see that the necessary page and cursor information is returned, as needed for pagination of
    results:</p>

<pre>
{
    "data": {
        "users": {
            "edges": [
            {
                "node": {
                    "id": "d9b7302f-xxx-xxx-xxx-b403242e3f26",
                    "name": "Danton Black",
                    "externalUserId": "96fxxxx85cd7"
                },
                "cursor": "ZDliNzMwMmYtxxxxxxxxxxxZmUtYjQwMzI0MmUzZjI2"
            },
            {
                "node": {
                    "id": "8db466c0-xxx-xxx-xxx-158c704c59de",
                    "name": "Miguel Rangel",
                    "externalUserId": "96b9327xxxxxxx-xxx86ce-b79e66872daa"
                },
                "cursor": "OGRiNDY2YxxxxxxxxLWFmMzUtMTU4YzcwNGM1OWRl"
            }
            ],
        "pageInfo": {
            "hasPreviousPage": true,
            "hasNextPage": true,
            "startCursor": "ZDliNzxxxxxxxxxxxxxxxxxxxUtYjQwMzI0MmUzZjI2",
            "endCursor": "OGRiNDY2YzAxxxxxxxxxxxxxMTU4YzcwNGM1OWRl"
        }
        }
    }
}
</pre>