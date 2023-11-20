All endpoints are limited at a rate of **30 requests per second**

There is limited burst capacity to allow for momentary spikes in usage, as long as the overall rate is not broken in a set window.

If you exceed a certain rate of requests, you will receive a response similar to the following:

    {
        "data": null,
        "errors": [
            {
                "message": "Rate limit exceeded",
                "path": [
                    "users"
                ],
                "locations": [
                    {
                        "line": 2,
                        "column": 3
                    }
                ],
                "extensions": {
                    "name": "PreconditionError",
                    "time_thrown": "2023-06-29T14:55:54.518Z",
                    "code": "access_not_allowed"
                }
            }
        ]
    }

The `path` property will tell you the query or the mutation that exceeded the threshold.

### Tips and best practices to avoid being rate-limited

For the **Get Users** query, we recommend not using the `externalUserId`as a means of looking up or retrieving Tray users in a high-throughput production environment.

In this case, you should consider storing the Tray user `id` in your own application or data store, in order to facilitate creation of user tokens / deletion of users without making repeated calls to the **Get Users** query.

Similary, you should consider storing Tray Ids for other resources such as **Solution Instances** or **Authentications**.

Exactly how you will manage this will depend on your usecase and setup.

However these are the considerations that you need to be aware of.
