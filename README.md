# Atlassian PHP OAuth Example
This is an example of connecting with Atlassian Jira's OAuth service, thus allowing you to use their REST api. This example is built with Silex and Twig and uses the Guzzle library for OAuth and subsequent REST requests.  All of these tools can be easily installed with  [Composer](http://getcomposer.org), which can be installed using:

	curl -s https://getcomposer.org/installer | php
	
Once you have composer, simply run the following inside of the source directory:

	composer.phar install

Next you will need to generate a private/public key and setup an Application Link inside of Jira.  You can generate the private/public key by running the following from your command line:

	openssl req -x509 -nodes -days 365 -newkey rsa:1024 -sha1 -subj '/C=US/ST=CA/L=Mountain View/CN=www.example.com' -keyout ~/myrsakey.pem -out ~/myrsacert.pem

Next you'll want to setup your application link inside of Jira, you can find instructions for that [here](https://confluence.atlassian.com/display/JIRA/Configuring+OAuth+Authentication+for+an+Application+Link).

*Note: you'll be dealing with the incoming authentication and the public key you generated above will need to be pasted into the OAuth window.*

Next up we need to make some changes to the config to point to your Jira instance, specifically these three lines:

	$oauth = new Lemon\OAuth('http://localhost:8181/');
	$oauth->setPrivateKey('/Users/stan/Sites/ssl/myrsakey.pem')
	      ->setConsumerKey('1234567890')

In the first line you'll want to change this to your Jira install.
In the second line you'll want to change this to the path of your private key
In the third line you'll want to put whatever you labeled as your *"consumer key"*.

Once you've completed these changes point your web browser to the 'web' folder and click to authenticate with Jira.