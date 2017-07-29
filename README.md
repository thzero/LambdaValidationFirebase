# Lambda Validation with Firebase

Using the Amazon template, this shows how to valdiate a Firebase token (https://firebase.google.com/docs/auth/admin/verify-id-tokens) with NodeJs and a Lambda function.  This can then be used in API Gateway to validate API usage.

## Getting Started

* Clone this repository.
* Run npm install from the project root.
* Zip the following:
 * node_modules
 * package.json
 * server.js

In AWS, create a new Lambda function.

* Set the following environment variables under the Advanced section of the Code tab.
 * firebaseUrl - https://[appname].firebaseio.com
 * firebasePrivateKey - from property 'private_key' of the private key json file
 * firebaseClientEmail - from property 'client_email' of the private key json file
 * firebaseProjectId - from property 'project_id' of the private key json file
 * See the Admin Setup from Firebase docs (https://firebase.google.com/docs/admin/setup) on how to setup admin access. 
* Upload the zip file of code on the Code tab; once uploaded to you can edit the code via the inline Lambda editor.
* Configure the test input.

```javascript
{
  "authorizationToken": "",
  "methodArn": "arn:...../*/GET/",
  "type": "TOKEN"
}
```

## AuthorizationToken

The authorization token can be fetched from via the following snippet:

```javascript
firebase.auth().currentUser.getToken(/* forceRefresh */ true).then(function(idToken) {
  // Send token to your backend via HTTPS
  // ...
}).catch(function(error) {
  // Handle error
});
```

See https://firebase.google.com/docs/auth/web/google-signin#redirect-mode for more info.

## License

MIT License

Copyright (c) 2017 thZero.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
