# gittag-dbots
GitHub based Git Tags for the Discord Bots Discord Server.

- [GitTags GitHub](https://github.com/7coil/GitTags)

## Tags are:
1. Downloaded from the `tags` folder when someone uses the FETCH prefix `git>`
2. The content of the tag is processed via the Handlebars engine.
3. The resulting output is parsed as JSON
    - If it is not valid JSON, the output of handlebars is sent.
    - If it is JSON, the JSON is sent as part of `TextChannel.createMessage()` as the payload
				- Please match the Discord specification for an `Embed Object`
				- https://discordapp.com/developers/docs/resources/channel#embed-object

## Tags are not:
- To be used for illegal stuff (Your GitHub and Discord account are going to be destroyed)

## Cool

### Cute of the Year
This tag uses the `moment` helper to select a date and output a timestamp for Discord to use.
```hbs
{
  "embed": {
    "title": "Katie's Cute of the Year is...",
    "description": "Ally!",
    "timestamp": "{{moment "next year" "YYYY-MM-DDTHH:mm:ssZ"}}",
    "footer": {
      "text": "Next COTY will be revealed"
    }
  }
}
```

### Selam Alakum
This tag uses the `get` helper to get the `id` property from the `author` object.  
This is wrapped with `<@  >` to turn this into a mention.

[See all available properties here](https://github.com/7coil/GitTags/blob/master/index.js#L103)

```hbs
<@{{get 'id' author}}> Aleyküm Selam kardeşim.
```

### Daily Random
This tag uses the `floor`, `split`, `multiply`, `itemAt` helpers, along with the `dayRandom` variable to select one of the COTDs.  

```hbs
{{ itemAt (split "Colour,Cute,Cat,COTD" ",") (floor (multiply dayRandom 4)) }}
```

This is similar to the following:
```js
return 'Colour,Cute,Cat,COTD'.split(',')[Math.floor(Math.random() * 4)]
```
