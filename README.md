# serverless-demo
Demonstrates using the npm package "serverless" to work with AWS Lambda functions.

See the npm scripts in `package.json`.

To run in AWS:
* `npm run deploy` deploys the Lambda functionto AWS
* `npm run invoke` invokes the Lambda function

To run locally:
* `npm start` starts a local server
* `npm run send` sends an HTTP requests to trigger the Lambda function
