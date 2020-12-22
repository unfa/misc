# Ardour MIDI Masterclass

The Complete Ardour 6 MIDI Tutorial
Noob2Pro in 1 video
The Good, The Bugs and The WTF

Ardour's MIDI workflow is a bit strange. It's also a bit lacking and even a bit buggy.
Despite this every month on my livestreams I play dozens of amazing tracks made with Ardour.
And I'm not even talking abotu my own work, these are viewer submissions.
How do they do it? How do I do it? I will show you.

In this video I'll teach you *everything* there is to know about MIDI in Ardour.
If you'd like a written version of this video, the link is in the description.
Also check out the timestamps if you're looking for a specific thing.

As I'm recording this the latest official release of Ardour is *6.3*.
Make sure you're up to date before proceeding.

## Intro

[ post-intro scene ]

You ready?

## Clean Slate

This is what Ardour 6.3 looks like if you create a new session after a fresh install.

## Ardour Configuration
There's a few settings I highly recommend you change before we start making sounds.

### Audible MIDI editing feedback
Go to Edit > Preferences > MIDI > and make sure "Sound MIDI notes as they are selected in the editor" is enabled. With this setting on - Ardour will play any MIDI notes you touch in the editor. Otherwise - the only way to hear what you're doing is to play the timeline.

### Independent MIDI region copies
Go to Session > Properties > Misc > MIDI Options and enable "MIDI region copies are independent".
After you got that click on "Use these settings as defaults" so you don't have to repeat what we just did for each new session.

Why do I recommend you change this? By default if you duplicate a MIDI region in the editor - the copy will be linked, so if you then modify either the copy or the original region - the other will also change, and you might not notice that until much later. This could be a very cool feature, but it's missing visual feedback and functionality - so for now I recommend you keep all your MIDI regions independent.

### Overlapping MIDI notes on the same channel

While we're here, there's another setting that determines what Ardour will do if you have two notes playing the same pitch on the same MIDI channel. Usually that's not a valid thing to have, as it may result in stuck notes. If you're having problems with that - maybe play with it. I personally prefer full manual control.

### Editor Mixer
Another thing I always enable right away is the "Editor Mixer" - go to View and select Show Editor Mixer from the main menu, or use the Shift+E keyboard shortcut.

This will bring up a mixer strip for the currently selected track or bus. I have this on all the time, and I think it's very convenient. I rarely need to use the full-blown mixer view thanks to this thing.

### Tempo grid not emphasizing beats
If you're still running Ardour 6.0 - either update or we'll have to fix one thing for you. Otherwise skip ahead here: [ insert timestamp ]

In Ardour 6.0 the color themes have changed in a way that the beat lines are not emphasized if you use anything finer than a quarter note grid. To fix this, we need to change one value in Ardour's color theme. No worries - we won't have to touch any configuration files.

Go to Edit > Preferences > Appearance > Colors > Items > and find "grid line minor" - as you can see the **Grid Line Minor** and **Grid Line Micro** colors are identical, which is not what we want. I recommend you change Grid Line Micro (which is used for the quarter notes, or beats) to a different color. The default is "neutral:midground", and I'd propose to use "neutral:foreground2" instead. Done!

## Adding MIDI tracks

Now that our environment is ready, let's look into creating MIDI Tracks. MIDI Tracks are what allows us to record, sequence and edit MIDI data that can drive virtual or hardware instruments.

There's three ways to open the dialog window for adding tracks.

1. From the main menu go to Track > Add Track, Bus or VCA...

or 

2. Use the Ctrl+Shift+N keyboard shortcut (you can memorize it as N for New Track)

or

3. Right-click in the empty space under the track headers. Not in the timeline itself though, that does nothing.

Let's change the track type to MIDI. As you can see the available options have changed a little. They're all described in the dialog itself - you can reference that if in doubt.

Let's take a closer look at all the available settings here.

- We can choose how many tracks we want to add at once.

- Obviously we can specify the name for the new track (or tracks) - if we add multiple, Ardour will add sequential numbers at the end, as tracks and buses must have unique names.

- Below we can select the instrument plug-in that the track will be created with. Ardour will list all available instrument plug-ins here. I'll keep the default "General MIDI Synthesizer" for now. It's a stock Ardour plug-in that unsurprisingly plays a General MIDI soundfont installed on your system. You can also select **-none-** which is on the top of the list (use the Home key on your keyboard to go there) . Note that I have installed a lot of 3rd party plug-ins in my system, and Ardour itself comes with a very minimal set of stock virtual instruments.

- Pin Mode is mostly useful for Audio tracks - the **Strict-I/O** mode keeps the number of the audio output ports identical to the input ports, no matter the intermediate port layouts of the inserted plug-ins. For MIDI tracks this doesn't matter unless you're also going to add additional audio inputs (as any track or bus in Ardour can have any number of audio and MIDI inputs and outputs - these types listed here are just presets made for our convenience).

- You can also choose to add the newly created tracks to a group right away, or make a new group out of them - I never used that though.

- The last setting is Position - this will determine where the new tracks will be placed vertically. It's very useful if you have a lot of tracks and shuffling them up and down becomes an ordeal.

There's two things we can do now - select "Add and Close" which will do exactly as stated on the label, but we can also add the tracks _and_ keep the dialog open to add more with different settings. Let's Add and Close for now.

The MIDI track is here, it has the selected instrument plug-in placed in the processor box, and the stereo audio output should automatically be connected to the Master Bus. Sweet.

There's two more special ways to create MIDI tracks: drag a MIDI region down to empty space, or import a MIDI file into a new track - I'll cover them in detail later.

\\ If all went well and you have configured your MIDI keyboard as I have shown you before - if you now select the new track and hit a key on your controller - you should hear a piano note.

### Instrument plug-ins missing from the list

There's one quirk that I've found with the virtual instrument list in the new track dialog - it can fail to include an instrument plug-in that has auxiliary audio inputs.
If that happens:

[ Demonstrate with Surge LV2 ]

1. Create a MIDI track using "-none-".
2. Add the new instrument plug-in manually
3. Make sure it's located above the fader in the processor box.
4. Disable the Strict-I/O setting to fix audio port routing
5. Rename and Duplicate the track if needed.

## Operations on Tracks

### Duplicating Tracks

To duplicate a track right-click on the track's header for a context menu and select "Duplicate...".

