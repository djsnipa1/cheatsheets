# NiftyWindows Help

### <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>BACKSPACE</kbd>

This powerful hotkey removes *all* visual effects (like on exit) that have been made before by NiftyWindows. You can use
this action as a fall-back solution to quickly revert any always-on-top, rolled windows and transparency features you've
set before.

> Note: This hotkey is particularly important during your test stage to revert some nifty visual effects after you 
completed a single feature test and before you're going to test the next. So keep it in mind!

### RIGHT BUTTON + DRAG

This is the most powerful feature of NiftyWindows. The area of every window is tiled in a virtual 9-cell grid with three
columns and rows. The center cell is the largest one and you can grab and move a window around by clicking and holding 
it with the right mouse button. The other eight corner cells are used to resize a resizable window in the same manner.

> Note: This drag and resize feature is not provided on some certain windows because this mouse behaviour may have a 
special handling controlled by the application itself. You can use the forced mode (see explanation in the introduction
of 'features') to manipulate these windows as well. Currently the following windows (and its possible child windows) 
have been taken into account:

>> Windows Explorer; Cabinet; Internet Explorer; Mozilla/Firefox; Opera; Xplore

### <kbd>CTRL</kbd> + RIGHT BUTTON + DRAG

This modifier enables the forced mode for this action as
described in the introduction of 'features'.

### <kbd>SHIFT</kbd> + RIGHT BUTTON + DRAG

This modifier lets the window bounds snap to a virtual 10 pixel grid to ease window alignment and to allow a complex 
window arrangement.

### <kbd>WIN</kbd> + RIGHT BUTTON + DRAG

This modifier lets you resize all four edges of a window in a symmetrical manner around the window center.

### <kbd>ALT</kbd> + RIGHT BUTTON + DRAG

This modifier locks the width and height ratio (aka aspect ratio) during the resize operation.

### RIGHT BUTTON + LEFT BUTTON

Minimizes the selected window (if minimizable) to the task bar. If you press the left button over the titlebar the 
selected window will be rolled up instead of being minimized. You have to apply this action again to roll the window back down.

> Note: If you exit NiftyWindows all rolled windows will be unrolled first.

### <kbd>CTRL</kbd> + RIGHT BUTTON + LEFT BUTTON

This modifier enables the forced mode for this action as described in the introduction of 'features'.

### <kbd>CTRL</kbd> + <kbd>WIN</kbd> + <kbd>R</kbd>

Unrolls all windows (like on exit) that have been rolled up before by NiftyWindows.

### RIGHT BUTTON + MIDDLE BUTTON

Closes the selected window (if closeable) as if you click the close button in the titlebar. If you press the middle 
button over the titlebar the selected window will be sent to the bottom of the window stack instead of being closed.

### <kbd>CTRL</kbd> + RIGHT BUTTON + MIDDLE BUTTON

This modifier enables the forced mode for this action as described in the introduction of 'features'.

### RIGHT BUTTON + WHEEL

Provides a quick task switcher (alt-tab-menu) controlled by the mouse wheel.

> Note: If you like task switching by using the alt-tab-menu you should give Microsoft's 'Alt-Tab Replacement' (part 
of the PowerToys) a try. With this PowerToy, in addition to seeing the icon of the application window you are 
switching to, you will also see a preview of the page. This helps particularly when multiple sessions of an application
are open.

