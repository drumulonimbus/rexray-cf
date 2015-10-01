# rexray-cfn
This project exists to house proof-of-concept code for spinning up an AWS instance using CloudFormation, downloading and configuring the most recent `Docker` and `rexray` code, and making the instance available online. The purpose of the proof-of-concept is to allow an end user to 'kick the tires' a bit, without having to invest much time or energy into the setup.

## Usage
A basic familiarity with CloudFormation is expected - you'll want to [install the AWS CloudFormation CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) (hint: most likely `pip install awscli`), or just use the web interface.

To begin the instance with the CLI tools, clone this repository, enter the `rexray-cfn` directory, and use the following command:
> `aws cloudformation create-stack --template-body file://./rexray-template.json --stack-name rexraytesting --parameters ParameterKey=KeyName,ParameterValue=YOURKEY`

...where, of course, "YOURKEY" is your own key.

## Details
Really not much to this thing. It installs a basic AMI, downloads the latest Docker install script to /tmp and runs it, then downloads the latest REX-ray install script to /tmp and runs it, then reboots. Upon reboot, a user should be able to log into the instance as the user 'ec2-user' and immediately be able to run containers with the REX-ray volume driver.


