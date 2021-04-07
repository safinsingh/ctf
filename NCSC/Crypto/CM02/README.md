# Description

Download the file and find a way to get the flag.

# Steps

Inside the archive is a text file filled with emojis. This is probably a substitution cipher, but nobody likes doing manual frequency analysis. Since most online tools can't handle emojis, you can replace emojis with random letters like so:

```
👶👉🍇👀 💪👨 👯🔥👯🏃👀👅💪🏃💪👀😰?

💛👼 👀👉👯 👷🔥👀💪👽🍇👀👯 🐍🍇👀👷👅👯 💛👼 👯🔥👯🏃👀👅💪🏃💪👀😰, 🍇👨 💛👼 👀👉🍇👀 💛👼 👉👯🍇👀 🍇🐍😏 🔥💪😽👉👀, 👶👯
🍇👅👯 🍇👀 🙉👅👯👨👯🐍👀 💪😽🐍💛👅🍇🐍👀.

// becomes

abcd ef ghgidjeiedk?

lm dbg nhdeocdg zcdnjg lm ghgidjeiedk, cf lm dbcd lm bgcd czx heubd, ag
cjg cd yjgfgzd euzljczd.
```

An online substitution solver spits out the following:

```
what is electricity?

of the ultimate nature of electricity, as of that of heat and light, we
are at present ignorant.
```

From there, it's really just guess and check for the rest of the emojis. The flag is:

```
flag: frequently_substitute_frowny_face_for_smiley_face
```
