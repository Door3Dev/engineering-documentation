---
title: 2. How to connect Figma with GitHub repository to synchronize Design Tokens
template: third-level-navigation.html
---

Sign up at <https://github.com/> and login.

Got to ``Settings > tokens`` page <https://github.com/settings/tokens>.

Click on ``Generate new token``.

![step1](/engineering-documentation/assets/images/figma/tokens/step1.png)

On a **New personal access token (classic)** page fill in ``Note`` input with the description of the token, select `Èxpiration` with `No Expiration` value and check `repo` under `Select scopes` section.

![step2](/engineering-documentation/assets/images/figma/tokens/step2.png)

Copy generated GitHub access token.

Go to Figma project and open **Tokens Studio for Figma** plugin

![step3](/engineering-documentation/assets/images/figma/tokens/step3.png)

Switch to ``Settings`` tab and click on ``Add new sync provider``

![step4](/engineering-documentation/assets/images/figma/tokens/step4.png)

Select ``GitHub`` option

![step5](/engineering-documentation/assets/images/figma/tokens/step5.png)

Enter ``Name`` of the sync provider connection. 

Paste ``Personal Access Token`` generated in GitHub.

Enter `Repository (owner/repo)` value `Door3Dev/cnhi-dls`. 

Select Git repo `Branch` where all changes for the Figma tokens are going to be pushed and pulled from - `figma-design-tokens`. 

Enter `File path` where figma tokens are located inside Git repository - `/tokens/figma/tokens.json`. 

And click `Save` button.

<img alt="step6" height="400" src="/engineering-documentation/assets/images/figma/tokens/step6.png"/>

Now you should see at the bottom of the **Tokens Studio for Figma** plugin window a new set of items - GitHub branch name (`figma-design-tokens`) and two icons - to pull changes from GitHub and to push changes from Figma to GitHub.

![step7](/engineering-documentation/assets/images/figma/tokens/step7.png)

Once you are done with the local changes to the Design tokens in Figma, you can click on ``Push`` icon highlighted with blue dot. 

New modal ``Push to GitHub`` will be opened, where you can enter ``Commit message`` and click ``Push changes``.

![step8](/engineering-documentation/assets/images/figma/tokens/step8.png)

To notify developers you have to ``Create Pull Request``. Click on the button in new window, and you will be redirected to the GitHub site.

![step9](/engineering-documentation/assets/images/figma/tokens/step9.png)

On an **Open Pull Request** page enter ``Title``, select ``Reviewers`` and click on ``Create pull request`` button.

![step10](/engineering-documentation/assets/images/figma/tokens/step10.png)

Congratulations! Integration are done!

