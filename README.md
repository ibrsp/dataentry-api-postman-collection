# dataentry-api-postman-collection
A set of re-usable [Postman](https://www.getpostman.com/) scripts for working with the Dataentry API

## Getting Started by cloning Repository
To get started with this collection and test that everything is working, follow these steps:

1. Clone the repositoy, using one of theese commands: `git clone https://github.com/ibrsp/dataentry-api-postman-collection.git` (for https) or  `git clone git@github.com:ibrsp/dataentry-api-postman-collection.git` (for SSH)
1. Open Postman
1. Click Import
1. Click Choose Files
1. Browse to the location where you cloned the repository to
1. Select the `Dataentry API.postman_collection.json` file and click `Open`
1. Click the `Environment Options` gear at the top right hand corner of Postman
1. Click `Manage Environments`
1. Click Import
1. Click Choose Files
1. Browse to the location where you cloned the repository to
1. Select the `Dataentry Empty Environment.postman_environment.json` file and click `Open`
1. Click the newly imported Environment
1. Edit the name of the Environment as required
1. Fill in the required information:

    * _dataetnry_url_
      * Endpoint of Dataentry website
        * `https://data.tbportals.niaid.nih.gov` for PRODUCTION
        * `http://tbportal-dataentry-dev.ibrsp.org` for Staging 
    * _authenticationToken_
      * The API Token of the client that you want to use to access the API. *See below to find out how to get the token*.
1. Click Update
1. Close the `Manage Environments` window
1. In the collections list on the left hand side, expand `Dataentry API` then `Projects and Builds`
1. In the Environments drop down list at the top right hand corner of Postman, select the Environment that you named earlier

***IMPORTANT***: *Some of requestsa require additionnal params, such as **patientId** or **conditionId**. The list of this paramters you can see clicking the `PARAMS` button (to the left of `SEND` button). Befare each requestyou **MUST** define all of theese parameters*

## Getting the authorization token via Postman

The instruction how to use `OAuth 2.0` authentication you can see at the [Postman docs](https://www.getpostman.com/docs/postman/sending_api_requests/authorization) (section **OAuth 2.0**)

### Parameters to get the token

| Field  | Value  | Description |
|---|---|---|
| Token Name  | any value (could be empty)  | The name of the token.  | 
| Grant Type  | Authorization Code  | A drop down menu where you can specify one of the following grant types: “Authorization Code”, “Implicit”, “Password Credentials”, and “Client Credentials”.  | 
| Callback URL  | {{dataentry_uri}}/  | The Application’s callback URL that’s registered with the server. If not provided, Postman uses a default empty URL and extracts the code or access token from it. | 
| Auth URL  | {{dataentry_uri}}/identity/connect/authorize  | The endpoint for authorization server, which retrieves the authorization code. | 
| Access Token URL  | {{dataentry_uri}}/identity/connect/token  | The endpoint for the resource server, which exchanges the authorization code for an access token.  | 
| Client ID | {{client_id}} | The client identifier given to the client during the Application registration process. |
| Client Secret | {{client_secret}} | The client secret given to the client during the Application registration process. |
| Scope | offline_access {{scopes}} | The scope of the access request, which might have multiple space-separated values. 'offline_access' is required for retrieving the `RefreshToken` |

After defining all the fields, click the **Request Token** button, follow the instructions/steps to authenticate with **User**, copy value of **Access Token** field and paste this value to _authenticationToken_ parameter in the environment you created earlier. Also you should save the **Refresh Token** to have ability to get a new **Access Token** after its expiration (default **Access Token** lifetime is 3600 seconds)

***IMPORTANT***: After getting the **Access Token** and **Refresh Token** you MUST select **No auth** in the Authorization tab of Postman. Otherwise you'll get an *invalid headers* error when sending requests.

### Geting a new Access Token token using Refresh Token

To get a new **Access Token** after its expiration you should prepatre **POST** request to the *Access Token URL* from previous part.

Set body type *x-www-form-urlencoded*.

And add the following keys

| Key  | Value | 
|---|---|
| client_id  | {{client_id}} |
| client_secret  | {{client_secret}} |
| grant_type  | refresh_token  |
| refresh_token  | {{Refresh Token you got earlier}}  |
| scope  | offline_access {{scopes}}  |

The example of this request you can see in the Postman Collection: **Security/Refresh Token** (NOTE: you should fill the bosy values). 
