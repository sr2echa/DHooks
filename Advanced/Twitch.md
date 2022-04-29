###  Filter code for Twitch to Discord Webhooks notifications with fixed stream preview

```json
const body: any = {
  embeds: [{
    author: {
      name: `${Trigger.ChannelName} started streaming!`,
      value: Trigger.ChannelUrl,
      icon_url: `https://avatar.glue-bot.xyz/twitch/${Trigger.ChannelName}`
    },
    fields: [{
      name: 'Game',
      value: Trigger.Game || 'No Game',
      inline: true
    }, {
      name: 'Viewers',
      value: Trigger.CurrentViewers,
      inline: true
    }],
    image: {
      url: `${Trigger.StreamPreview}?${Math.floor(Math.random() * 1000000)}`
    },
    color: 0x9146ff,
    timestamp: Meta.triggerTime
  }]
};

MakerWebhooks.makeWebRequest.setBody(JSON.stringify(body));
```

### Twitch Live notification after x minutes

```json
{
  "embeds": [
    {
    "color": 6570405,
    "author":{
      "name":"{{ChannelName}}",
      "url":"{{ChannelUrl}}"
    },
    "description": "**is now streaming on Twitch**",
    "fields": [
      {
        "name": ":video_game: Game",
        "value": "{{Game}}",
        "inline": true
      },
      {
        "name": ":eye: Viewers",
        "value": "{{CurrentViewers}}",
        "inline": true
      }
    ],
    "image": {
      "url": "{{StreamPreview}}"
    },
    "footer": {
      "text": "http://twitch.tv",
      "icon_url": "https://d1qb2nb5cznatu.cloudfront.net/startups/i/114142-19c0993bf69c468f1350fd422bfad6b2-medium_jpg.jpg?buster=1410211530"
    }
  }
 ]
}
```


#### Twitch with @everyone and Intro text

```json
{
	"content": ":loudspeaker: Hey @everyone! {{ChannelName}} checkout my channel {{ChannelUrl}} and say hello :wink:",
	"embeds": [
    {
		"color": 6570405,
		"author": {
			"name": "{{ChannelName}}",
			"url": "{{ChannelUrl}}",
			"icon_url": "URL AVATAR"
		},
		"description": "**[{{ChannelName}}]({{ChannelUrl}})** ist jetzt live on Twitch!",
		"fields": [
      {
			"name": ":video_game: Game",
			"value": "{{Game}}",
			"inline": true
		}, {
			"name": ":eye: Viewers",
			"value": "{{CurrentViewers}}",
			"inline": true
		}
    ],
		"thumbnail": {
			"url": "URL AVATAR"
		},
		"image": {
			"url": " {{StreamPreview}}"
		},
		"footer": {
			"text": "twitch.tv | {{CreatedAt}}",
			"icon_url": "https://d1qb2nb5cznatu.cloudfront.net/startups/i/114142-19c0993bf69c468f1350fd422bfad6b2-medium_jpg.jpg?buster=1410211530"
		}
	}
 ]
}
```
