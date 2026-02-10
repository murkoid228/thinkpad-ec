Description of the patch sets
-----------------------------

This repository has several sets of patches - for keyboard remapping,
battery validation, and Caps Lock LED support.  The battery and Caps Lock
LED patches are disabled by default, but are easy to enable.

Any combination of the patch sets can be enabled or disabled (even
including a version with no patches at all - to revert all changes)

After changing the configuration, you will need to build the patched EC
image as normal.

### KEYBOARD patchset

Applying this set of patches will adjust your Embedded Controller to support
the slightly different keymapping used with a xx20 keyboard.  If you prefer
to use the older 7-row keyboard instead of the newer xx30 6-row keyboard, then
you want this patchset enabled.  It is enabled by default.

### BATTERY patchset

Applying this set of patches will disable the check that the system makes for
Lenovo original batteries.  If you wish to use aftermarket batteries, then
you want to enable this patchset.  It is disabled by default.

Note that this authentic battery check was done by Lenovo for a good reason
as aftermarket battery construction and quality is highly variable.  There
have been a number of people who have discovered that their aftermarket
battery is not working even after installing this patch and (so far) they
have all found that the battery itself was broken.

### CAPSLOCK_LED patchset

Applying this patch enables the Caps Lock LED on the classic X220 keyboard
when installed in an X230.  The X220 keyboard has an LED in the Caps Lock
key driven by keyboard connector pin 21, which is routed to EC GPIO163 on
the X230 motherboard.  This patch configures GPIO163 to drive the LED based
on the Caps Lock state.  It is disabled by default and only useful for x230
with an X220 classic keyboard installed.

Configuring which patches are used
----------------------------------

There are several makefile targets that exist to help you configure which
patches are enabled.  Choose one or more of the following commands to
configure as you want:

    make patch_enable_battery clean        # Uses the battery validate patch
    make patch_disable_battery clean       # Turns off the battery validate patch
    make patch_enable_keyboard clean       # Uses the keyboard patches
    make patch_disable_keyboard clean      # Turns off the keyboard patches
    make patch_enable_capslock_led clean   # Enables the Caps Lock LED patch
    make patch_disable_capslock_led clean  # Turns off the Caps Lock LED patch

The selected commands from the above list simply need to be typed in exactly
as shown, at the command prompt, before building the patched image, while
following the Step-by-step instructions (This is step 6)


Behind the scenes
-----------------

Each hardware and EC firmware version combination needs its own set of
patches, which are stored in directories called "*.img.d".  The Makefile
defines these patches into named groups ("KEYBOARD", "BATTERY", and
"CAPSLOCK_LED") which can be enabled or disabled via a config file.

The enable and disable commands are simply updating the config file with
the appropriate settings.
