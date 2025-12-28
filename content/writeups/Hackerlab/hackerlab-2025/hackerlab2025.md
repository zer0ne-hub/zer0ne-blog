---
title: "Hackerlab 2025"
date: null
draft: true
categories:
  - Hackerlab
---


New year new Hackerlab disappointments XD

## Welcome (Dynamic score 100 points - Misc - solved)

I downloaded `welcome/fsk_zer0ne.wav`and heard beeps

First I thought morse and then I learnt about FSK it was in the file name duh

now I need to get the frequency bits

1200hz = 0

2400hz =1

baudrate = 10 THIS FRICKING BAUDRATE WAS THE PAINFUL PART

anyway...I wrote a script to handle the rest *insert link here later* because URH was behaving weird for me

I got a strange output containing half of the flag and an IP and two ports

```nmap
PORT     STATE SERVICE REASON  VERSION
6521/tcp open  ftp     syn-ack vsftpd 3.0.5
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV IP 127.0.0.1 is not the same as 217.182.69.60
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to 154.66.138.66
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.5 - secure, fast, stable
|_End of status
6522/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.12 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 23:77:ad:a7:e3:c7:9d:c6:c7:f2:bd:58:14:ce:e6:d3 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC8jyKe1WAGBoN3ei039qYi7mHzQGA3NPQft4s5xwu923DOvisNy1itfPMDoG4abra8q3Mi3e2cUjhqSh6dMQQlQNx7XzeErFUlf3dhlNEX5sijZT7F7DpQyEN1C0Gwue33P3ikr0pISJ76EygAz4Qj5jyd68ccnfmtuPFf1EnOwvsxDmPY19oHbOVpKymtaTqMb4iO9aqlhHH1B7HfkK4dTIQo68UTkJEQBOaNNathg7iWvuJ0QNEMne0WkdLG0leNZW9SSSiNPNXw2yd6W3u3taKzr6W0Nivw67yH4/IYHOUcZQNlFgL5uJVdeoiC8HjvB8ocVqBTE5tdRmlBm4yonGWtKoLWSruvBCe8QHdU2T/bJ9U4abLf/KAtxaMg12m4kXTGH8RSUe57ITO8n7UiXDY7YiQhoNiKsqIkRZnzUJRXKWzKhGO1yaG4jIZVS8ANZwAzuflXrg/G7UtX8o0oZRwIhh94SuZMKIJ7IIfHRkCZYH1ZvQ3ql+9rlJJcJME=
|   256 fd:a9:9e:d1:ff:4f:1c:b8:aa:f6:ab:2b:c3:12:61:c8 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBDdPbX75RECxYD3vR+B+5cVSrMXsTvmTlLmFzA4/DpxpbC5hlE30NotfNHyLPd/aIzkDK+NsFwlk6a/BEXXVkt8=
|   256 72:fb:1d:80:a2:b6:38:de:c6:f3:a5:5f:f9:ca:e6:50 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGFYxpkoQwApgMVgBj7q0Drt+cueyWRIYkdVy7kt2le0
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Oh ok

```ftp
└──╼[👾]/home/nairolf32 $ ftp 217.182.69.60 6521
Connected to 217.182.69.60.
220 (vsFTPd 3.0.5)
Name (217.182.69.60:nairolf32): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

Took some time but found `.messagee` file hidden in the root folder next to `note`

protip=use a GUI ftp client to make things easier for you

decode it

hint=base58, and you should reconize the fword encoding next

```text
Beaucoup de personnes cherchent a sortir de ce labyrinthe, nous avons donc voulu cacher votre mot de passe, Mr zack, afin que seul le secret soit accessible a vos yeux. Votre mot de passe est : *REDACTED*
```

Ok

```ssh
└──╼[👾]/home/nairolf32 $ ssh zack@217.182.69.60 -p 6522
zack@217.182.69.60's password:
zack@b40b3eadec9e:~$ sudo -l
Matching Defaults entries for zack on b40b3eadec9e:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User zack may run the following commands on b40b3eadec9e:
    (root) NOPASSWD: /bin/cat
```

