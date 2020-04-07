# Using a FHIR Server In Conjuction with InterSystems API Manager.

### Introduction

------

This demo comes pre-configured with a FHIR server, pre-populated with synthetic patient data.  The new InterSystems API Manager (IAM) includes OpenAPI Swagger specs to quickly generate REST client code to work with many common FHIR resources.   

### How to Run the Demo

------

The demo can be run locally with the following steps:

1. git clone https://github.com/sleblanc0916/covid-19-challenge.git
2. cd into the covid-19-challenge directory where docker-compose.yml is located
3. Run "docker-compose up --build"

Please note that the build can take 15-20 minutes, with most of the time spent loading synthetic patient data.  Make sure that you have at least 20GB of disk space.

After perfomring these actions your demo should be up and running on your machine. This includes an instance of InterSystems IRIS running an underlying FHIR server, and an Instance of the Intersystems API manager.

### Running the demo on AWS

------

IRIS-FHIR-Server.yaml is a CloudFormation Template that would deploy this demo on AWS EC2 instance. You need to be logged in the AWS account and have at least one EC2 SSH Keypair avaliable. 

https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=InterSystems-FHIR-Server&templateURL=https://isc-tech-validation.s3.amazonaws.com/IRIS-FHIR-Server.yaml

Alternatevely go to CloudFormation, Create Stack, Upload Template and then select IRIS-FHIR-Server.yaml.

Choose the name for your demo and Existing EC2 SSH Keypair. If you don't have one - follow [this guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) to create one.

In 3-5 minutes you'll see the following in the Outputs tab:

| Key | Value | Description |
| --- | :---: | :--- |
| AStartingPoint	| https://www.youtube.com/watch?v=VQrTATu1CU4	| It takes up to 10 minutes for all the resource to became avaliable after COMPLETE status is displayed. While you wait - watch the video and read: https://gettingstartedhealth.intersystems.com/interoperability/exploring-fhir-apis/ |
| FHIRAPIDevPortal	| http://x.x.x.x:8003/default/documentation	| FHIR API Catalog	|
| IRISPortal |	http://x.x.x.x:9088/csp/sys/%25CSP.Portal.Home.zen	| IRIS Management Portal |

### What will you see

------

After running the above commands you will have multipe Docker containers running on your machine. The most important ones are:

- Intersystems IRIS for Health running on port 9088 
  - Management Portal: http://localhost:9088/csp/sys/UtilHome.csp
    - Username: _SYSTEM 
    - Password: sys
- InterSystems API Manager running on 8002, and 8003
  - API Manager Development Portal (FHIR Resource API Documentation): http://localhost:8003/default/documentation
  - API Manager Overview: http://localhost:8002



### Testing Your Demo

------



To take and make sure that your FHIR Server is up and running successfully you can test that you can successfully make requests to the exposed FHIR Endpoint. A tool like Postman can be very helpful here although it is not explicitly required. A simple curl request should work as well. I have provided an example request below (note the different port... the demo will run on 9088 by default)


![Screen Shot 2020-02-10 at 12.08.49 PM](./TestingDemo.png)



### Additional Resources

------

- https://gettingstartedhealth.intersystems.com/interoperability/exploring-fhir-apis/	
  - Exploring FHIR Resource APIs With InterSystems IRIS for Health
- http://clinfhir.com/
  - A UI for generating FHIR requests
- http://hl7.org/fhir/resourcelist.html
  - The official FHIR resource documentation

