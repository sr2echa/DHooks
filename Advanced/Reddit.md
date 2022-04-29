### More complex Reddit checks

**Info**
Reddit RSS Feeds need filters, you get it [here](https://gist.github.com/Birdie0/5830535877a94ab772efeb897e58e0e8).


**Subreddits**
* `http://www.reddit.com/.rss` - front page
* `https://www.reddit.com/r/cats.rss` - certain subreddit
* `https://www.reddit.com/r/cats+dogs.rss` - temporal multireddit
* `https://www.reddit.com/user/frubbliness/m/cats.rss` - personal multireddit
* `http://www.reddit.com/domain/imgur.com/.rss` - subs from certain domain


**Sorting**
All of them support sorting by

* `/hot` (default)
* `/new`
* `/rising`
* `/controversial`
* `/top`
* `/gilded` (gold comments)


**Examples:**
* `https://www.reddit.com/rising.rss` - rising posts in front page
* `https://www.reddit.com/r/cats/new.rss` - new posts in /r/cats
* `https://www.reddit.com/r/cats+dogs/top.rss` - top posts in /r/cats


**How do I search?**
To use search you have to add `/search` to subreddit link (don't combine it with `/hot`, `/new`, etc.)

`https://www.reddit.com/user/frubbliness/m/cats/search?q=subreddit%3Apartyparrot&restrict_sr=on&sort=relevance&t=all`

The best practice is to open search page in your browser, fill the query and add `.rss` instead of making it by yourself.

Search parameters:
* `q=` - don't leave it empty! search query (check https://www.reddit.com/wiki/search for more info, P.S %3A = :)
* `restrict_sr=on` - required parameter for multireddit and should be set to on. restrict posts by it.
* `include_over_18=` - include NSFW posts
  * `on`, yes, 1 - include
  * `off`, no, 0 or missing - don't include
* `sort=` - sort by
  * `relevance`
  * `top`
  * `comments`
* `t=` - posts from past
  * `hour`
  * `day`
  * `week`
  * `month`
  * `year`
  * `all` time

**References**
* https://www.reddit.com/wiki/rss
* https://www.reddit.com/r/pathogendavid/comments/tv8m9/pathogendavids_guide_to_rss_and_reddit/
* https://www.reddit.com/r/newreddits/comments/m8sni/introducing_rssreddits_subscribe_to_any_rss_feed/
* https://www.reddit.com/wiki/search


### Example with specific tags like Title, Author, Content, Posted at

```json
{
  "embeds": [
    {
      "title": "**New Post on r/DataHorder**",
      "color": 981524,
      "fields":
      [
        {
          "name": "**Title**",
          "value": "**[<<<{{Title}}>>>](<<<{{PostURL}}>>>)**",
          "inline": true
        },
        {
          "name": "**Author**", "value": "**<<<{{Author}}>>>**",
          "inline": true
        },
        {
          "name": "**Content**",
          "value": "**<<<{{Content}}>>>**",
          "inline": true
        },
        {
          "name": "**Posted At**",
          "value": "**<<<{{PostedAt}}>>>**",
          "inline": true
        }
      ],
      "footer":
      {
        "text": "Data Horder Subreddit™",
        "icon_url": "https://cdn.discordapp.com/icons/505347422847762434/c264dc59a86c64a7f7496efcb7ba3e68.jpg"
      }
    }
  ]
}
```

### More complex solution

```json
if (entryTitle.length > 250) { // Check for long title and move it to description if needed
  body = { // EDITABLE-BEGIN!!!
    embeds: [{
      author: {
        name: authorName.slice(0, 256),
        url: authorUrl
      },
      description: `**[${entryTitle}](${entryUrl}):**\n${postContent.slice(0, 1748)}`,
      image: {
        url: postUrl
      },
      footer: {
        text: `r/${subredditName}`,
        icon_url: "https://www.redditstatic.com/desktop2x/img/favicon/favicon-96x96.png"
      },
      color: 0xFF4500
    }]
  }
 }
 else { // Safe length title means normal body
  body = { // EDITABLE-BEGIN!!!
    embeds: [{
      author: {
        name: authorName.slice(0, 256),
        url: authorUrl
      },
      title: entryTitle,
      url: entryUrl,
      image: {
        url: postUrl
      },
      footer: {
        text: `r/${subredditName}`,
        icon_url: "https://www.redditstatic.com/desktop2x/img/favicon/favicon-96x96.png"
      },
      color: 0xFF4500
    }]
  } // EDITABLE-END!!!
 }
```
