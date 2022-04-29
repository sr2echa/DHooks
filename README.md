# DHooks
`Discord <-> Ifttt Webhooks`

Just a little collection of [Ifttt.com](https://ifttt.com/my_applets) applets which are linked to [Discord webhooks](https://support.discord.com/hc/en-us/articles/228383668-Webhooks-gebruiken).


## 🏛️ Creating your Organization

* Go to [https://platform.ifttt.com/](https://platform.ifttt.com/) and (Sign in)
* Click **(Get Started)**
* On the next page fill the required fields and click (Next)
* Change the page address to https://platform.ifttt.com/p/zzz/applets/private
* It will redirect you to "Personal Applets" section, which is not accessible without creating an organization.


## 🖊️ Creating an Applet with Filter Code

<img src="./Screenshots/Applet with filter code.png" width="600" align="center" />

* Click (New Applet)
* For if section select Trigger Service and Action, fill values below as you usually do in classic mode.
* For then section select Webhooks and Make a web request, fill the fields with next values:
  ```bash
  • URL - webhook url
  • Method - POST
  • Content Type - application/json
  • Body - {}
  N.B. Visibility should be set to Set by you
  ```
* Now the filter section is not grayed out anymore and can be enabled!


For example your request body looks like this:
```json
{
  "content": "<@&role-id> <<<{{AuthorName}}>>> just released new video!\nCheck it out! {{Url}}"
}
```

Write it like this:
```json
const body: any = {
  content: `<@&role-id> ${Trigger.AuthorName} just released new video!\nCheck it out! ${Trigger.Url}`
};
MakerWebhooks.makeWebRequest.setBody(JSON.stringify(body));
```

**Don't forget to fill the fields at the bottom:**
* Applet title
* Applet description
* Save your first applet!


## ✅ Activating your first Applet
* After you saved applet you have to activate it, click on Activate it on IFTTT
* Press (Save)!
* Done!
* (_optional_) Check "Activity" to monitor possible problems/errors.


## ❗Common mistakes people often run into

* `"color"` attribute is in HEX format, it has to be decimal format.
* `{{Name}}` must be in `<<<{{Name}}>>>`.
* Tweets typically need to remove inner's, they should look like `{"content":"<<<{{Url}}>>> <<<{{SourceUrl}}>>>"}`.
* `"icon_url"` must end in .png, .jpg, etc.
* Both, gif and timestamps aren't possible.
* `"timestamp":"{{EntryPublished}}",` will not work anymore.
* A blank message requires `{"content":""}`.
* Make sure you select the correct if ... then argument e.g. If RSS then Webhook, If Twitter then...


## 🦄 Useful websites to help you with regex & Discord Embeds
* [Beginner tutorial on how to use Discord Webhooks](https://markramsey.com/2019/12/03/bringing-twitter-tweets-into-discord-channels/)
* [RSS Bridge](https://github.com/RSS-Bridge/rss-bridge)
* [Working with Twitetr filters](http://followthehashtag.com/help/hidden-twitter-search-operators-extra-power-followthehashtag/)
* [Advance Twitter filters](https://developer.twitter.com/en/docs/tweets/rules-and-filtering/overview/standard-operators)
* [Discord + Ifttt step-by-step PDF Guide by Ben](https://mega.nz/#!uc5gHYZC!1dqXUlgMwtioJpcxYnhhS0rfYo2u2T8L1afpIOYtFuc)
* [Reddit.rss to Discord filter code + parser](https://gist.github.com/Birdie0/5830535877a94ab772efeb897e58e0e8)
* [Google-Forms-to-Discord](https://github.com/Iku/Google-Forms-to-Discord/blob/master/google%20script.js)
* [Tutorial how to use Discord Plex Notifications](https://blog.matiasnaess.no/2020/02/25/discord-plex-notifications/)


## 🌐 Online formatters/validators
* [Json Beautifier](https://jsonbeautifier.org/)
* [Json Editor online](https://jsoneditoronline.org/)
* [Json Formatter Online](https://jsonformatter-online.com/)
* [Json Validator & Formatter](https://jsonformatter.curiousconcept.com/)
* [Json Viewer](https://codebeautify.org/jsonviewer)
* [Json formatter](https://jsonformatter.org/)
* [Live Json Formatter](https://www.jsonformatter.io/)
* [Regular Expressions 101](https://regex101.com/)
* [Unicode Text Converter](http://qaz.wtf/u/convert.cgi)
* [Visualizer and validator for Discord embeds](https://leovoel.github.io/embed-visualizer/) (_ensure you enable "webhook mode"_)


## 📰 How a typical webhook must look like

**On the Ifttt website do the following**

* Go to `Webhooks` -> `Make a web request`
* Fill the fields with the values:
* URL - `Webhook url` _// The one you get from Discord Webhook menu_
* As Method choose: `POST`
* Content Type - `application/json`
* As Body, only one example: `{"content": "{{LinkToTweet}}"}` //This is the part you can freely change (see examples below)


## ❔What does `Action failure message: Rate limited by the remote server` mean?

This means that Discord rate limited request because IFTTT sends it too frequently. This mostly happens when IFTTT tries to send a lot of requests on same webhook in short amount of time. **Discord's webhook rate limit is 5 requests per 2 seconds**. Unable to make web request. Your server returned a 400. 400 means request is invalid. Can be caused by:
- wrong method verb (should be POST)
- wrong content-type (should be application/json)
- bad request body:
- empty, not json or invalid json also it should be filled correctly, [check this for more info](https://birdie0.github.io/discord-webhooks-guide/).
- **resulting json is broken** (usually caused by newlines in ingredients (json doesn't support them in values) and Unicode characters (rare but happens sometimes)), can be fixed by escaping variables with `<<<{{ingredient}}>>>` (_the website says to use <<double>>, ignore that_)
- **error from server saying that one of fields hit limit** (sadly, but ifttt doesn't show error that came from server). Try replace ingredients with data from applet logs and send it through Postman, Insomnia, other REST Client or using @glue's g.jp <JSON>, g.test <JSON> or g.webhook <JSON> commands (last one requires adding webhook through g.set webhook <url>).
* **Error 401** - webhook url isn't full. Usually happens on phone where is hard to copy url from web version of discord. I've made this simple web app https://get-discord-webhook-url.herokuapp.com/ that allows you to create webhook on phone.
* **Error 404** - url of webhook you're using has been removed. Means somebody removed it. Solution: create new webhook and replace old url.
* **Error 405** - Happens when you use other than POST methods.


## 🧰 Debug possible errors

**Where the IFTTT logs are?**

1. Open My Applets tab `https://ifttt.com/my_applets`
2. Click the applet you have problems with.
3. Click the gear icon in the corner.
4. Click `View activity log`.


