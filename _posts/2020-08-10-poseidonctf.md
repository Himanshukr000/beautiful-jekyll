---
layout: post
published: true
title: PoseidonCTF
image: 'https://i.ibb.co/KLj3R6H/LOGO-PNG.png'
date: '2020-08-10'
---
Another CTF writeup from PoseidonCTF by @[sousselovectf](https://twitter.com/sousselovectf)

[https://pbs.twimg.com/media/Ee1RIxGXYAIDe5z?format=jpg&name=small](https://pbs.twimg.com/media/Ee1RIxGXYAIDe5z?format=jpg&name=small)

## DB64

We (ByteForc3) got the first blood on this challenge.

A memory forensics challenge. Starting off with usual Volatility `imageinfo` to get the profile.

![https://imgur.com/jgC4D04.png](https://imgur.com/jgC4D04.png)

Now as the description said about passwords , Firefox and Google products, So used the obvious plugins. (`chromehistory`, `firefoxhistory` and the well known `mimikatz` 😛)

![https://imgur.com/OR8SVf7.png](https://imgur.com/OR8SVf7.png)

Chrome gave a bunch of googledrive links 

[https://drive.google.com/file/d/1jYpvi9Va8be022G1SL4xUpEmZoknveTd/view](https://drive.google.com/file/d/1jYpvi9Va8be022G1SL4xUpEmZoknveTd/view) (A encrypted keepass db). Also Firefox plugin gave no output :( and mimikatz gave the password for the user `PoseidonCTF:dVi29Tv8` . (password will be of use in later part 😄)

![https://imgur.com/f3vWmkB.png](https://imgur.com/f3vWmkB.png)

But this password was not enough to unlock the keepass db. So on further play with volatility plugins. `consoles` gave a pretty much hint to proceed further.

![https://imgur.com/dDN2JIi.png](https://imgur.com/dDN2JIi.png)

`I cant paste the binary in recyle bin` . Now this part contained references to `pastebin` (the paste and the binary part). Also the password above looked same as pastebin's bin ID `dVi29Tv8`.

And it was correct 😃 [](https://pastebin.com/dVi29Tv8).

[https://pastebin.com/dVi29Tv8](https://pastebin.com/dVi29Tv8)

Now this had strings seperated by newline and contained a password for the keepass db. `keepass2john` and JTR with the wordlist above gave us the password.

![https://imgur.com/ISXJOXp.png](https://imgur.com/ISXJOXp.png)

![https://imgur.com/M7QZU3N.png](https://imgur.com/M7QZU3N.png)

Opening the db in keepassXC.

![https://imgur.com/YUITSoZ.png](https://imgur.com/YUITSoZ.png)

Now all the passwords were the pastebin ID's (also joining all the usernames makes `Pastebin/KEY` . Now one of the ID had flag and rest were just trolls.

`rtLPrXqL` this had the real flag image (b64 encoded).

![https://imgur.com/saKSV1G.png](https://imgur.com/saKSV1G.png)

`Poseidon{F1ref0x_P1ugIns_V0latI1Ity}`.

Thanks.