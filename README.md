## Custom Windows 2019 AMI using Packer
I’m going to follow the steps from the hashicorp website and create a customised Windows 2019 server and setup winrm, and set the Administrator password.

Once the AMI image is ready, were going to build an instance bases on our new AMI image, then get Ansible to setup the server for us.

This is the [hashicorp link](https://learn.hashicorp.com/tutorials/packer/aws-windows-image?in=packer/integrations)

### Assumptions
I won’t be going into detail on these items:

  * I’m assuming your have already installed Packer!
  * I’m also assuming you know how to obtain and use the AWS access and Secret key from the AWS console.

Don’t worry if you don’t know how to do these steps. You can follow my previous video’s where I show you how to do this in details:

  * Build you’re first EC2 instance: https://youtu.be/XzWyudb4N04
  * Install Packer and create an AMI: https://youtu.be/dIAhHhQ_J-c


### The demo
Now I’ll show you how to do it. A quick note here, I make these video’s for you. I hope they help with your learning so feel free to share any of them with your colleagues, on LinkedIn and other social media platforms. Subscribe so you see new content I post and like the video.

If you have question, pop them in the comments and I’ll reply as soon as I can. Now, lets get down to it.

**Steps**

  * Create the required packer files
  * Create the AMI image
  * Build a windows server from the new AMI
  * Login to test credentials
  * Open the FW for winrm-HTTPS
  * Test with Ansible win_ping to confirm connectivity
  * Now run my test playbook


### Clone my repo
Feel free to clone my repo. Please give the repo a like and follow me if this code has helped you.

```
git clone https://github.com/dmccuk/packer_windows_build.git
cd packer_windows_build
```

no build the packer image:
```
packer validate 
packer build 
```

The build process takes around 5 minutes...

Once it completed, you will see something like this:

```
output...
```

### Creats an EC2 instance fom the AMI
I'm not doing anything amazing here. I'm just creating an EC2 image from the AMI we just created. Pop into the console and follow my steps in the demo.


### Ansible Steps
I've provided the Ansible code that is ready to go for this demo. We're using winrm over HTTP. This is obviously not entrypted. I'm just using it for the demo. You can change the script to do whatever you need, including changing the configuration to HTTPS or even SSH (I have demo's on this. Comment in the YouTube video if you need a hand).

Now lets test our Ansible connectivity with win_ping
```
win_ping command
```

Once that's successful, we can run my test playbooks against the windows server and configure it to out needs.

```
ansible-playbook command
```

## Remove all resources
Now that the demo has worked, I'm going to destroy my EC2 instance, the AMI image we created and the snapshot. This way I won;t be charged by AWS for any of these resource sticking around. I advise you to do the same as you don;t want to be spending any money you don;t need to.

Follow my demo and I'll show you how to delete everything.

