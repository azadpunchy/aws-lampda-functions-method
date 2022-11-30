install dependency serverless

#npm i -g serverless

then goto aws credentials manager and get
your credentials and then run this command

#serverless config credentials --provider aws --key <key> --secret <secret-key>

fake
Access Key ID:
AKIA33EHFPLAAV4OVOMZ
Secret Access Key:
vug84w87RiIv73fKTGejDieOoRpWh7TqCnfvGhRe

i.e 
#serverless config credentials --provider aws --key AKIA33EHFPLAAV4OVOMZ --secret vug84w87RiIv73fKTGejDieOoRpWh7TqCnfvGhRe

then create awsnode lampda function
by running

#serverless create -t aws-nodejs

then you will get two files i.e
handler.js
serverless.yml

now modify .yml file according to your need
<em>
// here serveice name would be any name
// and any framework version
// and required node version 
// stage means your environment 
// you can create as many stages as you want
service: node-app-with-env
frameworkVersion: "3"

provider:
  name: aws
  runtime: nodejs12.x
  memorySize: 2048
  stage: dev
  timeout: 15
  region: us-east-1

functions:
  hello:
    handler: handler.hello
    events:
      - http: ANY /{proxy+}
      - http: ANY /
    environment:
      TEXT: I am from Backend
</em>

install serverless http in your project folder

#npm i serverless-http

then import serverless and wrap your express app in
handler file as 

module.exports.hello = serverless(app)

then update pacakge.json scripts as:

"deploy": "serverless deploy"

to deploy your code on aws lampda function run this cmnd:

#serverless deploy