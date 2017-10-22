# serverless-demo
This demonstrates using the npm package "serverless"
to work with AWS Lambda and Google Cloud functions.

See the npm scripts in `package.json`.

To run in AWS:
* `npm run deploy` deploys the Lambda function to AWS
* `npm run invoke` invokes the Lambda function

To run locally:
* `npm start` starts a local server
* `npm run send` sends an HTTP requests to trigger the Lambda function

Google Cloud Platform (GCP) demo
- to create a GCP account
  * browse https://cloud.google.com/ and press the "TRY IT FREE" button
  * must enter a credit card number
  * will get $300 in free credit
  * won't automatically start billing when that is exhausted
- to setup a "billing account"
  * browse https://console.cloud.google.com/billing/create
- to create a project
  * browse https://console.cloud.google.com/home/dashboard
  * at top to the right of "Google Cloud Platform",
    click the menu that should say "Select a project"
  * a dialog will appear
  * press the "+" button in the upper-right
  * enter a project name
  * select a billing account
  * wait about 30 seconds for the project to be created
  * a project ID and project number will be displayed
    - note the project ID because it will be needed later
  * from the hamburger menu in the upper-left, select "APIs & services ... Dashboard"
  * click "ENABLE APIS AND SERVICES"
  * enter "Cloud Deployment" and click the tile for
    "Google Cloud Deployment Manager V2 API" and press "ENABLE"
  * enter "Cloud Functions" and click the tile for
    "Google Cloud Functions API" and press "ENABLE"
- to setup credentials
  * click "Credentials" in the left nav
  * click "Create credentials" and select "Service account key"
  * in the "Service account" dropdown select "New service account"
  * enter a name for the service
  * in the "Role" dropdown select "Project ... Owner"
  * in the "Key type" radio buttons select "JSON" (the default)
  * press the "Create" button
  * a JSON keyfile will be downloaded
    - contains private_key
  * move this file to ~/.gcloud/keyfile.json
- to create a project starting point
  * enter `serverless create --template google-nodejs --path gcp-demo`
    - creates the files for a "Hello World!" service
    - one generated file is serverless.yml
      * defines the service
      * includes any number of Google Cloud Functions,
        the events that trigger them,
        and resources they require
  * cd gcp-demo
  * npm install
    - without this you will get an error about a plugin not being found
  * edit serverless.yml
    - verify that the "credentials" property is
      set to the path to the JSON keyfile
    - change "project: my-project" to the project ID noted earlier
- to deploy the service
  * enter `serverless deploy`
- to invoke the service
  * enter `serverless invoke --function {function-name}` (-f)
    where "first" is a function name specified in serverless.yml
- to view logs from past runs of a function
  * enter `serverless log --function *function-name*` (-f)
- to remove the service
  * cd to the project directory
  * enter `serverless remove`
