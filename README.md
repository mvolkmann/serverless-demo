# serverless-demo
This demonstrates using the npm package "serverless"
to work with AWS Lambda and Google Cloud functions.

Amazon Web Services (AWS) demo
- to setup an AWS account
  * browse https://aws.amazon.com
  * press "Sign Up" button
- to setup "Identity and Access Management" (IAM)
  * from the "My Account" menu in the upper-right,
    select "AWS Management Console"
  * enter your password and press "Sign In"
  * from the "Services" menu,
    in the "Security, Identity, & Compliance" group,
    select "IAM"
  * in the left nav, select "Users"
  * press the "Add user" button
  * enter a user name
  * check both access types, programmatic and AWS Management Console
  * press the "Next: Permissions" button
  * press the big "Attach existing policies directly" button
  * check "AdministratorAccess"
  * press the "Next: Review" button
  * press the "Create User" button
  * save the "Access key ID" and "Secret access key" values
    so they can be used later
    - for example, can save in 1Password
  * press the "Close" button
- to configure serverless for AWS
  * enter `serverless config credentials --provider aws --key {access-key-id} --secret {secret-access-key}`
- to create a service that will be implemented in Node.js
  * enter `serverless create --template aws-nodejs --path {service-name}
  * enter `cd {service-name}`
  * enter `npm install`
  * edit handler.js to change the default implementation
  * edit serverless.yml
    - to change the version of Node that is used
    - to add more functions
    - to configure the triggers for the functions
- see the npm scripts in `package.json`
- to deploy the Lambda function
  * enter `serverless deploy -l`
  * consider creating an npm script in package.json
    so this can be done with `npm run deploy`
- to invoke the Lambda function
  * enter `serverless invoke -f hello -l`
    so this can be done with `npm run invoke`
  * consider creating an npm script in package.json
- to run the Lambda function locally
  * enter `serverless offline start`
  * consider creating an npm script in package.json
    so this can be done with `npm start`
  * enter `curl http://localhost:3000/hello` to trigger the Lambda function
  * consider creating an npm script in package.json
    so this can be done with `npm run send`

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
    - if this isn't your first project, click the name of your last project
      which will appear instead of "Select a project"
  * a dialog will appear
  * press the "+" button in the upper-right
  * enter a project name
  * select a billing account
  * wait about 30 seconds for the project to be created
  * a project ID and project number will be displayed
    - note the project ID because it will be needed later
  * from the hamburger menu in the upper-left,
    select "APIs & services ... Dashboard"
  * click "ENABLE APIS AND SERVICES"
  * enter "Cloud Deployment", click the tile for
    "Google Cloud Deployment Manager V2 API", and press "ENABLE"
  * enter "Cloud Functions", click the tile for
    "Google Cloud Functions API", and press "ENABLE"
- to setup credentials
  * click "Credentials" in the left nav
  * click "Create credentials" and select "Service account key"
  * in the "Service account" dropdown select "New service account"
  * enter a service account name
  * in the "Role" dropdown select "Project ... Owner"
  * in the "Key type" radio buttons select "JSON" (the default)
  * press the "Create" button
  * a JSON keyfile containing a private key will be downloaded
  * move this file to ~/.gcloud/keyfile.json
- to create a project starting point
  * enter `serverless create --template google-nodejs --path {project-name}`
    - the project name was entered earlier when the project was created
    - this creates the files for a "Hello World!" service
    - one generated file is serverless.yml
      * defines the service
      * can describe any number of Google Cloud Functions,
        the events that trigger them,
        and resources they require
  * cd {project-name}
  * enter `npm install`
    - without this you will get an error about a plugin not being found
      when the function is invoked
  * edit serverless.yml
    - verify that the "credentials" property is
      set to the path to the JSON keyfile
    - change "project: my-project" to the project ID noted earlier
- to deploy the service
  * enter `serverless deploy`
    from within the project directory
- to invoke the service
  * enter `serverless invoke --function {function-name}` (-f)
    from within the project directory
    - the default function name in serverless.yml is "first"
- to view logs from past runs of a function
  * enter `serverless log --function {function-name}` (-f)
    from within the project directory
- to remove the service
  * enter `serverless remove`
    from within the project directory
