---
title: "Recolouring Images With a Colormatrix"
date: 2020-03-22T15:36:51+10:00
---

I fell in love with this wallpaper (_"[Sunny Stag](https://www.reddit.com/r/wallpapers/comments/8z0za6/sunny_stag_by_robert_farkas_6211x2662/)" by Robert Farkas_) the moment I saw it:

![Sunny Stag by Robert Farkas](https://preview.redd.it/xrh00l5uf3a11.png?width=960&crop=smart&auto=webp&s=cd91f9aaa7f1c0a0c3b4c8b4f3f2a6294a9490b0)

However I prefer dark themes and darker-coloured wallpapers, the original was a bit too bright for me. One Reddit user had made some inverted versions but I wanted a similar-coloured stag on a dark background (i.e. the colours should stay mostly the same). I use [NegativeScreen](https://zerowidthjoiner.net/negativescreen) all the time to darken my screens because it has "smart inversion" modes, which mostly preserve colours while still making things darker.

I had a look in its config file and noticed each inversion mode uses a "colour matrix", so I did a little Googling and came across [the MS docs](https://docs.microsoft.com/en-us/dotnet/api/system.drawing.imaging.imageattributes?view=netframework-4.8#examples) for using the ColorMatrix class to recolour an image. All I really had to do was change the matrix to the "smart inversion" matrix from NegativeScreen's config, and save the resulting image. Here's the code for it:

<script src="https://gist.github.com/mwanchap/aa590e8ed8d3988b9ec4d3aabe8d5bf8.js"></script>

And I think the resulting image looks pretty nice!

![Sunny Stag by Robert Farkas](https://i.imgur.com/qVD5akE.jpg)
[(Full-size version)](https://i.imgur.com/dseh2op.jpg)
