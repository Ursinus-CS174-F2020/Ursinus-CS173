---
layout: assignment
permalink: /Assignments/MIDI
title: "CS173: Intro to Computer Science - MIDI Audio"
excerpt: "CS173: Intro to Computer Science - MIDI Audio"

info:
  coursenum: CS173
  githubclassroom:
    joinlink: https://classroom.github.com/classrooms/61290261-billmongan-cs173-fall20
    clonelink: false
  points: 100
  goals:
    - To implement functions to facilitate code re-use
    - To invoke functions that may accept parameters
  rubric:
    - weight: 60
      description: Algorithm Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 30
      description: Code Quality and Documentation
      preemerging: Code commenting and structure are absent, or code structure departs significantly from best practice, and/or the code departs significantly from the style guide
      beginning: Code commenting and structure is limited in ways that reduce the readability of the program, and/or there are minor departures from the style guide
      progressing: Code documentation is present that re-states the explicit code definitions, and/or code is written that mostly adheres to the style guide
      proficient: Code is documented at non-trivial points in a manner that enhances the readability of the program, and code is written according to the style guide
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup)
      progressing: The program is submitted according to the directions with a minor omission or correction needed
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution

tags:
  - functions
  
---

The [Musical Instrument Digital Interface (MIDI)](https://en.wikipedia.org/wiki/MIDI) standard enables your computer to play synthesizer music that you can control programmatically.

## Adding the MIDI library to your project

To use this jar, after creating a Gradle Java project in Netbeans, add the following line inside the `dependencies` section of your `build.gradle` file:

```
compile fileTree(dir: 'libs', include: '*.jar')
```

If you do not have a dependencies section, you can add one as follows:

```
dependencies {
    compile fileTree(dir: 'libs', include: '*.jar')
}
```

Now, jar files added to the libs directory of your project will be available for use in your code.  Download and copy the [MIDILib.jar]({{ site.baseurl }}/files/asmt-midi/MIDILib.jar) file into a subdirectory of your project called `libs`.  See the [Javadoc]({{ site.baseurl }}/files/asmt-midi/javadocdoc/index.html) for more information about the library \[[^1], [^2], [^3], [^4], [^5], [^6]\].

[^1]: [http://math.hws.edu/eck/cs124/f17/lab8/lab8-files/midi/SimpleSynth.java](http://math.hws.edu/eck/cs124/f17/lab8/lab8-files/midi/SimpleSynth.java)
[^2]: [https://www.inspiredacoustics.com/en/MIDI_note_numbers_and_center_frequencies](https://www.inspiredacoustics.com/en/MIDI_note_numbers_and_center_frequencies)
[^3]: [https://www.geeksforgeeks.org/java-midi/](https://www.geeksforgeeks.org/java-midi/)
[^4]: [http://www.cs.albany.edu/~sdc/CSI201/Spr12/201Stuff/bookClassesJavaFiles/MidiPlayer.java](http://www.cs.albany.edu/~sdc/CSI201/Spr12/201Stuff/bookClassesJavaFiles/MidiPlayer.java)
[^5]: [https://stackoverflow.com/questions/2064066/does-java-have-built-in-libraries-for-audio-synthesis/2065693#2065693](https://stackoverflow.com/questions/2064066/does-java-have-built-in-libraries-for-audio-synthesis/2065693#2065693)
[^6]: [https://stackoverflow.com/questions/22467633/java-midi-player-program](https://stackoverflow.com/questions/22467633/java-midi-player-program)

## Instantiating a MIDIPlayer object

The MIDI library you imported includes a `MIDIPlayer` class that you can instantiate to help you play sounds through your computer.  You can create one like you would any object variable, with the `new` keyword:

```java 
MIDIPlayer player = new MIDIPlayer();
```

Open the [Javadoc]({{ site.baseurl }}/files/asmt-midi/javadocdoc/index.html) to find out about the method interface this library provides.  There are a number of methods you can call inside the `MIDIPlayer` class.  What are a few of them, and, in your own words, what do they do?

In addition, there are two classes `Instruments` and `Notes` which contain constants that represent some of the instruments, notes, and note durations that you can play.  These include `Notes.NOTE_C4` for a C4 note, `Instruments.GUITAR` for a guitar, and `Notes.NOTE_QUARTER` which specifies a quarter note duration.  Click on the `Instruments` and `Notes` javadoc classes and make a note of some of the instruments and notes that are available to you.  Because it's a synthesizer, some of the "instruments" are actually creative sound effects - feel free to have fun with this!

Javadoc documentation is really helpful because it enables you to observe functionality made available by a library "at a glance."  You can see how methods are named, information about how they are invoked, and what parameters they require.  These are generated programmatically through comments that you write throughout your code, and this is prescribed by the [Style Guide]({{ site.baseurl }}/Style-Guide).

## Part 1: Playing a Note

Let's test the interface and the computer sound setup by playing a note using a synthesized instrument.  The MIDI interface works by defining a number of "channels" on which you can play notes, chords, and sounds.  You can think of a channel as a particular instrument.  In fact, you can assign an instrument to a channel.  The default channel is "channel 0," but you can have several more of them, referenced by number.

To do this, you can first set an instrument on the default channel by calling the following method of the `MIDIPlayer` library:

`player.setInstrument(Instruments.HARP);`

Here, `Instruments.HARP` is the instrument that you want to use.  This will assign the harp to the default channel 0.  To play a note, you can call the following function:

`player.playNote(Notes.NOTE_C4, Notes.NOTE_QUARTER, Notes.DEFAULT_INTENSITY);`

This will play a C4 quarter note, using a default intensity value.

Try it and verify that you get sound output.  Try changing this to play an A4 whole note at half intensity.  The A4 note is a higher pitched note, and this is because A4 is a higher frequency vibration which your ear perceives as a higher pitch.  In fact, A4 is defined here as 440 Hz, and, consequently, C4 (known as "middle C") is ~262 Hz. Every note is defined by its own fundamental frequency.

## Part 2: Playing a Song

Using the playNote function, try playing the first part of the "alphabet song," (actually, it's basically [Twinkle Twinkle Little Star](https://en.wikipedia.org/wiki/Twinkle,_Twinkle,_Little_Star)) which plays the following quarter notes: `C4 C4 G4 G4 A4 A4 G4`.

Now, try adding the second part: `F4 F4 E4 E4 D4 D4 D4 D4 C4`.  Note that there are more notes in this part than the first: to align the time, the D4 notes should be eighth notes instead of quarter notes.

There should have been a brief pause between the first part (`C4 C4 G4 G4 A4 A4 G4`) and the second part (`F4 F4 E4 E4 D4 D4 D4 D4 C4`).  The following function call will introduce a "rest" or pause (in this case, equivalent to an eighth note duration) in between the parts:

`MIDIPlayer.rest(Notes.NOTE_EIGHTH);`

Try inserting this in between the parts.

Finish the alphabet song.  Here are the notes, which are quarter notes unless otherwise specified (I suggest adding an eighth note duration rest in between each part):

```
C4 C4 G4 G4 A4 A4 G4(whole)
F4 F4 E4 E4 D4(1/8th) D4(1/8th) D4(1/8th) D4(1/8th) C4(whole)
G4 G4 F4 (rest 1/16th) E4 E4 D4(whole)
G4(1/8th) G4(1/8th) G4(1/8th) F4 (rest 1/16th) E4 E4 D4(whole)
C4 C4 G4 G4 A4 A4 G4(whole)
F4 F4 E4 E4 D4 D4 C4(whole)
```

For fun, try changing the instrument to a guitar before playing the song: 

`player.setInstrument(Instruments.GUITAR);`

Compare the result to [Twinkle Twinkle Little Star](https://en.wikipedia.org/wiki/Twinkle,_Twinkle,_Little_Star) (there is a MIDI rendition on the Wikipedia page that you can play!).  There are a few small differences to make the alphabet fit into the song - can you spot them?  What would you change in your program to match [Twinkle Twinkle Little Star](https://en.wikipedia.org/wiki/Twinkle,_Twinkle,_Little_Star)?

## Part 3: Using Functions to Enable Code Re-Use and Repitition

Did you notice that part of the song repeats?  The first part is exactly the same as the fifth part!  You can avoid having to do this extra work of copying and pasting your code using functions.  In addition to saving you some typing, functions a standard good practice in case it becomes necessary to change that part of the song in a way that affects every use of the part.  With a function, you can change the song once, and have it play correctly both times that you use it.

Define a function `playMainPart()` that contains the code to play the `C4 C4 G4 G4 A4 A4 G4` part, and modify your program so that you call this function each of the two times you want to play that part in the song.

When we explore arrays and loops, we will see how we can represent a song like this using a single variable (an "array") that represents the entire collection of notes, and this can be played using a single call to the function to play all the notes.  "Loops" can iterate over these collections, one by one, and automatically play each note, so that you don't have to copy your code like you did here.