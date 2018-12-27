How to Use
--------------
You will need to have an environment that uses a command line terminal and devkitPro installed. How to set that up is out-of-scope from these steps.
This branch is compatible with [Navenatox's Dynamic Overworld Palettes](https://github.com/Navenatox/DynamicOverworldPalettes) patch.

1. Assemble Navenatox_Pallete_Patch_Fix.asm and insert into free space.

2. Change rtc.asm's updateNPCPal offset one line 436 to the offset you inserted Navenatox_Pallete_Patch_Fix.asm. Keep the +1.

3. Put your FireRed rom named Test.gba into the mapfilter folder. Run compile.sh and npcmod.c will be inserted for you into the rom. Then assemble and insert mapfilter/npchook.asm at 0x80598CC.
   You can also choose to customize where to insert npcmod.c by editing B02500, but then you will have to modify mapfilter/npchook.asm to point to the new offset.

4. Put your FireRed rom named Test.gba into the npcfilter folder. Run compile.sh and npcmod.c will be inserted for you into the rom. Then assemble and insert npcfilter/npchook.asm at 0x8083598.
   You can also choose to customize where to insert npcmod.c by editing B01500, but then you will have to modify npcfilter/npchook.asm to point to the new offset.

5. Now assemble and insert rtc.asm into free space. You can change the 0x8B01000 at the top to your desired free space as 0x8XXXXXX where XX XX XX is your desired free space. In the assembled file, ignore all of the FF's.
   Insert 00 B5 01 48 00 47 00 00 XX+1 XX XX 08 00 00 10 BC at 0x80004B0 where XX XX XX is the reversed offset of where you inserted rtc.asm. 
   For example, my offset is 0x8B01000 so I put 01 10 B0 in that spot.

6. At 0x8059A28 to 0x8059A2F, add 00's. At 0x8059A12, add 00 00.

Note: If you have an error with -lgcc when running compile.sh, change line 19 in the makefile in the current folder you're in to have the correct version of arm-none-eabi in your $DEVKITARM/gcc/lib/arm-none-eabi folder.
      For example, mine had an 8.1.0 folder in it so I changed the 4.7.1 to 8.1.0 in line 19.


Wizard-DN
--------------

This is a day/night system initially designed on Fire Red and soon to be ported to Emerald and (maybe) Ruby. The core principle in this D/N system is gradients and ease of use for the user. Instead of doing sloppy, faster masks, this D/N system uses an intelligent and fast blending system which will blend 32 bit ARGB colors with the existing colors in the palette, allowing for more natural colors depending on the time of day. In addition to the palette blending, a 144 color gradient is used to create a smooth transition between times of day. The difference is clearly visible in these two pre-rendered GIFs which were made using MEH:

![GIF](http://giant.gfycat.com/LateSpiffyHyrax.gif)
![GIF](http://fat.gfycat.com/FlippantBoilingFeline.gif)

Full Source is obviously provided here under GPLv3. This means that any modifications publicly released must also provide their source code as well.


GPL License
---------------

Copyright (C) 2014 Shiny Quagsire, diegoisawesome, and others

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>
To contact the author of this work, e-mail him at mtinc2@gmail.com