We can specify how many duplicates we want - let's choose 7, we can choose how Ardour should treat the source track's playlist (the default is sane here, let's use that), and the position of the new tracks.
I'll touch on playlists later in this video.

Click OK.

Now we've got our duplicates.

### Selecting and Deleting Tracks

Let's say I changed my mind, and I want to get rid of some tracks.

I'll select the first one by clicking on the header - to select more - you can hold Ctrl and pick them one by one [ select 3 tracks ], or hold Shift and click to select a whole range at once [select all but the first and last track ]

Right click for context menu and choose "Remove". Note that the same options (and more) are in the main menu's Track section.

Ardour will warn you that deleting tracks is permanent. There's no undo. So if you're not sure - I recommend you make a snapshot first to be able to go back. I'm going to show you how to do that in a second. For now - let's delete the tracks.

## Renaming Tracks

We've got the tracks we want, now let's rename them.
Double click on the track's name to edit it [ name first track ~~Paino~~ Piano ]. If you press Tab or Shift+Tab you'll jump between tracks up and down - this way you can easily rename a bunch at once [ name the second track Piano 2 ]

### Deactivating & Hiding Tracks

Sometimes you know you'll need a track later, but for now it's only taking up resources and screen space - you can deactivate or hide tracks though.
Deactivated tracks are not processed by Ardour, so they don't consume CPU, but they will still use your system's memory, so if you've got some heavy samplers that are hogging your RAM (like DrumGizmo)- Deactivating them will not help with that.

### Deactivating a Track

Let's deactivate a track. Right click on the track header and click on "Active" to disable it. You can see that the track is grayed out and it's name is now in parenthesis.

## Hiding a Track

Hiding tracks only cleans up your timeline view. Hidden tracks can sill be active and play sounds - you can spook your collab mates this way. Just please don't use loud sounds or I will personally shred your system disk's partition table, and I will also eat your lunch.

Ok, let's now hide this track. Right click on the track header and select "Hide".

## Unhiding Tracks

If you want to show hidden tracks again - you can do so with The Editor List. Open it up from the main menu with **View > Show Editor List** or with the Shift+L keyboard shortcut. It has many tabs, but the one we need is right at the top - "Tracks & Buses".

Here you can easily control which tracks are visible and active. You can also rename tracks right in here if you double click on the names!
Let's activate and unhide both tracks.

## Making session snapshots

This is a bit tangential to the MIDI topic, but I think it's a good idea to teach you this.
Ardour can manage multiple versions of your project - it's the .ardour file, containing all the information related to your project's arrangement.
What I do every time I sit down to work on a project again - I create a new snapshot and switch to it before I do any work.

From Main Menu go to Session and select **Snapshot (and switch to new version)**
If you've got unsaved changes Ardour will first ask if you want to save them, before it creates a new project snapshot and switches to it.

I name my snapshots with incremental numbers so that it's clear which one is the latest in case I mess something up and want to reference a previous version of my project. To load an older snapshot, go to _Session > Recent..._.
Click on the arrow by the Project name to expand the snapshot list. By default Ardour will always load the latest one.

## Recording MIDI

Finally we can record some MIDI!

Assuming you have a MIDI controller keyboard or a MIDI dance pad, I'll show you now - how to capture your performance. If you don't have such devices, there's still some options for you that I'll cover in a moment.

First thing you need to do is obviously make sure your MIDI input device is connected to your computer - mine is a USB keyboard.

Now let's select the MIDI track, and hover over the INPUT button. It shows "ardour" and the tooltip soon confirms that the track is now fed input from Ardour's Virtual MIDI keyboard.
That's nice, we'll talk about this in a while, but we want a real, physical MIDI keyboard right now.

Let's click on the INPUT button. There's a context menu with a bunch of options.

The first one will disconnect all inputs.
Next is a list of all available system MIDI sources Ardour has detected. My MIDI keyboard is listed here as Oxygen 49 - let's select that.

Now if I hit a key on my keyboard - the MIDI track will receive the MIDI data and push it through the instrument plug-in, turning it into a stereo audio signal, that is then pushed to the master bus.
In short: you should be able to hear a piano note.
Good.

Now to capture a performance, we need to first arm the track for recording - it's the big red button of course.

Now we have two options. Either use the mouse to arm the whole session for recording, and then start the transport...

[ record something ]]

(Let's delete that)

Or - just press _Shift+Space Bar_ which'll do both at the same time instantly starting the capture.

[ record something else ]

Once you're done - press the Space Bar again to stop the transport and finish recording.
Pressing Ctrl+Spacebar will stop, delete the last capture and rewind your playhead as if nothing has ever happened.
Useful if you've made a horrible mistake, need to forget about it and promptly start over.

A very useful thing is the "Auto Return" option for transport which will rewind your playhead without deleting anything.
You can enable it on the toolbar or by pressing the number 7 on your alphanumeric keypad.

When you stop the transport, it'll automatically return the playhead back to where it was when you started. This is great for two things - re-recording a part over and over or listening to a part of your project and iteratively tweaking it.

### Playlists

Now let's talk about Playlists. Each track in Ardour - either audio or MIDI can have multiple playlists. You can think of this as alternate takes. I most often use this to record multiple different vocal performances for songs. Instead of duplicating a track and stashing it as a backup copy I can just create a new playlist. We can either make the new playlist a copy of the current one, or have it be empty.

Let's create a new playlist here and record something onto it.

I can now switch between different takes. One downside is that I'd need another "temporary" track if I want to comp segments from both playlists, as I can't access them at the same time from a single track.
The easiest way to deal with this is to use another track as a buffer.

I'll use this second piano track to view my other playlist and drag a region from it onto the first one.

There's also an option to select a playlist from another track.
Click on the P button, choose "Select from All...".
Now expand Other tracks, choose Piano and select the second playlist.

Now I can move regions between playlists!

Watch out though as playlists are still a little bit buggy in my experience.

### Metronome

Another useful thing for recording is the metronome or click. You can toggle it with the button on the toolbar or with the Tilde key on your keyboard. Also - check the button tooltip for extra options. You can change the click volume with your mouse wheel for example or right click to jump into preferences.

## The Virtual MIDI keyboard

Now some good news for those of you who don't have access to a MIDI keyboard or a MIDI dance pad for that matter.

Ardour 6 introduced the _Virtual_ MIDI keyboard.
You can access it from the Main Menu: Window > Virtual Keyboard

The virtual keyboard window will stay above other windows, so unless you put it away in a corner and forget about it - it's gonna stay visible.
Now - by default you'll only have 1,5 octaves of your computer keyboard mapped to MIDI.
We can change that however.

Let's go to Edit > Preferences > MIDI > Virtual Keyboard. The default layout is "QWERTY Single" - that means only one row of keys (technically it's two rows, since we have white and black keys mapped here) will be used. If you switch to QWERTY instead - you'll see the assigned keys have changed and now we have more than 2 MIDI octaves mapped to our computer keyboard - this of course comes at the cost of less of Ardour's hotkeys being usable while the Virtual Keyboard is open, as it'll take precedence and steal these key presses for itself!

If you'd prefer to keep your hotkeys operational and only use the Virtual Keyboard with your mouse - just select *Mouse Only - (no keyboard)* in the keyboard layout. This option was introduced after the Ardour 6.2 release on my request. Thanks Robin!

I'll set this back to *QWERTY - Single* and close the preferences dialog window for now.
Let's take a closer look at the keyboard itself.

Of course you can use it with your mouse to trigger MIDI notes, but what do all of these controls do?


