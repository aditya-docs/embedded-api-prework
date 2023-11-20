When interacting with GraphQL APIs, depending on the call, you will need to use

1. A <a href="https://tray.io/documentation/embedded/getting-started/embedded-id-and-master-token/" target="_blank">master token</a> obtained from the Tray Embedded UI (required for calls such as 'Get Users')
2. A user token obtained with <a href="#operation/create-user-token">Create user token</a> (required for calls such as 'Get Soluton Instances')

Some calls like <a href="#operation/get-authentications">Get Authentications</a> support both master and user token where using a master token gives all auths in your orgnaziation workspace while a user token only gives auths owned by that end user.