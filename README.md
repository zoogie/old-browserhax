# old-browserhax

## Thanks 
- MrNbaYoh for his [nice](https://mrnbayoh.github.io/blog/exploiting-the-3ds-browsers-p1/) [blogs](https://mrnbayoh.github.io/blog/exploiting-the-3ds-browsers-p2/).
- Yellows8 for the hbmenu loader code: https://github.com/yellows8/3ds_browserhax_common

## Intro

This is a new homebrew menu loading userland exploit for the old3ds browser, Spider. 

## What's needed

An old3ds (or old2ds) on firmwares:<br>
```
11.9.0-42 -> 11.13.0-45 for USA, JAPAN
11.10.0-43 -> 11.13.0-45 for EUROPE
11.9.0-36 -> 11.13.0-39 for KOREA
```
Note: The last number on the firmware version matters. If you updated from a cartridge to your current firmware, you will need to update to latest firmware as your browser would have been erased by the cart update.

## Directions 

1) In the release folder, find your region (USA, EUROPE, JAPAN, KOREA) and take all files *inside* that folder and put them on the root of your sd card. Do not copy the entire region folder over, just its contents.
2) Place the homebrew launcher boot.3dsx from [here](https://github.com/fincs/new-hbmenu/releases/tag/v2.2.0) also on the root of your sd card.
3) With wifi on and working, scan [this QR](http://api.qrserver.com/v1/create-qr-code/?color=000000&bgcolor=FFFFFF&data=https%3A%2F%2Fzoogie.github.io%2Fweb%2Fnbhax&qzone=1&margin=0&size=400x400&ecc=L) after pressing L+R should buttons together and tapping the QR button on the bottom screen. The link to the sploit page is https://zoogie.github.io/web/nbhax if you want to type it in manually and/or bookmark it.
4) Click on the "PROCEED TO HAXX" button and the exploit should then load the homebrew menu. Make sure to add homebrews to the sdmc:/3ds folder first in order to have something to run. See other guides online about what you can do with homebrew.

## Exploit details

This is a Use-After-Free based on the layout crash test [here](https://github.com/WebKit/webkit/blob/master/LayoutTests/fast/canvas/canvas-bg-multiple-removal.html).

## Troubleshooting

- Problem: The 3ds freezes on a yellow screen.<br>
Solution: Try again. Boot rate is about 75-80%. This has always been an issue with *hax homebrew and not specific to this implementation.* If this keeps occurring over and over, it's likely being caused by running browserhax while cfw (luma3ds + boot9strap) is already installed -- don't do this! Follow https://3ds.hacks.guide for proper instructions on how to launch .3dsx homebrew under cfw. Hard freezing with regular screens (ie no solid colored screen) can also indicate running under cfw.

- Problem: The 3ds freezes on some other color screen or "An error has occured" prompt shows up.<br>
Solution: Make sure you have *all* the correct files. Check your region is correct.<br>
At minimum, make sure to have the below 3 files in the sd root as shown.<br>
```
sdmc:/arm11code.bin
sdmc:/browserhax_hblauncher_ropbin_payload.bin
sdmc:/boot.3dsx
```

- Problem: I still can't get the exploit to work and the two solutions above didn't help.<br>
Solution: Go to your browser's settings and select Clear History and Delete Cookies. Now create a bookmark with https://zoogie.github.io/web/nbhax as the address (or just edit an existing bookmark). Exit the browser, then launch it again (this saves your changes), and then finally launch that nbhax bookmark you just made. It may also be helpful to power cycle the 3ds in between attempts if the exploit is still being stubborn.

## FAQ
Q: Will you support new3ds, new2ds?<br>
A: Always have :p https://github.com/zoogie/new-browserhax

Q: Will you support the other 2 minor regions (China, Taiwan)?<br>
A: They are supported now, sort of. The exploit has been ported successfully, but a different method is being used and that requires hack.guide/youtuber updates to address the new method (not very likely there will be any interest). You may go ahead and try with my minimal instructions included [here](https://github.com/zoogie/old-browserhax/releases/download/v1.1/CHINA_TAIWAN_ONLY-BETA.zip), but be warned that this is "experts only" given they're very minimalist and lack hand-holding. Proceed with caution.

Q: Can I install [unSAFE_MODE](https://github.com/zoogie/unSAFE_MODE) with this to get cfw?<br>
A: Absolutely, be my guest : ) You can boot slotTool.3dsx and install the hacked wifi slots, then run the unSAFE_MODE exploit. No explicit directions will be given for that here, but guides should pop up soon with directions.

Q: Where did this browser exploit come from originally?<br>
A: There's no CVE of this exploit that I know of. It is based on that webkit layout test I mentioned above. The adding and removing of objects, then crashing made it seem like a use-after-free was the obvious culprit. I tested my theory with heap spraying dynamically sized fuzz objects, and I got a crash with PC control pretty quickly : )

Q: The 3ds_browserhax_common code you used works in php server code, why does your hax just use a github io page?<br>
A: I used a local webserver to emit the unescape output of y8's hb loading code, then converted it to a u32int array for my implementation. I used [this script](https://gist.github.com/zoogie/42adb5eab6b7f813f569f5250f7c800f) for the conversion. I just really wanted to avoid having to set up a server or asking someone else for that favor.

Q: Will this exploit be fixed in a firmware update?<br>
A: Don't know, but it's definitely possible. N has never fixed one of my exploits but they've always been proactive about fixing browser exploits. I give it 50/50 odds.