- Choose the MIDI channel the MIDI messages are sent on.
- Virtual Pitchbend and Modulation wheel.
- 4 virtual MIDI CC knobs - you can choose the CC number with the dropdown.
- Change the middle C octave, and the octave range of the keyboard.
- MIDI note velocity. You can either select from a few common values or scroll your mouse to fine tune.
- Chromatic Note Transpose - you can use this to, for example, play in A-minor while having the notes be generated in a different key.
- And last: MIDI Panic. This forces all MIDI notes currently playing on the active MIDI channel to stop immediately.

## MIDI Tracer

While we're at it I think it's good to mention the MIDI Tracer. It's a great tool to troubleshoot MIDI problems.

You can open it - again - from the main menu > Window > MIDI Tracer.

It let's you see the exact MIDI data being sent or received on any port in Ardour.
Let's pick the Virtual Keyboard and see what we get.

[ click on some keys and move a CC knob ]

Yeah, it works! I'll leave the extra settings on the bottom for you to try out.

[ close the virtual keyboard and the MIDI tracer window ]

## Creating MIDI regions

Ok, let's get back to our MIDI track and create some MIDI regions manually - that is - sequencing stuff with the mouse, as opposed to capturing a live performance.

To create a MIDI region - first you need to activate the Draw Mode. You can either use a Toolbar button, or just hit the D key on your keyboard. I recommend you learn the hotkeys as they're gonna save you a lot of time in the long run.

Here's my list of Tool Hotkeys in order of importance:

Grab - G
Draw - D
Edit - E
Timestretch - T
Cut - C
Audition - A

So hit D to Draw, now click and drag on the MIDI track where you want to create an empty MIDI region.
You can see that now if I hover my mouse over this new MIDI region, I can draw notes inside straight away.

[ Insert 3 notes ]

This is cool and all, but this region isn't following the grid, so let's enable snapping and correct that first.

Enable Snap, I'll choose quarter note grid.

To move and resize regions we'll need to switch to the Grab mode using the G key.

Now let's move the region to align it's start. Click on the regions center and drag left. Good. Now I'll change it's length by hovering over the right edge until the mouse cursor changes shape. Let's click and drag again. This region now fills an entire bar. We'll insert some notes in a while, but first - I need to tell you about

### Navigating the view

Ardour doesn't have a dedicated Piano Roll editor - each MIDI track has it's own embedded one, and you'll edit the MIDI notes right in the timeline. It's a bit uncommon, but once you get used to it - it does the job. The difficulty here is that you'll need to keep resizing tracks to have enough room to be precise with MIDI note editing.

I'll show you how to do that right now.

#### Zoom to Selection [Z]

You can quickly focus on your selected MIDI region or regions with the Z key. The selected regions will fill the screen, giving you maximum possible working area. The downside of course is that you can't see the context too well.

[ undo view add two automation lanes and make one of them huge for demonstration and hit Z again]

Also - note that all the visible automation lanes will be included in the view, but will not be resized, so you may need to resize these manually. Now click on your region and hit Z again to re-adjust the view.

To get back to the normal view, use the Shift+Z key combination, which works like undo for view changes - you can use it multiple times to undo multiple view changes.

[ undo until the view goes back to normal, also hide the automation lanes]

# Fit Selection (Vertical) [F]

Another useful hotkey is F. F will set the combined height of selected tracks to fill the screen vertically. Note that this one will only work if you have selected some track headers. Regions don't count.

[ demonstrate using F with selected regions to no avail ]
[ demonstrate using F with selected track headers instead ]

Again - Shift+Z will undo the view change. Unless you maximized an automation lane with this - that doesn't work as expected right now. [ bug report: https://mantis.ardour.org/view.php?id=8409]

Let's now zoom in manually. First I'll hold Ctrl and use my mouse wheel to zoom horizontally around my mouse cursor. Up and Down. Nice.
We can also zoom in and out using three buttons on the far right side of the toolbar - the third one makes sure everything between the session Start and End Markers is visible. If you need more zooming options - go to the View menu and explore the Zoom submenu. You can also learn some hotkeys there.

Now let's resize the track to get more piano roll space vertically. Hover your mouse over the track header. Now move the cursor down until it changes - this indicates that you can now click and drag to resize the track. There's a few other ways to change track height.

