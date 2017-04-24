## SpamExperts API Library

This library makes common interaction with the SpamExpert API interface easier to use in bash scripts. Currently it only contains functions i've needed myself and might be expanded later.

## Prerequisites

The library only needs Curl to be installed for posting the API calls. Also an API user needs to be made that is allowed to post to the API.

## Settings

Copy the example config from se-lib.cfg-example to se-lib.cfg the first time.

The following settings can be set in the config file:

* filterhosts: the hosts that handle the mail filtering, default: 'filter[1-4].mydomain.tld'
* seapihost: the host that contains the web/API interface, default: filter1.mydomain.tld
* seapiuser: the API user, default: exampleuser
* seapipassword: the API users password, default: mypassword
* date: the date format wanted in the log file, default: $(date +%Y%m%d%H%M)
* deleteconfirmation: ask for confirmation before deleting in the queues, default: true
* logfile: the name of the log file, default: se-lib.log
* msgage: minimal age in seconds of messages in the queues, default: 300
* msgagemax: maximum age in seconds of messages in the queues, this is typically 5 days, default: 432000

## Usage

Source the se-lib file in your bash script.

	source se-lib

Then set the required variables for the functions below and call the function.

addlruser:

Adds a user as local recipient to a certain domain. This needs the following variables set:

	${domain}	The domain you're adding the user to
	${recipient}	The user that is allowed to receive mail

delmailuserincoming:

Deletes all mails from a certain mail address from the incoming queue, in either normal or frozen state. If it has a lot of mails in the queue, the API calls will use batches of 50 mails per call.

	${mailaddress}	The mail address that needs to be deleted

delmailuserincomingstr:

Deletes mails matching the supplied keyword in recipient and sender from the incoming queue, in either normal or frozen state. If it has a lot of mails in the queue, the API calls will use batches of 50 mails per call.

	${keyword}	The keyword that will be matched to recipients and senders

delmailuseroutgoing:

Deletes a mail address from the outgoing queue, in either normal or frozen state. If it has a lot of mails in the queue, the API calls will use batches of 50 mails per call.

	${mailaddress}	The mail address that needs to be deleted

delmailuseroutgoingstr:

Deletes mails matching the supplied keyword in recipient and sender from the outgoing queue, in either normal or frozen state. If it has a lot of mails in the queue, the API calls will use batches of 50 per call.

	${keyword}	The keyword that will be matched to recipients and senders

disablelrdomain:

Disabled the active local recipients list for a certain domain.

	${domain}	The domain where the local recipients list will be disabled for

enablelrdomain:

Enable the local recipients list for a certain domain.

	${domain}	The domain where the local recipients list will be disabled for

fetchrecipients:

List the active recipients for a certain domain in the past 7 days.

	${domain}	The domain that the recipients should be listed for

showoutgoingip:

Shows the current IPs used for sending outgoing mails