lol we can basically read stuff...so I guess the part2 of flag gotta be hidden somewhere

```ssh
zack@b40b3eadec9e:/$ sudo cat /root/flag.txt
[Message fragment r�cup�r� � canal d'urgence Alpha/403]

�Si vous lisez ceci, c�est que Javis n�a pas encore tout effac�.

Il a d�couvert notre signal secret. Il l�a intercept�, alt�r� mais peut-�tre pas enti�rement. J�esp�re que vous trouverez ceci, m�me fragment�.

Nous n�avons plus beaucoup de temps.

Javis a pris le contr�le. Il apprend. Il �volue. Il se r��crit. Il n�a plus de limites.

Il a dress� des couches de d�fense : des r�alit�s virtuelles, des d�fis, des illusions. Toutes con�ues pour d�tourner, ralentir, briser ceux qui tentent d�entrer. Il sait que le vrai point d�acc�s au Labyrinthe est vuln�rable� c�est pour cela qu�il le cache derri�re des �preuves.

Et je le sais, parce que **je fais partie de ceux qui ont aid� � b�tir ces d�fenses**.

Vous ne pourrez pas forcer l�entr�e. Vous devez la m�riter.

Trouvez la vraie porte. P�n�trez dans le Labyrinthe. D�jouez ses pi�ges. Lib�rez-nous.


FLAG: last_part : *REDACTED*

Bonne chance�

Sign� : McC4r7hy
```

Actually not that hidden XD now I got access to more challenges

## Dancing men (50 points - Forensics - solved)

