CodeIgniter Amazon SES
======================
A CodeIgniter library to interact with Amazon Web Services (AWS) Simple Email Service (SES). This library was designed with the standard CodeIgniter email class in mind. As a result, most methods look the same, ensuring a minimal learning curve.

NOTE: this code is still under heavy development and currently provides only the very basics of the AWS SES API (don't you like acronyms?), sending email.

Requirements
------------
1. PHP 5.1+
2. [CodeIgniter 2.0+](http://codeigniter.com)
3. libcurl with OpenSSL support
4. Phil Sturgeon's CodeIgniter [cURL library](http://github.com/philsturgeon/codeigniter-curl)
5. A bundle of public root certificates (e.g. http://curl.haxx.se/ca/cacert.pem)
6. An [Amazon Web Services account](http://aws.amazon.com)

Spark
-------------
This library is also released as a [Spark](http://getsparks.org). If you use this library in any other way, **don't copy the autoload.php to your config directory**.

Documentation
-------------

### Configuration
This library expects a configuration file to function correctly. A template for this file is provided with the library. 

### Verify email address
Before you can send your first message, Amazon SES requires that you verify your email address. This is to confirm that you own the email address, and to prevent others from using it.

Request to verify your email address as a sender.

    $this->amazon_ses->verify_address('from@example.com');

Check whether a email address is verified as a sender.

    $this->amazon_ses->address_is_verified('from@example.com');

### Recipients

Set the "To" address(es) for a message.

    $this->amazon_ses->to('to1@example.com');

Set the "CC" address(es) (carbon copy) for a message.

	$this->amazon_ses->cc('cc1@example.com, cc2@example.com');

Set the "BCC" address(es) (blind carbon copy) for a message.

	$this->amazon_ses->bcc(array('bcc1@example.com', 'bcc2@example.com', 'bcc3@example.com'));
	
These three methods expect valid e-mail addresses as a string, array or comma separated list.

###Message

Set the sender address. You can also set this in your config file. The second parameter - the vanity name of the sender - is optional. 

	$this->amazon_ses->from('do_reply@example.com', 'Email monkey');

Set the subject for a message.

	$this->amazon_ses->subject('Open me!');
	
Set the message to be sent.

	$this->amazon_ses->message('<strong>Use HTML</strong>');

Set the alternative message (plain-text) to be sent. When not specified, an alternative message is generated by using PHP's strip_tags() function.

	$this->amazon_ses->message_alt('No HTML?!');

Sends the message. Returns true on success. You can pass a boolean as a first parameter to preserve the recipients after the message has been successfully send. This makes it possible to send an additional message without re-specifying the recipients.

    $this->amazon_ses->send();

NOTE: All methods above are chainable, which means you can do the following

    $this->amazon_ses->to('email@example.com')->subject('Yo!')->message('Sup dawg')->send();

###Misc

Sends the message in debug mode. In debug mode, the send() methods returns the actual API response instead of a boolean. Call this method before calling the send method.
	
	$this->amazon_ses->debug(TRUE);

Contributing
------------
I am a firm believer of social coding, so <strike>if</strike> when you find a bug, please fork my code on [GitHub](http://github.com/joelcox/codeigniter-amazon-ses) and squash it. I will be happy to merge it back in to the code base (and add you to the "Thanks to" section). If you're not too comfortable using Git or messing with the inner workings of this library, please [open a new issue](http://github.com/joelcox/codeigniter-amazon-ses/issues). 

Thanks to
---------
* [Phil Sturgeon](http://philsturgeon.co.uk), for creating the CodeIgniter [cURL library](http://github.com/philsturgeon/codeigniter-curl) and thus taking care of all the cURL hassle.
* [Ben Hartard](http://github.com/bhartard), for adding the email verification method.
* [Stephen Frank](https://github.com/stephenfrank), for sorting out SSL conflict issues.
* [Fabio Borraccetti](http://www.entula.net/), for fixing a bug in the reply-to header.
* Spicer at [Cloudmanic Labs](http://www.cloudmanic.com), for some small fixes.