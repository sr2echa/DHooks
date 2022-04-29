### Spotify "New Song added"

```json
{
  "embeds": [{
    "color": 2021216,
    "title": "I've added a new song to my playlist!",
    "thumbnail": {
      "url": "{{AlbumCoverURL}}"
    },
    "fields":[
      {
        "name": "Track",
        "value": "[{{TrackName}}]({{TrackURL}})",
        "inline": true
      },
      {
        "name": "Artist",
        "value": "{{ArtistName}}",
        "inline": true
      },
      {
        "name": "Album",
        "value": "{{AlbumName}}",
        "inline": true
      }
    ],
    "footer": {
      "text": "Added {{SavedAt}}",
      "icon_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Spotify_logo_without_text.svg/200px-Spotify_logo_without_text.svg.png"
    }
  }]
}
```
