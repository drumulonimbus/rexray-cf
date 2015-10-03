# rexray-cfn
This project exists to house proof-of-concept code for spinning up an AWS instance using CloudFormation, downloading and configuring the most recent `Docker` and `rexray` code, and making the instance available online. The purpose of the proof-of-concept is to allow an end user to 'kick the tires' a bit, without having to invest much time or energy into the setup.

## Usage
A basic familiarity with CloudFormation is expected - you'll want to [install the AWS CloudFormation CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) (hint: most likely `pip install awscli`), or just use the web interface.

To begin the instance with the CLI tools, clone this repository, enter the `rexray-cfn` directory, and use the following command:
> `aws cloudformation create-stack --template-body file://./rexray-template.json --stack-name rexraytesting --parameters ParameterKey=KeyName,ParameterValue=YOURKEY --capabilities=CAPABILITY_IAM`

...where, of course, "YOURKEY" is the name of your own keypair in AWS. Note that the `--capabilities=CAPABILITY_IAM` is needed!

## Details
This cnf template installs a basic AMI, downloads the latest Docker install script to /tmp and runs it, then downloads the latest REX-ray install script to /tmp and runs it, then reboots. Upon reboot, a user should be able to log into the instance as the user 'ec2-user' and immediately be able to run containers with the REX-ray volume driver.

The template also creates an IAM keypair for the rexray user to use - that's the 'CAPABILITY\_IAM' part. The script then populates the `/etc/rexray/config.yml` file with the AWS\_ACCESS\_KEY and AWS\_SECRET\_KEY values for rexray to use. Currently, *this doesn't work*. I'm not 100% sure why, but I'm actively working on fixing that...

(upon bringing up the stack, running `rexray volume help` gives the error "FATA[0000] Error: Driver Volume discovery failed: You are not authorized to perform this operation. (UnauthorizedOperation)". I suspect this is due to some sort of IAM policy oversight, but will have to dig harder into it to be sure.).

## TODO

- fix the auth bug
- tighten up the IAM policies
- clean up the documentation, adding better instructions


