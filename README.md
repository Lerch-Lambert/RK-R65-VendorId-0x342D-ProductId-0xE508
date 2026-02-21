Details on issues and solutions are provided below.  If you don't care about the details and just want to use this json file, first make sure that you have a keyboard with the same Vendor ID and Product ID.

To check these IDs, open up Microsoft Edge and navigate to edge://usb-internals/
Click the Devices tab on this page, and look for the Product name "RK-R65."
Take note of the Vendor ID and the Product ID.
For this json, you should be using Vendor ID 0x342D, and Product ID 0xE508.

If these IDs match, download the json file here, then navigate to https://usevia.app/
Click the settings tab (gear icon), and turn on "Show Design tab."
Navigate to the Design tab (paintbrush icon), and click "Load" next to "Load Draft Definition."
Load the json file you just downloaded into VIA, and authorize the device.

Now when you go to the Configure tab, you should see the customization options for the keyboard.  Layers 0 and 1 seem to be for when you have the keyboard in Windows mode (activated with Fn + A).  Layers 2 and 3 seem to be for Mac systems (activated with Fn + S).  The remaining layers are layers that can be switched into using the Function/Layer keys within the configuration.


Details:

I recently bought a new keyboard from Amazon, and started looking for a json to customize the keyboard in VIA.  Most of the *.json files that I found for the Royal Kludge R65 QMK/VIA wired keyboard were setup for a different version of the keyboard.  Most of them used the Product ID of 0xE453, or some other E4xx series.  I even found that several had completely different Vendor IDs.  This lead to the json files not working properly in VIA with my keyboard, which meant I could not customize any of the keys.

The second problem is that even when I changed the Product ID and Vendor ID within the json to match my keyboard, the keys were all skewed to the wrong positions within the configuration tab of VIA.  It turns out that this was happening because of a design oversight on the keyboard.  The physical keyboard has 15 columns.  However, it seems that the firmware on the keyboard is 16 columns.  There was one simple line of code in the json that resolved this issue (changed 15 to 16).

I changed the following lines within the json file to get this keyboard working properly with VIA.

  "vendorId": "0x342D",
  
  "productId": "0xE508",

AND

  "matrix": {"rows": 5, "cols": 16},

I want to also not that there were minor issues with some of the code that labels each key.  This doesn't really affect what you see when editing the keyboard in VIA, but can affect what you see when using some other types of keyboard software.  I changed edited the labels on each key so that they can be easily identified for anyone using some other keyboard software or json editor.


Troubleshooting:

If you are having issues with this json file, double-check that the Vendor ID and Product ID are exactly as specified.  If they are not, you can try editing these lines within the json file to see if they will work properly that way.  However, you may also have to edit the rows/columns if the keyboard is significantly different from the one that this json file was created for.  Beyond this, I'm not sure what else might cause problems.  You will have to do some additional troubleshooting, and possibly asking around on reddit or Discord about your specific issue.
