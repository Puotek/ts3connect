[github]: https://github.com/Puotek/ts3connect

[github:issues]: https://github.com/Puotek/ts3connect/issues

[example]: ts3connect://voice.teamspeak.com?port=9987

[ts3server:support]: https://support.teamspeak.com/hc/en-us/articles/360002712818-How-can-I-link-to-my-TeamSpeak-3-server-on-my-webpage

[puotek:discord]: https://discord.com/users/291967371646599169

[puotek:workshop]: https://steamcommunity.com/id/puotekpl/myworkshopfiles/?appid=107410&numperpage=30

[shield:github:pages]: https://img.shields.io/github/deployments/Puotek/ts3connect/github-pages?label=GitHub%20Pages&logo=github&labelColor=151b23

[shield:discord]: https://img.shields.io/badge/Puotek-%235865F2.svg?logo=discord&logoColor=white

[shield:workshop]: https://img.shields.io/badge/Puotek-1b2838?logo=steam&logoColor=white

[banner]: https://capsule-render.vercel.app/api?type=blur&animation=fadeIn&height=222&descAlignY=70&fontColor=FFFFFF&fontSize=70&color=0:161b22,30:a99cff,60:8bc5ff,100:90f0e4&text=ts3connect&desc=TS3%20server%20connect%20links%20for%20Arma%203

<!--suppress HtmlDeprecatedAttribute -->
<div align="center">

[![Banner][banner]][example]

[![Discord][shield:discord]][puotek:discord]
[![Steam][shield:workshop]][puotek:workshop]

</div>

ts3connect makes working TeamSpeak 3 server links possible with people who have borked `ts3server://` protocol and also allows to use those links in Arma 3. (ts3server links should work with next profiling branch, but that wouldnt apply to `ts3connect://`)

This is done by installing a small registry file that registers a new protocol handler:
`ts3connect://` that launches TeamSpeak 3 similar to how `ts3server://` normally would.

If you encounter bugs, errors, or have suggestions, please open an [issue on github][github:issues].

## Installation

Download the [ts3connect.reg](ts3connect.reg) file from github or from link in redirect page and than run the file. After installing you should be able to use links like `ts3connect://...` same as you would `ts3server://...`.

## Creating Direct Protocol Links

You can use the `ts3connect://` protocol exactly like `ts3server://`:

```ts3connect://voice.teamspeak.com?port=9987```

You can also add other elements to the link, such as:
- `&password=serverPassword`
- `&nickname=UserNickname` // Dont use this or you will have duplicate usernames for everyone
- `&cid=channelID` // Is prioritized above `channel=`
- `&channel=myChannelName` // Requires URL encoding (eg space is `%20`)
- `&channelpassword=defaultChannelPassword`
- `&token=TokenKey`
- `&addbookmark=MyBookMarkLabel` // I dont recommend this

Here is an example:
```
ts3connect://voice.teamspeak.com?port=9987&password=BESTUNIT&channel=Briefing%20Room&channelpassword=123
```

## Creating GitHub Pages Redirect Links

Redirect links are required for Arma 3, but also have the bonus of mentioning the requirement of installing `ts3connect.reg`.

To convert a direct protocol link to a github redirect one, you simply replace the `...` in the link below with your direct protocol link. `ts3connect://` is optional and can be removed here.
```
https://puotek.github.io/ts3connect/#...
```

As an example you will end up with:
```
https://puotek.github.io/ts3connect/#voice.teamspeak.com?port=9987
```
or
```
https://puotek.github.io/ts3connect/#ts3connect://voice.teamspeak.com?port=9987
```

## Arma 3 Setup

Arma 3 does not allow custom URI extensions such as `ts3connect://` so you will have to use redirect links mentioned above. Arma 3 also restricts which external URLs can be opened, so you will need to whitelist `https://puotek.github.io/*` inside a `CfgCommands` class in a `config.cpp` or `description.ext` like this:

```cpp
class CfgCommands {
    allowedHTMLLoadURIs[] += {
        "https://puotek.github.io/*"
    };
};
```

If you dont understand what that means, you can also just use the [ts3connect.pbo](ts3connect.pbo) in your mod.
After whitelisting, you can use the redirect links inside Arma in GUI elements or in scripts, like:

```cpp
url = "https://puotek.github.io/ts3connect/#voice.teamspeak.com?port=9987";
```

Keep in mind that Arma has an artificial limit of 255 characters for urls.

As a note `ts3server://` URI extension is allowed by Arma (at least in the profiling branch as of writing this) but that doesn't matter to us, since we use `ts3connect://`