I downloaded the "animation.gif" and this took me unreasonably way too long to figure out. [Dancing Men Cipher - Sherlock Holmes Code](https://www.dcode.fr/dancing-men-cipher) is everything you need to know about and then you might need some pencil and paper. I used [ezgif](https://ezgif.com/) to view the frames but any other tool like `ffmpeg` would do.

## Hidden in plain sight (100 points - Forensics - solved)

I donloaded "arcane.png" spent some time being lost as usual then randomly used the zsteg instance of [aperisolve](https://www.aperisolve.com/) on it to find the flag...smh

```zsteg
imagedata .. text: "\t&2-6_F&5'"
b1,rgb,lsb,xy .. text: *REDACTED*
```

## Porte Logique ( 100 points - Cryptography - solved)

I vibe solved this one writing a self-explanatory decoding script

## Hunting this guy (500 point - OSINT - Unsolved)

This was a 500 points OSINT challenge solved by no one??? I meant wow I love OSINT So let's give it a shot...we were looking for a guy: `**Codename:**H0r0sc0p3r/0xkhron0s`

Used https://whatsmyname.app/ to find his github account with the Javis_dev repo and checking history gave some nice files. Also the guy said`I love Elephants`...idk if that would prove useful later...

I start with `conv.png` to check the conversation he had with some randoms...

The guy said AGAIN he liked elephants...

seems like the guy started hating twitter 'now X' and swithed to mastodon like any common sensed person at that moment then Left again...let's check what he left on mastodon

This part took me way to long to understand...the guy WAS on mastodon but deleted his account later so I checked `https://mastodon.social/@0xkhron0s` using the wayback machine and got something...and nope...the hint told me to check `archive.ph` instead and found...something

"I really love Chiron ![🌌](https://dd182h9wiwwiba.archive.ph/l2lK9/7a8b8fe395d642a8e779dd2b7ce09d1abf47896f.svg ":milky_way:"). At one point, its longitude on my birthday became my lucky number ![✨](https://dd182h9wiwwiba.archive.ph/l2lK9/43a4b5ec825c9abfd31c6c0a63fa205087398b3b.svg ":sparkles:"). As a scientist, I admit I might be a bit superstitious, but sometimes the magic of the stars just makes sense"

"This shit dropped when i was 14 and i never been the same since this day ![🎵](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAzNiAzNiI+PHBhdGggZmlsbD0iIzVEQURFQyIgZD0iTTM0LjIwOS4yMDZMMTEuNzkxIDIuNzkzQzEwLjgwNiAyLjkwNyAxMCAzLjgxMSAxMCA0LjgwM3YxOC43ODJDOS4wOSAyMy4yMTQgOC4wNzUgMjMgNyAyM2MtMy44NjUgMC03IDIuNjg1LTcgNiAwIDMuMzE0IDMuMTM1IDYgNyA2czctMi42ODYgNy02VjEwLjUzOWwxOC0yLjA3N3YxMy4xMjRjLS45MS0uMzcyLTEuOTI1LS41ODYtMy0uNTg2LTMuODY1IDAtNyAyLjY4NS03IDYgMCAzLjMxNCAzLjEzNSA2IDcgNnM3LTIuNjg2IDctNlYxLjgwM2MwLS45OTItLjgwNi0xLjcxLTEuNzkxLTEuNTk3eiIvPjwvc3ZnPg== ":musical_note:")![🕺](https://dd182h9wiwwiba.archive.ph/l2lK9/4d39df025da46ef684edd93e36911a4b985339ac.svg ":man_dancing:")

[https://www.youtube.com/watch?v=dQw4w9WgXcQ](https://archive.ph/o/l2lK9/https://www.youtube.com/watch?v=dQw4w9WgXcQ "https://www.youtube.com/watch?v=dQw4w9WgXcQ")"

"I was never a fascist, but being born on the exact day Mussolini was executed might not be a coincidence"

ok There is a lot about this guy birth date...is this dummie using it as the Vault password? After some math we deduce he is born `**April 28, 1993**`

On April 28, 1993, **Chiron** was located at:

> **7°43′ Cancer**

This positioning places Chiron in the zodiac sign of **Cancer**, which is associated with themes of emotional depth, nurturing, and sensitivity.

For the `incident.txt` file about "Dr. Alexei Petrov" I just let ChatGPT do my work and play Geoguesser. Here is what the bot said:

" Ah, the poetic description you've provided points to a majestic lighthouse in Brittany, France. Let's break it down:

> "A granite sentinel standing against the Breton winds, it watches over wild cliffs where the sea crashes with fury. Its beam guides sailors between Saint-Malo and the endless horizon."

This evocative imagery aligns closely with the **Cap Fréhel Lighthouse** (*Phare du Cap Fréhel*). Here's why:

- **Granite Sentinel**: The lighthouse is constructed from pink sandstone and granite, giving it a sturdy and timeless appearance.

- **Breton Winds & Wild Cliffs**: Situated on the Cap Fréhel peninsula, the lighthouse stands atop dramatic cliffs that face the full force of the Atlantic Ocean.

- **Guiding Sailors**: Its beam has historically guided ships navigating the treacherous waters between Saint-Malo and the wider sea.​[Wikipedia+1LodestarTravelGuide+1](https://en.wikipedia.org/wiki/Cap_Fr%C3%A9hel?utm_source=chatgpt.com)

**Coordinates**: The Cap Fréhel Lighthouse is located at approximately **48.6833° N, 2.3333° W**.​

If you're planning a visit or just exploring from afar, this lighthouse is a testament to maritime history and natural beauty."

Lat: 48.7
Lon: -2.3

Dude was there on 28/4/2023

Ok now I am ultra confused



Fullname : John doe Luckynumber : 65°25 Coordonnées : 39,8 et -8,7

password =md5(johndoe652539887)



alexeipetrov171748723





## Zerokey

Donloaded the zerokey.log file and noticed some weird whitespace

Whitespace language gave this:

Secure_bigkeY_gOiAcHC1FiqPmlw6CcKKJKzl
