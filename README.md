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

[![Banner][banner]][github]

[![GitHub Pages][shield:github:pages]][example]
[![Discord][shield:discord]][puotek:discord]
[![Steam][shield:workshop]][puotek:workshop]

</div>

ts3connect makes working TeamSpeak 3 server links possible with people who have borked `ts3server://` protocol and also allows to use those links in Arma 3. (ts3server links should work with next profiling branch, but that wouldnt apply to `ts3connect://`)

This is done by installing a small registry file that registers a new protocol handler:
`ts3connect://` that launches TeamSpeak 3 similar to how `ts3server://` normally would.


If you encounter bugs, errors, or have suggestions, please open an [issue on github][github:issues].
## Installation

Download the [ts3connect.reg](ts3connect.reg) file from github or from link in redirect page and than run the file. After installing you should be able to use links like `ts3connect://...` same as you would `ts3server://...`.


## Raw Links Setup

To create a working link to a Teamspeak 3 server, create a link same as you would for `ts3server://...` eg.:

replace `ts3server://` with `ts3connect://` or
without `ts3server://` make a link like `https://puotek.github.io/ts3connect/#...`

to get this working in arma you have to whitelist in a `config.cpp` in `CfgCommands` the `https://puotek.github.io/*` domain, like this:

```cpp
class CfgCommands {
    allowedHTMLLoadURIs[] += {
        "https://puotek.github.io/*"
    };
};
```

than you can add the link to any button or otherwise as a `url="https://puotek.github.io/#..."` and it should work

## Link Creation

You can create TeamSpeak connection links in two ways:

### 1. Direct Protocol Link

Use the `ts3connect://` protocol exactly like `ts3server://`:

`ts3connect://voice.teamspeak.com?port=9987`

you can also add other elements to the link, such as `&channel=Briefing%20Room` or `&password=123` like this:

`ts3connect://voice.teamspeak.com?port=9987&channel=Briefing%20Room&password=123`

### 2. GitHub Pages Redirect Link

Useful when direct protocol links are blocked (e.g., inside Arma 3):

https://puotek.github.io/ts3connect/#voice.teamspeak.com?port=9987

Example redirect link:  
https://puotek.github.io/ts3connect/#voice.teamspeak.com?port=9987

## Arma 3 Integration

Arma 3 restricts which external URLs can be opened.  
To enable the redirect page, whitelist the domain in your config.cpp:
To be able to use the redirect page links, you need to whitelist them in CfgCommands inside a config.cpp

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

## Notes

- ts3connect.reg can be downloaded directly from the repository or via the redirect page.
- Direct `ts3connect://` links require the registry handler to be installed.
- The HTTP-based redirect method works even in environments that block custom protocols.
