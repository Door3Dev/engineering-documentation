---
title: 1. LinkedIn login
template: third-level-navigation.html
---

1.Go to <https://www.linkedin.com/developers/app> and create a new app

![linkedin](/assets/images/linkedin1.png)

2.Populate Create app page. Also you need to create a new LinkedIn Page for your company

![linkedin](/assets/images/linkedin2.png)

3.Once app is created Verify it

![linkedin](/assets/images/linkedin3.png)

4.Once your app is verified you need to go to Products page and select ‘Sign In …’

![linkedin](/assets/images/linkedin4.png)

5.Check that after you selected product these scopes appeared on Auth tab:

![linkedin](/assets/images/linkedin5.png)

6.Specify redirect URLs:

![linkedin](/assets/images/linkedin6.png)

7.When you have Scopes and Redirection setup you can make queries to 
- https://www.linkedin.com/oauth/v2/accessToken - to get accessToken (urlGetAccessToken in the code below)
- https://api.linkedin.com/v2/userinfo - to exchange accessToken for user email (urlGetUserInfo in the code below)


```js
	try {
            const parameters = {
                grant_type: 'authorization_code',
                code: linkedInPayload.code,
                redirect_uri: urlRedirect,
                client_id: clientId,
                client_secret: clientSecret,
            };

            let response = await firstValueFrom(this.httpService.post(urlGetAccessToken, parameters, { headers: { 'content-type': 'application/x-www-form-urlencoded' } }));
            response = await firstValueFrom(this.httpService.get(urlGetUserInfo, { headers: { Authorization: `Bearer ${response.data.access_token}` } }));
            email = response.data.email;
        } catch (e) {
            this.logger.log(e.message);
            throw new HttpException("Can't exchange access code", HttpStatus.BAD_REQUEST);
        }
```

*This video can be usefu if you have problems with app creation <https://www.youtube.com/watch?v=dfof_ha0WGM>
But it is a little bit dated and once you get app scopes workflow can be different

