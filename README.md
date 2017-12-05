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
        * `http://tbportal-dataentry-dev.ibrsp.org` for DEVELPMENT 
    * _authenticationToken_
      * The API Token of the client that you want to use to access the API. *See below to find out how to get the token*.
1. Click Update
1. Close the `Manage Environments` window
1. In the collections list on the left hand side, expand `Dataentry API` then `Projects and Builds`
1. In the Environments drop down list at the top right hand corner of Postman, select the Environment that you named earlier

***IMPORTANT***: *Some of requestsa require additionnal params, such as **patientId** or **conditionId**. The list of this paramters you can see clicking the `PARAMS` button (to the left of `SEND` button). Befare each requestyou **MUST** define all of theese parameters*

## Getting the authorization token

The instruction how to use `OAuth 2.0` authentication you can see at the [Postman docs](https://www.getpostman.com/docs/postman/sending_api_requests/authorization) (section **OAuth 2.0**)

### Parameters to get the token

| Field  | Value  | Description |
|---|---|---|
| Token Name  | any value (could be empty)  | The name of the token.  | 
| Grant Type  | Client Credentials  | A drop down menu where you can specify one of the following grant types: “Authorization Code”, “Implicit”, “Password Credentials”, and “Client Credentials”.  | 
| Access Token URL  | {{dataentry_uri}}/identity/connect/token  | The endpoint for the resource server, which exchanges the authorization code for an access token.  | 
| Client ID | {{client_id}} | The client identifier given to the client during the Application registration process. |
| Client Secret | {{client_secret}} | The client secret given to the client during the Application registration process. |
| Scope | {{scopes}} | The scope of the access request, which might have multiple space-separated values. |

After defining all the fields, click the **Request Token** button, copy value of **Access Token** field and paste this value to _authenticationToken_ parameter in the environment you created earlier.
