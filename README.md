# DHooks
`Discord <-> Ifttt Webhooks`

Just a little collection of [Ifttt.com](https://ifttt.com/my_applets) applets which are linked to [Discord webhooks](https://support.discord.com/hc/en-us/articles/228383668-Webhooks-gebruiken).

## 🎗️ Table of Contents
* [DHook](#dhook)
  * [Table of Contents](#table-of-contents)
  * [Creating your Organization](#creating-your-organization)
  * [Creating an Applet with Filter Code](#creating-an-applet-with-filter-code)
  * [Activating your first Applet](#activating-your-first-applet)
  * [Common mistakes people often run into](#common-mistakes-people-often-run-into)
  * [Useful websites to help you with regex & Discord Embeds](#useful-websites-to-help-you-with-regex--discord-embeds)
  * [Online formatters/validators](#online-formattersvalidators)
  * [How a typical webhook must look like](#how-a-typical-webhook-must-look-like)
  * [What does `Action failure message: Rate limited by the remote server` mean?](#what-does-action-failure-message-rate-limited-by-the-remote-server-mean)
  * [Debug possible errors](#debug-possible-errors)
  * [My first webhook ever (Twitter)](#my-first-webhook-ever-twitter)
    * [Advance YouTube Upload finished announce feed](#advance-youtube-upload-finished-announce-feed)
    * [Android App Updates](#android-app-updates)
    * [Reddit Game Findings (_works basically with every Giveaway/Gift Subreddit_)](#reddit-game-findings-works-basically-with-every-giveawaygift-subreddit)
    * [Thank user for the follow on Twitter](#thank-user-for-the-follow-on-twitter)
    * [Twitch went live Feed](#twitch-went-live-feed)
    * [Twitch with viewer count & embed preview](#twitch-with-viewer-count--embed-preview)
    * [Twitter Basic Feed](#twitter-basic-feed)
    * [Twitter Advance Feed](#twitter-advance-feed)
    * [Twitter Advance Feed with Embed](#twitter-advance-feed-with-embed)
    * [Instagram (basic)](#instagram-basic)
    * [Instagram (very simple)](#instagram-very-simple)
    * [Nitter (Twitter) Tweet vi role-id](#nitter-twitter-tweet-vi-role-id)
    * [RSS Feed (Basic)](#rss-feed-basic)
    * [RSS (Advance)](#rss-advance)
  * [Old and unused stuff](#old-and-unused-stuff)
    * [Pizza Delivery (_I do not use it anymore since YAGPDB has a reminder function_)](#pizza-delivery-i-do-not-use-it-anymore-since-yagpdb-has-a-reminder-function)
    * [Tumblr](#tumblr)
    * [Facebook](#facebook)
    * [SoundClood](#soundclood)
    * [GitHub Webhook](#github-webhook)
    * [Yet another basic Twitter feed](#yet-another-basic-twitter-feed)
    * [NASA - Image of the Day](#nasa---image-of-the-day)
    * [Normal RSS-Feed](#normal-rss-feed)
    * [Google Calendar Event](#google-calendar-event)


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

  
## Verry Basic Twitter feed

Pretty basic, nothing special.

```json
{
    "content":"@<<<{{UserName}}>>> posted: <<<{{LinkToTweet}}>>> <<<{{TweetEmbedCode}}>>>"
}
```

**[`^        back to top        ^`](#readme)**


### Advance YouTube Upload finished announce feed

```json
{
    "content": "Hello @everyone peeps, **<<<{{AuthorName}}>>>** has uploaded a new video! <<<{{Url}}>>>",
    "embeds": [
      {
        "title": "<<<{{Title}}>>>",
        "description": "<<<{{Description}}>>>",
        "url": "<<<{{Url}}>>>",
        "color": 6570404,
        "fields": [
          {
            "name": "Timestamp",
            "value": "<<<{{CreatedAt}}>>>",
            "inline": true
          },
          {
            "name": "Added By",
            "value": "Magic",
            "inline": true
          }
        ],
        "author":
        {
          "name": "<<<{{AuthorName}}>>>",
          "url": "https://www.youtube.com/channel/",
          "icon_url": "https://yt3.ggpht.com/a/AATXAJyI_DBeZc7O5cJ-Ih5ovltedR1HBIvcVH9ERQ=s100-c-k-c0xffffffff-no-rj-mo"
        },
        "footer":
        {
          "text": "Notice: Please be patient if the bot is broken, or there is no Application Officer around attending to you.",
          "icon_url": "https://yt3.ggpht.com/a/AATXAJyI_DBeZc7O5cJ-Ih5ovltedR1HBIvcVH9ERQ=s100-c-k-c0xffffffff-no-rj-mo"
        }
      }
    ]
}
```

**[`^        back to top        ^`](#readme)**


### Android App Updates

```json
{
  "username":"App Update",
  "content":"<<<{{Name}}>>>(<<<{{Version}}>>>)\n <<<{{AppStoreUrl}}>>> \n Changelog: <<<{{ReleaseNotes}}>>>"
}
```
**[`^        back to top        ^`](#readme)**


### Reddit Game Findings (_works basically with every Giveaway/Gift Subreddit_)

```json
{
    "embeds": [
    {
     "title": "<<<{{Title}}>>>",
     "url": "<<<{{PostURL}}>>>",
     "description": "<<<{{Content}}>>>",
     "thumbnail":
          {
          "url": "<<<{{ImageURL}}>>>"
          },
          "footer": { "icon_url": "https://www.redditstatic.com/desktop2x/img/favicon/favicon-32x32.png",
          "text": "/u/<<<{{Author}}>>> | <<<{{PostedAt}}>>>"
        }
      }
    ]
}
```

**[`^        back to top        ^`](#readme)**

### Thank user for the follow on Twitter

```json
{ "content":"Thx For Following: @{{FullName}}\nFollow Count: {{FollowerCount}}" }
```


### Twitch went live Feed

```json
{
    "content": "{{ChannelName}} went live on Twitch",
    "embeds": [
    {
      "title": "{{ChannelUrl}}",
      "url": "{{ChannelUrl}}",
      "color": 6570404,
      "footer":
      {
      "text": "{{CreatedAt}}"
    },
      "image":
      {
      "url": "{{StreamPreview}}"
    },
      "author":
      {
      "name": "{{ChannelName}} is now streaming"
    },
      "fields": [
    {
      "name": "Playing",
      "value": "{{Game}}",
      "inline": true
    },
    {
      "name": "Started at (streamer timezone)",
      "value": "{{CreatedAt}}",
      "inline": true
      }
     ]
    }
  ]
}
```

**[`^        back to top        ^`](#readme)**


### Twitch with viewer count & embed preview

```json
{
 "username":"{{ChannelName}}",
 "avatar_url":"https://avatar.glue-bot.xyz/twitch/%7B%7BChannelName%7D%7D",
 "embeds": [
   {
     "author":
     { "name": "Candy",
     "url": "http://twitch.tv/twitch_candyx",
     "icon_url": "https://static-cdn.jtvnw.net/jtv_user_pictures/4aecbebc-b161-40ba-843a-86a497fe25be-profile_image-300x300.png"
     },
     "title":" {{ChannelName}}", "url":" {{ChannelUrl}}",
     "description":"Candy is now live!",
     "color":6570405,
     "thumbnail":
     {
       "url": "https://static-cdn.jtvnw.net/jtv_user_pictures/4aecbebc-b161-40ba-843a-86a497fe25be-profile_image-300x300.png"
     },
       "fields":[
         {
           "name":"Game", "value":" {{Game}}", "inline":true
         },
         {
           "name":"Viewers", "value":" {{CurrentViewers}}", "inline":true
           }
           ],
           "image":
           {
           "url":" {{StreamPreview}}"
     }
    }
  ]
}
 ```
**[`^        back to top        ^`](#readme)**


### Twitter Basic Feed

```json
{"content":" <<<{{EntryTitle}}>>> <<<{{EntryContent}}>>> "}
```


### Twitter Advance Feed

```json
{
  "embeds": [
    {
      "description": "**Elon Musk tweeted this at {{CreatedAt}}**\n\n> **content**\n\n\n\n",
      "color": 11927808,
      "fields": [
        {
          "name": "Link to Tweet",
          "value": "Click [here]({{LinkToTweet}}) to go to the original tweet."
        }
      ],
      "author":
      {
      "name": "{{UserName}} tweeted:",
      "url": "https://twitter.com/elonmusk/",
      "icon_url": ""
      }
    }
  ]
}
```


### Twitter Advance Feed with Embed

```json
{
  "embeds": [
    {
      "title": "LINK",
      "color": 1942002,
      "url": "{{LinkToTweet}}",
      "author":
       {
        "name": "Melon Husk (@elonmusk)",
        "url": "https://twitter.com/ElonMusk/",
        "icon_url": ""
        },
        "footer":
        {
          "text": "Elon Musk! at {{CreatedAt}}!",
          "icon_url": ""
        },
        "description": "Elon Musk tweeted this : {{Text}}"
        }
      ]
}
```

**[`^        back to top        ^`](#readme)**


### Instagram (basic)

```json
{
  "embeds": [
    {
      "title":"Title",
      "url":"{{Url}}",
      "author":
      {
        "name":"random",
        "url":"https://www.instagram.com/random/"
      },
      "description":"{{Caption}}",
      "image": {"url": "{{SourceUrl}}"
      }
    }
  ]
}
```


### Instagram (very simple)

```json
{
  "embeds": [
    {
      "title":"New Post From Random on Instagram!",
      "description":" <<<{{Caption}}>>>",
      "color":12592603
    }
  ]
}
```

**[`^        back to top        ^`](#readme)**


### Nitter (Twitter) Tweet vi role-id

```json
{
  "username": "<<<{{UserName}}>>>",
  "avatar_url": "",
  "content": "<@&role-id>",
  "embeds": [
    {
    "title": "New Tweet!",
    "url": "<<<{{LinkToTweet}}>>>",
    "color": 33972,
    "description": "<<<{{Text}}>>>"
    }
  ]
}
```

**[`^        back to top        ^`](#readme)**


### RSS Feed (Basic)

```json
{
  "embeds": [
    { "title": "{{Title}}", "url": "{{PostURL}}", "description": "{{Content}}" }
  ]
}
```


### RSS (Advance)

```json
{
  "content":"**Test**",
  "embeds": [
    {
      "title":"{{EntryTitle}}",
      "description":"{{EntryContent}}",
      "url":"https://discordapp.com",
      "color":14510884,
      "footer":{"icon_url":"https://cdn.discordapp.com/embed/avatars/0.png",
      "text":"{{FeedTitle}}"},
      "thumbnail":
      {
        "url":"https://cdn.discordapp.com/embed/avatars/0.png"},
        "author":
      {
        "name":"{{EntryAuthor}}",
        "url":"{{FeedUrl}}",
        "icon_url":"https://cdn.discordapp.com/embed/avatars/0.png"
      }
     }
   ]
}
```

**[`^        back to top        ^`](#readme)**


## Old and unused stuff

### Pizza Delivery (_I do not use it anymore since YAGPDB has a reminder function_)

```json
{
  "embeds": [
    {
    "author":
    {
      "name": "Pizza Delivery Girl",
      "url": "https://www.reddit.com/r/Pizza/",
      "icon_url": ""
    },
    "description": "Your pizza is ready!\n:timer:ETA: 10 minutes."
   }
  ]
}
```

**[`^        back to top        ^`](#readme)**


### Tumblr

```json
{
   "username":"Bot Name",
   "avatar_url":"The URL of a Profile Picture/Thumbnail For The Bot Goes Here",
   "embeds": [
      {
         "title":"{{Title}}",
         "url":"{{Url}}",
         "description":"{{Body}}",
         "footer":{
            "text":"Uploaded On: {{Time}}"
         }
      }
   ]
}
```

**[`^        back to top        ^`](#readme)**


### Facebook

I'm not active on Facebook (or not really), so I dropped it.

```json
{
  "username":"Bot Name",
  "avatar_url":"The URL of a Profile Picture/Thumbnail For The Bot Goes Here",
  "embeds": [
    {
      "title":"{{UpdatedAt}}",
      "url":"{{PageUrl}}",
      "author":
      {
        "name":"{{PageName}}",
        "url":"https://facebook.com/{{PageName}}"
      },
      "description":"{{Message}}"
      }
    ]
}
```

**[`^        back to top        ^`](#readme)**


### SoundClood

Sadly I'm not really active on SC anymore (_no time_).

```json
{
    "content": "New track posted to SoundCloud",
    "embeds": [
        {
            "title": "<<<{{Title}}>>>",
            "url": "<<<{{TrackUrl}}>>>",
            "color": 16742144,
            "footer": {
                "text": "<<<{{Tags}}>>> || <<<{{CreatedAt}}>>>"
            },
            "thumbnail": {
                "url": "<<<{{ImageUrl}}>>>"
            },
            "author": {
                "name": "<<<{{Username}}>>>",
                "url": "<<<{{UserProfileUrl}}>>>",
                "icon_url": "<<<{{ImageUrl}}>>>"
            },
            "fields": [
                {
                    "name": "Description",
                    "value": "<<<{{Description}}>>>"
                }
            ]
        }
    ]
}
```

**[`^        back to top        ^`](#readme)**


### GitHub Webhook

I replaced it with Yappy Bot. `timestamp` line might invalidate json.

```json
{
  "embeds": [
    {
      "title": "[<<<{{RepositoryName}}>>>] <<<{{PullRequestTitle}}>>>",
      "description": "<<<{{PullRequestBody}}>>>",
      "url": "<<<{{PullRequestURL}}>>>",
      "color": 21953,
      "timestamp": "<<<{{CreatedAt}}>>>",
      "author": {
        "name": "<<<{{AuthorUsername}}>>>",
        "url": "https://github.com/<<<{{AuthorUsername}}>>>",
        "icon_url": "<<<{{AuthorAvatarImageURL}}>>>"
      }
    }
  ]
}
```

**[`^        back to top        ^`](#readme)**


### Yet another basic Twitter feed

```json
{
  "username": "@MelonHusk tweeted",
  "content": "@USerName tweeted this {{CreatedAt}} : {{LinkToTweet}} "
}
```

**[`^        back to top        ^`](#readme)**


### NASA - Image of the Day

```json
{
  "content": "NASA posted something new!",
  "embeds": [
    {
      "title": "<<<{{ImageTitle}}>>>",
    "description": "<<<{{Description}}>>>",
    "color":15193,
    "image":
    {
      "url": "<<<{{ImageSourceURL}}>>>"},
      "author":
      {
      "name":"Image of the Day by NASA"},
      "footer":
      {
        "text": "<<<{{PublishedDate}}>>>"
    }
    }
  ]
}
```

**[`^        back to top        ^`](#readme)**


### Normal RSS-Feed

```json
{
  "embeds": [
    {
      "title": "? New Post ? ",
      "description": "<<<{{Caption}}>>>",
      "image": {
        "url": "<<<{{SourceUrl}}>>>"
      },
      "footer": {
        "text": "<<<{{CreatedAt}}>>>"
      },
      "url": "<<<{{Url}}>>>"
    }
  ]
}
```

**[`^        back to top        ^`](#readme)**


### Google Calendar Event

```json
{
  "content": "<@user-id> <<<{{Title}}>>> is starting in around 30 minutes! ",
  "embeds": [{
    "title": "{{Title}}",
    "description": "<<<{{Description}}>>>",
    "url": "<<<{{EventUrl}}>>>",
    "color": 526591,
    "author": {
      "name": "SSI Calendar",
      "url": "",
      "icon_url": "https://calendar.google.com/googlecalendar/images/favicon_v2014_31.ico"
    },
    "fields": [
      {
        "name": "Starts",
        "value": "<<<{{Starts}}>>>",
        "inline": true
      },
      {
        "name": "Ends",
        "value": "<<<{{Ends}}>>>",
        "inline": true
      },
      {
        "name": "Location",
        "value": "<<<{{Where}}>>>"
      }
    ]
  }]
}
```

**[`^        back to top        ^`](#readme)**