- You can right click on the track header for context menu and select Height (same options are in the Main Menu's > Track > Height section.
- You can also use three controls on the toolbar - one to select how many track you want to fit on the screen (for example - all), and two more that'll decrease and increase selected track's height.
- If you double click on a track's header it'll toggle between the Largest and Normal heights, so you can quickly expand a track to do some edits and then shrink it back once you're done.

Double click on all track headers to reset them to Normal

I guess creating a habit of Zooming and un-Zooming into MIDI regions could help mitigate the lack of a separate dedicated piano roll editor.

You know how to zoom around, now let's learn how to scroll the view.

The mouse wheel can do it all with the help of some modifier keys:

- Mouse Wheel alone will scroll the tracks up and down
- Shift + Mouse Wheel will scroll the timeline forward and back
- Alt + Mouse Wheel will change the active track's height
- Ctrl + Mouse Wheel, as stated before, will zoom in and out on the mouse pointer

- Page Up / Page Down keys will also scroll the tracks for you
- Home and End keys will teleport the playhead to the session Start and End markers, also affecting your view

#### Using the Summary

Another way to zoom and scroll horizontally is with the Summary panel.

- Click and drag the center to pan around the timeline
- Click and drag an edge to zoom in or out
- Use the mouse wheel to zoom in and out towards the center of the currently viewed area
- Right click and select "Reset Summary to Extents" to view the whole timeline.

### Grid

Now let's talk about the Grid snapping.

In case you don't know - grid snapping lets you make sure that whatever you do on the timeline will be aligned with the musical time of your session - that means bars, beats and that kinda stuff.
You move a region or a note - it snaps to the nearest grid line. You create a new region or a note - it starts and ends on a grid line.

You can enable or disable the grid snapping:
- with the Snap button on the toolbar
- From main menu Edit > Toggle Snap
- With the hotkey 4 on your alphanumeric keypad

If snapping is enabled, you can always temporarily disable it by holding Alt.
If it's disabled, holding Alt will temporarily enable it. I usually have Snapping on all the time and I temporarily disable it with the Alt key if needed.

As you've seen before you can change the grid size:
- using a button on the toolbar
- from the main menu _Edit > Snap & Grid_
- or with the hotkeys 5 and 6.

Snapping will also help you align objects to each other, even if they don't fit in the grid.
Let's enable snapping, hold alt, hit G and draw a region that isn't following  the grid.
Now I can resize or moe anothger region and alight it to this region's edge.

Before Ardour 6 this kinda stuff was done with a bunch of other snapping settings, now it's all automatic.

## Tempo and Meter

Since the Grid lets us enforce musical time on your editing - let's talk about the ways to influence the tempo and meter of your session so that grid snapping obeys your musical vision.

Please note that the tempo map functionality is most likely going to see a lot of changes and improvements in Ardour 7.0 but as I'm recorgding it - it doesn't exist yet.

To simply change the tempo of your session, double click on the first marker on the Tempo Ruler - this'll show you the Edit Tempo dialog.
You can get the same effect by right-clicking on one of the clocks and selecting "Edit Tempo" - you can also just click on the Tempo button beneath the secondary clock.

In the Edit Tempo dialog you can tap the tempo with your mouse or type in a value, you can also change the type of the Tempo marker - it's either constant or ramped. If you switch to ramped you'll have to enter the tempo at the end of this marker's section, but it needs a second marker to work. Otherwise the ramp should go to infinity and that doesn't make sense.

To change Meter also known as the Time Signature - use the Meter Ruler markers, the Edit Meter option in the clock context menu, or the Meter button beneath the secondary clock.

Let's now make a tempo ramp. To add a new tempo change you can either hold Ctrl and click with the left mouse button, or Right click on the tempo ruler, and select "New Tempo".
To edit the created marker either double click on it, or right click and select "Edit...".

Here we can change the tempo of course but also precisely determine the musical time at which the change should occur. There's also a setting for Lock Style - either music or audio.

This setting determines if the Tempo Markers should adjust their location when the tempo map before them is altered. Music Lock will keep the music time distances, so our tempo change will always occur at bar 7, beat 2, regardelss of how many seconds since the session start that should be.

Audio lock will ignore the musical time distances and make sure the tempo markers stay on the minutes:seconds position you've created them on. Music Lock is the sane default here as it retains the musical structure of the session as you're altering the tempo map.

Ok, we've got two Tempo markers, let's make a ramp between them.

Right click on the first tempo marker and select "Ramp to next" - now the transition will be smooth.
You can do some weird advanced stuff if you manually detemine the ramp start and end tempos, like tempo rising slowly to suddenly drop. Have fun!

Now - creating Meter changes is even simpler than Tempo, as there's no ramping involved and also you can't type in the musical time location of the marker in the dialog - it depends on where you put the marker on the timeline. 
Ctrl+Click on the Meter ruler and define the new Time Signture. To move it around - just click and drag. Note that you can only change Meter at the end of each bar, as it wouldn't make sense otherwise.

### Draw Mode

Alright. Back to creating our MIDI notes...

Let's make sure we can see what we're doing.
Make sure snaping is enabled and is set to a quarter note grid.
Hit the D key to enter the Draw Mode.

Click to place a note.
Click and drag to place a longer note.
Remember that you can hold down Alt at any time to release yourself from the grid.
So you can for example click and drag, then hit Alt to make the note length not be detemined by the grid.
Again: Shift+Click to delete a note.

In the Draw mode you can't drag to select multiple notes, so I most often use the Edit mode instead, which works a lot like the Draw mode, but lends itself better to editing overall, and not just inserting notes.

### Edit mode

Hit E to enter the Edit mode.

In the Edit mode clicking and/or dragging doesn't create notes - it selects them instead.
To create a note just hold Ctrl, and you'll have exaclty the same behaviour as in the Draw mode.
That's why I prefer to use it for any MIDI region editing.

To move a note click in the middle of it and drag.
If you click and drag on the head or the tail of the note - you can change the length of the note in any direction you want. It also works on multiple notes.

You can select all notes in a given region with the Ctrl+A keyboard shortcut. Just be aware that the Audible MIDI editing feedback may produce a screech if you select a hundred notes at once, as it'll play them all.

You can transpose the selected notes up and down by a semitone using the up/down arrow keys.
If you hold Shift or Alt while doing so, you'll transpose the notes in octave intervals.

### Editing velocity

As you know - MIDI note velocity is stored as a 7-bit number and it can hold values between 0 and 127. In Ardour the default note velocity is 64 - right in the middle.
There's multiple ways to change that value.
Using a lollipop graph is sadly *not* one of them. I know - that sucks. But not all is lost, as you'll see in a moment. You can still do some solid MIDI velocity manipulation in Ardour.

First - select a bunch of notes.

- Ctrl + Up/Down Arrows will change the velocity of selected notes by 10.
- Ctrl + Alt + Up/Down Arrows will do the same in intervals of 1.

- Using the mouse wheel you can also change the velocity of selected notes. On it's own it works in increments of 1. If you Hold Alt and use the mouse wheel - it'll go in the increments of 10.

- You can also hit the V hotkey (V fot Velocity) and type in a numeric MIDI velocity value between 0 and 127.

#### Velocity Ramps

There's two ways to create a note velocity ramp in Ardour. I'll show you one now and you'll learn the other one later in this video.

To create a velocity ramp, you need to put extremes first then fill in the rest - Ardour will interpolate the velocity of the notes to create a ramp.

Let's create a new region in the Draw mode.
Now let's insert two notes - at the start and at the end.
Next - I'll select the first one and hit V, then type 1 and press Enter.
Now I'll change the velocity of the final note - hit V, type 127 and press Enter again.

You can see that as I move my mouse between the two notes the "Phantom Note" that I can insert changes velocity depending on it's relative distance to the existing two notes.

Let's fill in the gaps!

Now we have a linear velocity ramp. let's play it.

I could tweak the velocities of the notes as I'm filling the note series, to affect the ramp's shape. 
Let's undo and try again - I'll first insert a note in the middle and make it quieter by holding Alt and using my mouse wheel on it. I'll also make the first note a bit louder. let's fill in the empty spaces and listen.

That's the first way of creating a MIDI velocity ramp, the other one involves using the powerful MIDI Transform tool which I'll cover in a moment.

But before that let's talk about

### MIDI Channels

[ bring up the HipHop beat region and reset all the MIDI channels to 1 ]

In Ardour each note in a MIDI region can play on a different MIDI channel. As you probably know MIDI supports 16 channels. This is useful if you want to sequence complex parts with different instruments all in a single MIDI track, so you can easily control relationships between them.

If I hover my mouse over a note you can see that Ardour shows us the MIDI Channel number and the note velocity.

[ play the region ]

This is a special MIDI region I've prapared that won't sound right until we change some MIDI channels.

- select notes
- hit "C" and select channel

Right now there's no way to know which note plays on which MIDI channel without checking them individually by hovering your mouse over them. But we can change that!

Right click on the track header and select _Color Mode > Channel Colors_.

Now we can visually distinguish different voices of our part!

As you can hear this MIDI region plays a simple HipHop beat for us.
How does it work?

The General MIDI Synthesizer plug-in has 16 channels and by default each is assigned a different General MIDI instrument.

Let's see what happens if I change the note velocities. Let's hit Ctrl+A to select all notes, hold Alt and use the mouse wheel. As you can see the note velocity is indicated by a thin inner bar of each note, but also by the note's transparency. So even when the _Color Mode_ of the MIDI track is set to _Channel Colors_, we can still visually identify note velocities!

Let's select all and reset the velocity to 100.

### MIDI Buses and MIDI Channels

Now - having all of these instruments on a single track means we can't mix them properly. So let's split them into 3 separate MIDI Buses that'll still be driven from this single MIDI Track.

Let's create 3 MIDI buses

Let's rename them to Paino... I mean: Piano, Drums and Bass.
Let's also rename our conductor MIDI track to HipHop Beat so we can identify it easily.

Now I'm going to route the MIDI signal from the Track that's going to be driving everything to the new buses.

Let's select the first MIDI Bus and click on the Input button.
Our Hiphop Beat track is not here. but if we cut the Instrument Plug-in out the track's port layout has changed and it only outputs a MIDI signal, so it show on this list for us.

Let's connect it and paste the plug-in we've cut.
Let's repeat that for the other two buses.

It seems to work, but it's strangely loud!
It's because now each bus plays all three instruments at the same time. We haven't used the MIDI Channels to separate the parts yet.

Let's use the MIDI Simple Channel Filter plug-in and insert it on the Piano track.
This plug-in lets us choose which MIDI channel we want and discards everything else.

All we need to do is copy it to the other two buses and pick the right channels.

### Copying plug-in in the Mixer view

Previously we used cut and paste to manage our plug-ins in the editor mixer, but it's even easier to do in the full-blown Mixer view. You can switch to it using the Mixer button on the top toolbar, or using the keyboard shortcut Alt+M.

Now we can simply drag and drop a plug-in from one track to another to copy it.
Let's change the MIDI channels. The drums are channel 10, and the Bass is channel 5.

We can play the timeline using the space bar. If we activate Auto Return we can easily audition this phrase over and over while tweaking the settings in the Mixer view.

BTW - you can detach the Mixer view into a separate window if you've got a dual-monitor setup. Just right click on the Mixer button and choose Detach.

Now - let's replace this bass with a synthesizer.
Let's add a new plug-in and select Helm.

Ardour will identify that it's another instrument plug-in and will ask us if we want to replace the existing one or add this new one and have them both. I want to replace the previous one.

Let's play our timeline and hear how that bass is sounding.
Let me tweak the patch a little.

Ok, this should be enough, I recommend you install the x42 MIDI Filter plug-in pack that'll help you manipulate your MIDI data - it's kind of essential, they are open-source and completely free for Linux, Mac and Windows. There's much more in that pack than I've shown you but it's a topic for another video.

[ https://x42-plugins.com/x42/x42-midifilter ]

### Operations on MIDI regions

The fastest way to rename a MIDI region is to Ctrl+Right click on it. Then you can type a new name right away.

If you select a single MIDI region and right click, you'll see a context menu option with the name of the region right on the top.
Then there's MIDI submenu and all the MIDI region operations are there.
"Transpose" let's you offset the pitch of all notes by semitones or octaves.
"Insert *Patch* Change can insert a MIDI bank/program change message. You may want this if you're driving hardware MIDI synthesizers from Ardour.
"Quantize" will let you snap note starts and ends to grid. Very useful for tightening up a sloppy performance.
"Legatize" from the musical term "legato" will extend notes to close all gaps, and shorten notes to avoid any overlap.
"Remove Overlap" does the same thing as Legatize, but it only shortens notes, and never extends them.
"Transform" is a very powerful tool that'll let you do all kinds of crazy math and other operations on MIDI note data. I've dedicated a whole chapter to it and we'll get to it in a while.
"Unlink from other copies" - if the MIDI region is linked, this option lets you make it unique. Thought if you followed my recommendation at the start of this video, you'll never have to use this.
And the last one: "List Editor" - this gives you all notes in a table, where you can directly change all of their properties and audition notes.
Note that the "Sound Selected MIDI notes" button present here is linked to the preferences setting I've told you to alter in the beginning of this video. If you disable this, it's going to be off globally.

### Operations on MIDI notes

We'll go one level deeper now and explore the things that can be done on individual notes or groups of them - that means they are accessible in the Edit or Draw modes.

Let's switch to the Edit mode by hitting the E key.

Let's select a note and right click for a context menu.

Of course we can delete the notes, but I'd recommend using the Delete key or Shift+Right click instead as it's faster.

If you select a single note you can open the Note Edit dialog to directly change the MIDI note Channel, pitch, velocity, start position and length. I think this dialog was supposed to work with multiple notes selected, but it doesn't right now.

Let's now select a bunch of notes so we havemor options available. As you can see the rest of these are exactly the same as on the Region level. So I guess it's time to finally talk about the MIDI Transform.

### MIDI transform

This dialog lets us take some numbers describing MIDI notes, and transform them or even translate them into other properties.
I usually use this to manipulate note velocities, but there's much more that can be done here.

Let's prepare a test region and take a look.
[ make a series of 16th notes 1 bar long ]

Let's open the MIDI transform dialog window.

We can make our note velocities random - _a random number from_
Or - as I mentioned before - create a velocity ramp: _equal steps from_

We can also do math.

If we add another operator we can make a ramp and add randomization to it at the same time.

We can also do multiplication, division and modulus here - I'm not sure how practical this is, but if you figure out a cool trick - let us all know in the comments! 

Now - by selecting groups of notes and using the "equal steps from" operator we can create a bunch of velocity ramps pretty quickly.

[ Proceed to create a dual velocity ramp ]

### Splitting MIDI regions

Now, one of the more important operations in editing is cutting. You can cut MIDI regions just like audio regions.
The short tutorial is - use the S key to split on the Edit Point. The Edit Point is what you pick in the dropdown menu on the far left, next to the Edit Mode of the toolbar. By default it's set to the Mouse cursor position, but you can also cut on the playhead or a selected marker if you want.
To split a region:
- Enable the Grab Mode using the G key
- Click on the region you want to cut to select it
- Hover over your mouse in the spot where you want to split, and hit the S key.

Remember that splitting obeys grid snapping. So if your grid is coarse, you don't need to be as precise with your mouse. If it's fine or disabled though - you may want to zoom in before cutting. You can see what the snapping would do as Ardour draws a blue vertical line to indicate the edit point under the mouse cursor. Watch as that point is snapping to grid and breaking loose with distance as I move my mouse over the timeline.

You can also use the Cut Mode - available on the toolbar, or with the C hotkey. In this mode splitting is done simply by clicking with your left mouse button, and the splits are done under the mouse cursor, regardless of what the Edit Point is set to.

Now - say you want to cut multiple MIDI regions at once in the same place. Select all of them and cut - all selected regions will be split if they intersected with your cutting position.

If you want to cut all MIDI regions on all tracks, you can hit Ctrl+A to select all and proceed to do your cut - the regions outside of your cutting point will not be affected.

### Trimming MIDI regions

Another useful technique is trimming. In short - using the J and K hotkeys, you can quickly move selected region's start or end points while keeping the region contents in place. This is probalby a bit more useful for Audio Regions, but there's no reason to not use trimming on MIDI data.

Make sure the Edit Point is set to Mouse Cursor - now select a few regions and hit J, move the mouse cursor to the right and hit K.

When used with a single region this is like a shortcut to clicking and dragging the region bounds - gives you the same effect, only faster.
With multiple regions - clicking and dragging will move the region bounds independently in relation to their original positions, while J and K would make all selected region bounds snap into one place, most likely overlapping if they're on the same track.

There's some more trimming options available in the main menu under Region > Trim.

### Joining MIDI regions

We can join MIDI regions together - just like the audio regions - using the Consolidate Range function.

First switch to the range mode - now click and drag to select the range encapsulating everything you want to join together, right click to summon the context menu and select "Consolidate Range". 

This will create a new MIDI file on disk that's a combination of our previous ones.
Ardour will ask us to give this region a name, and it'll default to the Track's name. You cna just hit enter to dismiss this dialog.

### Cropping MIDI regions

Another cool thing we can do with the range tool is crop.
Let's select a smaller range this time, then right click again to open the context menu - and select "Crop region to range". Now - because we can't tell Ardour what regions we want to crop, as we can't have regions selected in the Range mode - it'll crop all regions touching the selected range. So you might need to clean up some residue afterwards.

### Copying MIDI regions

Another basic operation is copying regions around.

This can be done in many different ways.

Since we're using the Range tool already, let's talk about what it can do for us.

With a range selected, we can right click and select "Duplicate range" - this'll spawn an exact copy of our selected range head to tail with what we had selected.
The shortcut for this operation is Alt+D. You can hit it a few times to get more duplicates, as it cleverly shifts our selection to the copy, so we can keep doing this.

Another way to duplicate a range is with the Shift+D shortcut. This will show a Duplicate dialog, where you can type in the number of duplicates you want. With fractions.
This mass duplication however will keep your selection in place and I think that's reasonable.

Last but not least - we can cut, copy and paste selected ranges.

The usual Ctrl+C, Ctrl+V and Ctrl+X shortcuts apply. Pasting a range will put it's start at the edit point. Again - this will usually be the mouse cursor position, but it can be other things if you so choose.

In the Grab Mode you can copy a region simply by holding Ctrl and dragging it.
This also works on MIDI notes.
BTW - if you drag with the middle mouse button instead of the left mouse button - Ardour will move the region vertically. That's great for moving regions between tracks without messing up the timing. You can also use this to drag a MIDI region down into empty space to create a new MIDI track if you wnat to mult a MIDI part.

### Deleting MIDI regions

Since you know how to copy MIDI regions, you may want to know how to delete them too.

- You can menu dive and waste a lot of time, or:
- Use the Delete key, or even better:
- Shift+Right Click

Shift + Right Click will delete a region, a MIDI note, a marker or an automation point. It's really fast if you have a single object to delete.
It'll even delete a plug-in in the processor box. But there's no undo for that one for some reason.

PHUCK

It won't delete a track though, and I think that's good.

### MIDI automation vs regular automation

[ load Void project to demonstrate the following ]

Now this is a bit tangential, as it's not directly related to manipulating MIDI data, but if you're gonna use automation for synthesizers and effects on your MIDI tracks - you might need to copy and paste some automation from time to time.

In Ardour there's two different ways to store automation data - one is the "usual way" - that's stored in the main session project file (.ardour) that covers all the fader, panning, mute, and plug-in automation.

The second type is MIDI automation - this includes pitch bends, mod wheel, arbitrary MIDI CC automation and any extra MIDI events like program changes etc.

The big difference is - MIDI automation is bound to a MIDI region, and stored in the individual MIDI files on disk - so when you move or duplicate a MIDI region - the MIDI automation follows.
But - if you have any of the plug-in automation present in that track - it'll stay behind.

There is an option for regular automation to follow audio regions around - you can find this in Edit/Preferences/Editor/Editor Behaviour/"Move relevant automation when audio regions are moved". But there's no option for automation to follow MIDI regions around. I requested this back in 2017 BTW https://tracker.ardour.org/view.php?id=7490

So the solution I found is to use the Range tool to cut, copy and paste MIDI regions along with any other automation that would normally not follow the MIDI regions.

Let's copy a MIDI region along with related automation.

Range tool - click and drag, Ctrl+click the automation lanes you need. Ctrl+C, put your mouse where you want to paste. Ctrl+V.
Done.

Now let's scale this up a bit.

### Restructuring your song

Let's say you want to shuffle around sections of your song or just copy and paste a section. I believe The Range tool is the only way to do this without pulling your hair out.
So make sure you're in the range mode.

First let's make sure we can see as much vertically as possible - Click on this dropdown that changes the number of tracks visible at once and select *all*.
With a very big project it might not manage to squeeze it all in the view, but this already makes it much easier to see what's going on.

Now let's hit Ctrl+T to select all tracks.
Note that this has conveniently **omitted** all the automation lanes, so we need to manually add them to the selection.

Hold Ctrl and click on each automation lane header you need. I'm sorry, there's no short way of doing this that I know of. Yes. I've reported this issue back in 2018 https://tracker.ardour.org/view.php?id=7684

Once you have everything selected, be careful not to misclick or we'll have to do this all over again.
We'll cut the selection - hit Ctrl-X. Please note that with a lot of content selected this can take a while, so just wait and let Ardour chew on that rock until it's all sand. Ok, the selection has disappeared, now let's find a cozy place on our timeline to paste that temporarily.
Again - this might take a while.

Now - the good thing about the range selection tool is that you can move the start and end point of the selection window - so we don't need to re-select our tracks and automation lanes.

### Interting and Removing Time

While we're at the topic of restructuring your song, I'll jsut point that you can insert empty space at any point in your project.

1. Move the playhead to where you want to add a new song section.
2. Hit Ctrl+T to select all tracks (don't care about the automation lanes, they'll follow)
3. From main menu select Track > Insert Time

Here our playhead position is automatically set to the place the time will be inserted at.
What I usually do here is right click on the "Time to insert" number field and change the format to Bars:Beats.
Now click on the filed and type in the number of bars you want. Say: 16, now I'll add zeros until the umber 16 is in the leftmost section. The sections are Bars|Beats|Ticks.

You can choose what should happen to regions intersecting the insertion point. Usually I'd split them and fix any problems afterwards.
Now there's a bunch of options underneath that'll filter what objects should be affected. For this sue-case I think it's safest to select all.

Hit Intsert Time and giveArdour a second.

Voilà! Remove Time works exactly the same way, though it will obviously delete anything in it's way so it's a bit simpler.

[ back to the simple MIDI project ]

### Stretching MIDI regions

The timestretch tool works on MIDI regions as well as on audio regions. Select the region or regions you want to timestretch, then click and drag to set the new length. All the notes inside will be stretched to fill the new length. Timestretching obeys the grid snapping


### MIDI automation

We've discussed the differences between MIDI and regular autmation in regard to movin and copying data around, now let's take a closer look at what we can do wiht MIDI automation in Ardour.

#### Bender automation

One of the most basic types of MIDI automation is pitch bend automation, called Bender.

Unfortunately using this is not exactly a pleasant experience. Let me show you why.

Bender starts in the neutral position which is... 8192. WHAT? Ok. You see - the MIDI pitchbend automation is stored as a 14-bit digital number. Which means it can have values between 0 and 16384. 8192 is right in the middle being the neutral position. Unfortunately Ardour doesn't do anything to make this any easier on the users and just exposes the raw MIDI data and says "deal with it". It's fine if all you're ever going to do is capure and play back your performances, but editing this manually... can bite my shiny metal...

BTW - I've reported the issues with Bender automation back in 2017:
https://tracker.ardour.org/view.php?id=7294

Allright. So how do I use the Bender automation? A big problem here is that there's no easy way to know how many semitones you're pitching stuff up or down. You could go down and get your synth's Pitch Bend depth and calculate what magical number in this thing will correspond to 4 semitones, but - isn't that eactly what computers are supposed to do? Like - compute stuff so we can focus on the interesting bits? This is why if I'm in a need to do a bunch of precise pitch slides I'd rather going to use portamento and automate it's slide time instead. If I only need a couple of simple pitch bends, I will set the pitch bend range to 1 or 2 semitones in my synth and then ramp between full, zero or netrual Bender positions so there's not way I go out of tune. Ti gets out of tune anyway. I often also set the synth bender range to 24 semitones and just use this for special effects wiht no regard to tune or scale. It can be useful for expressive vibrato effects, but you need to reset every other automation point manually to 8192, and Ardoru doesn't snap that or even give you a guide line to aid in that process. More often I use plug-in automation to modulate a pitch LFO depth for a vibrato effect as it takes way less time to do and is more consistent.

What doesn't help is also the fact that when I edit automation in Ardour, it has this bad habit of selecting and moving two points at once when I only want to move one, which forces me to constantly Undo and retry a single move over and over liek a crazy person until it somehow finally works as expected.

Ardour has an option to ignore the vertcial position of the click when you insert a new automation point - it never worked for Bender automation until very recently - so enable that now and thank me later.

To make things worse - Bender automation seems to sometimes ignore the first automation point you place in a region, so that if you've made a bend somewhere - the bendr position will naturally remain out of balance and yo hae ot manually bring it back to 8192. So you insert a point in the next region before any note is player to reset it. But that sometimes doesn't play back and you'll have your notes pitch bent, so you need to add another point to make sure it does reset correctly. Also sometimes makin atoo steep ramp will not play properly.

Honestly working with Bender automation in Ardour is like trying to shave yourself with a shuriken - you'll cut yourself 5 times, but then it'll work.
Automation is not great in Ardour. But with some stamina and clever tricks you can get it to do you bidding. Avoid Bender if you can though - it's the worst.
I hope Ardour 7 will bring us some improvements in this dev-forsaken workflow.

##### Discreet Vs Linear Automation

MIDI Automation lanes have two modes available - Linear interpolated and Discrete. Linear ramps between points in straigt lines, Discreet on the other hand creates a straistep pattern. I've found that this is used by default when recording a MIDI performance with pitch bend.

#### MIDI CC

Now - a bit more intersting is the non-standard MIDI CC automation. These fields are filled in by the instrument plug-in used.
For the General MIDI Synth stock plug-in they look like this.

But if you're working with a hardware synthesizer, Ardour comes with a large set of presets that'll give you appropriate MIDI CC names so you can send MIDI CC automation of the right parameters without looking up spec. sheets. Just select the vendor and the model from the dropdown menu. The default is "Plug-in provided" which is what you'd want for virtual instruments.

I will omit the Pressure and Polyphonic Pressure automations because honeslty I have never used them or needed them and I don't even know what they are for.

If you'd like to learn more about automation in Ardour, I've given a live presentation about this on Sonoj Convention 2018 - hit the card to see the video:
https://youtu.be/PHoT0a2xGlw

### Automatic MIDI Input

A new and very useful feature in Ardour 6 is that it can automatically route a MIDI keyboard controller... or a dance pad... to the currently selected MIDI track.
I think this really improves Ardour's MIDI workflow, because you no longer have to manually assign your MIDI keyboard to a track input you want to record onto or just preview the instrument sound you're tweaking.

To use this featue, let's go to Edit > Preferences > MIDI

Here in MIDI Port Options we havea checkbox saying "MIDI input follows MIDI track selection". This is on by default, and that's good.

Now take a look at the MIDI Inputs tabel. You'll find here all the available MIDI data sources that Ardour detected. becasue of my recording setup there's a buch of plug-in present here, but normally it'll just be the hardware MIDI devices and the Virtual Keyboard.

I'll scroll down, and you can see there's my MID keyboarad - Oxygen 49 and Virtual Keyboard.
The Virtual Keyboard we've talked about earlier has all of that enabled by default, which I think is great.
Let's now tick the Music Data and Follow Selection boxes for the MIDI keyboard and test this.

It's working!
Now I can play and record on any MIDI track simply by selecting it. No more need to manually reassign the inputs all the time.
Remember that if you'll ever want disable this function - that the last created connection will remain active, and you may want to remove it manually after the fact.

Now - one problem automatic MIDI input routing may cause, is that if you hit some notes and select a different track before releasing them - the notes will play forever. So I think it's a good opportunity to mention...

### MIDI Panic

MIDI Panic is a function that'll stop all currently playing MIDI notes.
You can trigger it by hitting the buton with an exclamaition mark on the left edge of the transport controls panel or - using the Ctrl+Tilde keyboard shortcut.

## Generic MIDI Control Surfaces

# Recording automation with a MIDI controller

It's possible to assign MIDI CC inputs to various controls in Ardour's interface.
What that allows us to do is control faders, buttons, and automatable plug-in parameters with physical sliders or knobs on a MIDI controller.
There's also other control surface protocols, but I'm going to only cover the MIDI part in this video.

This could be used for recording fader or plug-in automation or for live performances - though due to the fact that this feature is a bit underdeveloped - I would rather recommend using Carla for such things.

## Enabling the Generic MIDI Control surface protocol

To get this to work, let's go to Edit > Preferences and fist - select Control Surfaces from the list.

Enable the Generic MIDI protocol by clicking the checkbox, then double click on the protocol name to open it's Settings. You can also use the button below the list.

Here we have two lists where we need to select our MIDI device. I'll select my MIDI keyboard for Incoming MIDI. Now - unless your device has motorized faders or some other form of feedback, there's no point in sending it output from Ardour. If it does though - you should select it in Outgoing MIDI, and enable feedback and motorized checkboxes. With proper hardware and this stuff enabled, Ardour should send control change feedback to the device so it can update it's physical state to reflect Ardour's state at all times. I have never tested this, so let me know if you do.

Underneath there's MIDI Bindings dropdown which lists presets for a bunch of MIDI controllers. This is great, because it'll let you use stuff like transport controls without hassle. There's M-audio Oxygen 49 listed there and even though my models is mark IV, this setting does the job and once I set my keyboard in Auto Mode, I can use the transport buttons to drive Ardour. Neat!

If your device has transport controls but is not on the list - I think you need to contact the developrs, as I wasn't able to map my tranport buttons manually.

## Disabling "Smoothing"

A very important setting is Smoothing - I recommend you set this to the maximum value of 127, as this function will give you trouble otherwise if you keep it on the default value of 10 or anything lower than maximum.

The feature name is not very useful - as it doesn't really smooth anything, it's not an interpolation of input. What I think it should be called is "Smooth Takeover" (or at least that's what a similar function in Mixxx is called) as it's a change threshold - if the current physical control position is further from your software control position than this value, the movements you perform will be ignored. So you need to get your physical control's position close enough to the software control in Ardour for you knob twisting to have any effect. And if you move your physical control too fast - creating discreete value changes bigger than this threshold - the control will fail to follow you, which is really annoying.

I think this is meant to avoid volume spikes if you control mixer faders or gain, but I think in the current state it's more trouble than help really.

The MIDI CC uses 7-bit values just liek the MIDI note velocity - giving a range between 0 and 127, that's why setting "Smoothing" to 127 will effectively disable this feature - making the threshold always accept user input. Even if you instantenously move the fader from minimum to maximum, Ardour will not ignore it. If you don't want to record automation or you plan to only do very slow movements. I think this feature would make sense used with pagination, but I don't know of Ardour supporting that in itself.

## Assigning controls

Let's map some controls, shall we?

First - a fader. Hold Ctrl and Middle Mouse Click on a fader in Ardour's UI - because we have a Control Surface protocol enabled, Ardour shows a simple dialog prompting us to move a MIDI control to assign it. I'll move a fader now - and you can see the two have been bound together.

You can try this with buttons too, but I didn't have and luck trying to map mine Ardour behaves like it got the mapping, but it doens't work.
If you want to cancel your MIDI control learning - just click with your mouse on this dialog, and it'll go away.
If you want to remove an assignment - trigger MIDI Learn again, and simply abort it - the control will no longer respond to your MIDI controller.

Ok, now let's assign a plug-in parameter. To do that, we first need to expose it in an automation lane. Let's use Helm's filter cutoff.
Let's now assign the control. Again: Ctrl+Middle Mouse Button, and I'll move a knob on my MIDI controller.
Now I can set the automation mode to Write and if I play my session, everything here gets overwritten by the current position of my physical fader.
After you stop the transport - Ardour will automatically switch the automation lane to Touch mode - this mode will play contents of the lane, unless you touch the control - in that case it'll overwrite the contents. It's a good thing, as leaving it on Write mode would overwrite all automation wherever you play your timeline. However instead of using the Latch mode I recommend you set it to Play mode instead - this'll make sure you can't overwrite your automation by mistake.

And that's basically it for Ardour CC control. There's no special visual feedback, no global list of assigned controls that you can alter, no saving and loading custom presets - the best you could do is hack the .ardour project file with a text editor I guess if you wnated to get more out of this system. It's better than nothing though, and being able to record your fader riding is a very useful too in a DAW.

## Exporting MIDI data

Exporting MIDI data from Ardour only works for single regions.
To do that, you need to right click on a MIDI region and choose export.
As the regions are internally stored as .mid files, this pretty much just gets you the regon you want, and makes a copy of that file optionally with a changed file name.
Exporting your whole project a MIDI Ithnk woudl require to first combine it into a single region somehow. I guess it could be done, if you'd consolidate all the tracks, give each track a unique MIDI channel, then move them all to a single track layered together, and inally consolidated them all together - you'd have a single MIDI file of your whole project. Would that work? No idea, I haven't tried. But I never really needed that. Usually people ask for stems anyway.

## Importing MIDI data

To import MIDI files, right click on an empty MIDI track and select "Insert Existing Media". You can also just drag and drop a MIDI file onto a MIDI track. or if you drop it below the last track - Ardour will create a new MIDI track for it.


## Audio to MIDI

We're almost done. There's very few things left to talk about.

What's really awesome about Ardour is that it's functionality can be easily extended with Lua scripting language.
Ardour comes with a bunch of scripts out of the box. A few of them are related to MIDI.

In the top right corner there's these 4 grayed out buttons. These are quick script launchers. Click on one of them to select what script should it launch.
I'll select Polyphonic Audio to MIDI. A you can see the button now has a not icon on it.

I've been told this tool works best for piano or guitar recordings, so what I've done is prepared a simple MIDI piano line. We'll bounce it to audio, and then convert the audio back to MIDI.

The signal routing is set up, let's just record onto this audio track. Make sure to leave some silence in the start, or the first ntes may get lost.

Now we have an audio region. To turn it into MIDI, we need to create a MIDI region somewhere that'll hold the resuls of this analysis.
I've prerared an empty MIDI track below for this purpose. Let's draw an empty MIDI region. The MIDI region doensn't need to be aligned with the audio region - the script will do that on it's own.

Now, I'll switch to Grab mode and select both the audio and the empty MIDI region by holding down Ctrl and clicking on each.

Let's click on the script launcher.

And here's our MIDI extracted from the audio! There's a small mistake - the analysis has put an octave note where it wasn't but, the rest is pretty much pot on. I am impressed!

There's other Lua Scripts that can help with MIDI - like one that converts MIDI CC automation to plug-in automation. You can find the Script Manager in Edit > Lua Scripts > Script Manager.

I'll leave these for you to explore later. [weird accent] We wouldn't want that beautiful head of yours exploding from an information overload, would we? [/weird accent]

## Step Entry

I have one more feature that I think no one in the world has every heard about before. Except for the developers of course.
Let me know if you knew about it - becasue that means you're amazing.

Step Entry is an interesting feature for classically-trained musicians. If you right-click on the record button on a MIDI track, you'll get a context menu. If you choose Step Entry, a special MIDI input dialog will appear that'll let you put your notes down using a classical music notation interface.

If you've used software like Musescore, you'll probably feel pretty familiar with this. I'm more of a homebrew noisemaker though, so I'm perplexed.

You can select the note duration, modify it to create triplets, dotted, double or triple dotted notes.
You can also choose the dynamics from piano pianissimo to forte fortissimo. There's also a mode that doesn't advance the input position when you add a note, so you can input chords - layering notes.

On the right you can inspect the exact numbers that the "classical notation interface" will put down, and also alter these numbers, like velocity, note duration value, MIDI channel and more.

The six buttons between sutain and dynamics will also let you insert rests and move the note-typing "cursor" back.

The keys from Z to , (colon) will change the input velocity. And there's some other unlabeled hotkeys here.

Most controls have tooltips, so feel free to explore on your own.

I haven't really used this tool in my work, but it's there and I think some of you might find it very useful.
Also - I've never ever seen anyone mention it before. This is possibly the first time it's been shown on video.
Again - let me know if you've known before, I'm really curious!

## Thanks

That's all!

I'm sure I've missed some things and this video will inevitable slowly become outdated. I may revisit it once Ardour 7 is out, if this gets enough attention. Let's see how it'll go.

For the complete script of this video - check the link in the description.

Thanks for watching, I hope this lengthy video was worth your time.
I also want to thank all the amazing people who support my work financially.
Thanks to you I was able to justify the time spent on writing, researching, reporting bugs, discussing issues with the Ardoru team, testing, recording, editing and all the other work that had to be done to complete this enormous tutorial. I really appreciate every bit of community support I get.
In case you - dear viewer - would like to join the crowdfunding, and help keep this show going - please go to Patreon.com/unfa or Liberapay.com/unfa

Also - feel free to join my community on chat.unfa.xyz, there's a lot of great things happening there, and I'd love to you see you there too :)

Now go - and make some music with Ardour MIDI!

## Outro
