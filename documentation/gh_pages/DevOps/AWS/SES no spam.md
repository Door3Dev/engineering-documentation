---
title: Prevent project emails from getting into spam folder
template: third-level-navigation.html
---
### General idea is to send emails from a custom domain with AWS SES. To make it work you will need access to domain registrar.

1.  Go to AWS SES and create a new identity with identity type **Domain**

	![A screenshot of a computer Description automatically
	generated](/assets/images/ses1.png)

	<br/>

	![A screenshot of a computer Description automatically
	generated](/assets/images/ses2.png)

2.  SES will provide several CNAME key-value records for verification. They should be added to domain DNS records in **domain management console** at a domain registrar site.

	![A screenshot of a email Description automatically
	generated](/assets/images/ses3.png)

3.  After successful verification it is possible to send mails from any email box under @some-domain.com (<support@some-domain.com>, <admin@some-domain.com>, etc.)

	But only in AWS SES Sandbox mode. Sandbox mode has two main limitations:
	
	-   Both sender and receiver emails should be verified
	-   Less than 200 mails per day can be sent
	
	<br/>

4.  To get out of SES Sandbox (if you need) you can request a production
    access:

    - Go to Request **Production access page**
    -   Select mail type **Transactional**
    -   As a description add a message like the following:

		<em>We are an IT consulting company. You can verify that we have multiple accounts in AWS and we do not send spam. Currently we are working on a new project so we need SES for Transactional mails. It is still in the beta stage but we need to send emails to different users and we can't verify them all as a recepients. This is the main reason why we need to get out the sandbox.

		Some information based on previous applications experience:

		1.Currently we are not going to send more than 100 mails per day

		2.We keep our recipient lists in RDS

		3.We do not manage bounces, complaints, and unsubscribe requests at the current moment. But we are not sending any marketing information. Also	we are going to create a specific email with a contact person to handle	all complaints once we go to production</em>

	![A screenshot of a computer Description automatically
	generated](/assets/images/ses4.png)

	<br/>

	![A screenshot of a computer Description automatically
	generated](/assets/images/ses5.png)