[Microsoft PowerToys](http://www.microsoft.com/windowsxp/downloads/powertoys/xppowertoys.mspx)

### MIDDLE BUTTON

Initiates a double click.

### FOURTH BUTTON

This additional button is used to toggle the windows start menu.

### FIFTH BUTTON

This additional button is used to toggle the maximize state of the active window (if maximizable).

### <kbd>CTRL</kbd> + FIFTH_BUTTON

This modifier enables the forced mode for this action as described in the introduction of 'features'.

### <kbd>WIN</kbd> + <kbd>0</kbd> .. <kbd>9</kbd> 

Opens or closes an installed CD/DVD-ROM reader/writer drive tray. The drives are assigned to their hotkeys by the certain drive number in your system. The hotkeys are used in the sequence of 
the key placement on your physical keyboard from left to right (1 refers to the first and 0 to the tenth drive). So you are limited to a total number of 10 drives controlled by NiftyWindows.

> Example: If you press <kbd>WIN</kbd> + <kbd>1</kbd> the first drive found (ordered by their drive letters) will be opened or closed (depends on the current state).

> Note: During the open or close operation NiftyWindows is suspended (and waiting) so you can control only a single drive per time. If you want to open or close more than one drive you have to do it sequentially.

### PAUSE

Toggles the muteness of an installed audio card.

### <kbd>WIN</kbd> + <kbd>S</kbd>

Starts the user defined screensaver (password protection aware).

### <kbd>CTRL</kbd> + <kbd>WIN</kbd> + <kbd>S</kbd>

This does the same as the feature described above with the addition that the display(s) will be powered down shortly 
(five seconds) after the screensaver started successfully. This feature is very useful if you already know that you are 
going to leave the system for a long period of time.

> Note: If you perform any user input that ends the saver in the first seconds certainly the display(s) will not be 
powered down. After the display(s) were powered down you can wake them up by any key or mouse inputs as well known.

### <kbd>WIN</kbd> + LEFT BUTTON ___OR___ <kbd>WIN</kbd> + <kbd>^</kbd>

Toggles the always-on-top attribute of the selected/active window.

> Note: If you exit NiftyWindows any always-on-top attributes will be removed first.

### <kbd>CTRL</kbd> + <kbd>WIN</kbd> + <kbd>^</kbd>

Removes any always-on-top attributes (like on exit) that have been set before by NiftyWindows.

### <kbd>WIN</kbd> + WHEEL

Adjusts the transparency of the active window in ten percent steps (opaque = 100%) which allows the contents of the
windows behind it to shine through. If the window is completely transparent (0%) the window is still there and
clickable. If you loose a transparent window it will be extremly complicated to find it again because it's invisible 
(see the first hotkey in this list for emergency help in such situations).

> Note: This mode is called window-transparency. This feature is only supported on Windows 2000/XP or later and needs 
a powerful processor and video card installed in your system. If you exit NiftyWindows any transparency effects will be
removed first.

### <kbd>SHIFT</kbd> + <kbd>WIN</kbd> + WHEEL

This modifier decreases the percent steps to one (instead of ten) for a more accurate control.

### <kbd>WIN</kbd> + <kbd>CTRL</kbd> + LEFT BUTTON

Makes all pixels of the same color the mouse cursor points at invisible inside the target window, which allows the 
contents of the windows behind it to show through. If the user clicks on an invisible pixel, the click will "fall 
through" to the window behind it. You should always be concentrated by using this feature. Otherwise you can loose some
windows completely (see the first hotkey in this list for emergency help in such situations).

> Note: This mode is called pixel-transparency. This feature is only supported on Windows 2000/XP or later and needs a 
powerful processor and video card installed in your system. If you exit NiftyWindows any transparency effects will be 
removed first.

### <kbd>WIN</kbd> + <kbd>CTRL</kbd> + MIDDLE BUTTON

Provides a special combination of multiple features (window-transparency & pixel-transparency & always-on-top). This 
action is intended to be used on small dialogs (e.g. file-copy or download with progress bar). By using this feature 
you can modify an important dialog to stay inside your field of vision all the time without affecting your 
concentration. You have to revert these changes manually by using the well known features of NiftyWindows (see the first
hotkey in this list for emergency help in such situations).

> Note: This mode combines 25% window-transparency and the pixel-transparency (pixel color at mouse click position). 
These features are only supported on Windows 2000/XP or later and needs a powerful processor and video card installed 
in your system. If you exit NiftyWindows any transparency effects will be removed first.

### <kbd>WIN</kbd> + MIDDLE BUTTON

Removes any transparency effects (windows- as well as pixel-transparency) of the selected window.

> Note: If you use pixel transparency you have to click on any remaining visible part of the window otherwise the 
action is catched by the window behind it as described above.

### <kbd>CTRL</kbd> + <kbd>WIN</kbd> + <kbd>T</kbd>

Removes any transparency effects (like on exit) that have been set before by NiftyWindows.

### <kbd>ALT</kbd> + WHEEL 

Changes the size of the active window in ten percent steps which allows a very quick resize operation with simply two snatches.

### <kbd>CTRL</kbd> + <kbd>ALT</kbd> + WHEEL

This modifier enables the forced mode for this action as described in the introduction of 'features'.

### <kbd>SHIFT</kbd> + <kbd>ALT</kbd> + WHEEL

This modifier decreases the percent steps to one (instead of ten) for a more accurate control.

### <kbd>WIN</kbd> + <kbd>ALT</kbd> + WHEEL

This modifier lets you resize all four edges of a window in a symmetrical manner around the window center.

### <kbd>ALT</kbd> + <kbd>NumAdd</kbd> ___OR___ <kbd>ALT</kbd> + <kbd>NumSub</kbd>

Changes the size of the active window in steps of the standard screen resolutions. /ALT+NumAdd/ increases to the next 
higher, /ALT+NumSub/ decreases to the previous lower standard resolution.

> This feature is very useful for testing web pages: you can easily set your browser window to any common screen resolution.

### <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>NumAdd</kbd> ___OR___ <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>NumSub</kbd>

This modifier enables the forced mode for this action as described in the introduction of 'features'.

### <kbd>WIN</kbd> + <kbd>F1</kbd> ... <kbd>F24</kbd>

Activates the next window in a process window group that was defined gradually before with the given /CTRL/ modifier. 
This feature causes the first window of the responsible group to be activated. Using it a second time will activate the
next window in the series and so on. By using process window groups you can organize and access your process windows in
semantic groups quickly.

> Note: When a window is activated immediately after another window was activated, the task bar buttons may start 
flashing on some systems (depending on OS and settings).

### <kbd>CTRL</kbd> + <kbd>WIN</kbd> + <kbd>F1</kbd> ... <kbd>F24</kbd>

This modifier adds all windows of the active process to the responsible group.

### <kbd>ALT</kbd> + <kbd>WIN</kbd> + <kbd>F1</kbd> ... <kbd>F24</kbd>

This modifier closes *all* windows of the responsible group.

### <kbd>WIN</kbd> + <kbd>ESC</kbd>

By pressing this hotkey you can disable (and reenable) all NiftyWindows mouse and keyboard features at once. This is 
commonly used when you're going to start a special application that handles some triggers itself or when you want to 
temporarily disable NiftyWindows.

> Note: There is an auto suspend mode that can be enabled/disabled in the tray icon menu. This auto mode disables 
NiftyWindows temporarily as soon as a fullscreen window (propably a 3D game) was activated (gain focus). After the 
fullscreen window was deactivated (lost focus) NiftyWindows is enabled again.

### <kbd>WIN</kbd> + <kbd>X</kbd>

Exits NiftyWindows.

> Note: If the tray icon is hidden this hotkey will show it again (if it is already visible NiftyWindows will exit as expected).

