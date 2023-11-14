---
title: 2. OpenAI integration
template: third-level-navigation.html
---

1.  Sign up at <https://platform.openai.com/> and login

2.  Create new API key

![screenshot1](assets/images/openai1.png)

3.  To use OpenAI in nodejs project install openai npm package
    <https://www.npmjs.com/package/openai>

4.  Code example for a request to openai:

```js
constructor(private configService: ConfigService) {
        const openAiConfiguration = new Configuration({ apiKey: configService.get('openAi').penAiApiKey });
        this.openAiApi = new OpenAIApi(openAiConfiguration);
    }
```

```js
async getGPTResponse(message: string): Promise<string> {
	try {
		const completion = await this.openAiApi.createChatCompletion({
			model: 'gpt-4-1106-preview',
			messages: [{ role: 'user', content: message }],
			temperature: 0.6
		});

		if (!completion?.data?.choices || !completion.data.choices[0]) {
			return `Sorry, can't analyse this page =(`;
		}

		this.logger.log('Analysis ended...');
		return completion.data.choices[0].message.content;
	} catch (error) {
		this.logger.log('Analysis ended with an ERROR...');
		this.logger.log(error);
		return `Sorry, can't analyse this page =(`;
	}
}
```
