---
title: Send emails in NestJs with NodemailerTransport
template: third-level-navigation.html
---

1.  Add email credentials to .env file

```js
EMAIL_FROM = support@perfectsite.ai
SMTP_HOST = email-smtp.us-east-1.amazonaws.com
SMTP_PORT = 587
SMTP_USER = UserName
SMTP_PASSWORD = UserPassword
```

2.  Create email config class

```js
import { IsNumber, IsString } from "class-validator";

export interface EmailConfig {
	from: string;
	smtp_host: string;
	smtp_port: number;
	smtp_user: string;
	smtp_password: string;
}

export class EmailConfigValidator implements EmailConfig {
	@IsString()
    readonly from: string;

    @IsString()
    readonly smtp_host: string;

	@IsNumber()
    readonly smtp_port: number;

    @IsString()
    readonly smtp_user: string;

	@IsString()
    readonly smtp_password: string;
}

export const getEmailConfig = (): EmailConfig => ({
	from: process.env.EMAIL_FROM || 'support@perfectsite.ai',
	smtp_host: process.env.SMTP_HOST || '',
	smtp_port: +process.env.SMTP_PORT || 587,
	smtp_user: process.env.SMTP_USER || '',
	smtp_password: process.env.SMTP_PASSWORD || '',
});
```

3.  Create email service and configure NodemailerTransport with
    credentials from email config service

```js
import {Injectable} from \'@nestjs/common\';
import {createTransport} from \'nodemailer\';
import \* as Mail from \'nodemailer/lib/mailer\';
import {ConfigService} from \'@nestjs/config\';

@Injectable()
export default class EmailService {
	private nodemailerTransport: Mail;

	constructor(private readonly configService: ConfigService) {
		const {smtp_host, smtp_port, smtp_user, smtp_password} =
		configService.get(\'email\');

		this.nodemailerTransport = createTransport({
		host: smtp_host,
		port: smtp_port,
		secure: false, // use TLS
		auth: {
			user: smtp_user,
			pass: smtp_password,
		},

		tls: { ciphers: \'SSLv3\' }
		});
	}

	sendMail(options: Mail.Options): Promise\<any\> {
		return this.nodemailerTransport.sendMail(options);
	}
}
```