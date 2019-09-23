# Arduino beeper music
Simple monotone music asynchronous decoder for beeper. It plays music in non blocking manner.

The code is minimalistic and can be used in small devices, like ATtiny85. The idea is to simplify note writing and transposing from the real notes.

## Settings and notation guide

Take a look at the Sandstorm notation example array:
```
// |- - - -   - - - -| |- - - -   - - - -|
    8,8,8,8,  2,        0,0,0,0,  0,0,4,
    8,8,8,8,  2,        0,0,0,0,  0,0,0,0,

    8,8,8,8,  2,        8,8,8,8,  2,
    8,8,8,8,  2,        8,8,8,8,  2,

    8,8,8,8,  8,8,8,8,  8,8,8,8,  8,8,8,8,

    2,        2,        0,0,0,0,  0,0,0,0,

    8,8,8,8,  4,8,8,    8,8,8,8,  4,8,8,
    8,8,8,8,  4,8,8,    8,8,8,8,  4,8,8,
    8,8,8,8,  4,8,8,    8,8,8,8,  4,8,8,
    8,8,8,8,  4,8,8,    8,8,8,8,  4,8,8,
    8,8,8,8,  4,8,8,    8,8,8,8,  4,8,8,
    8,8,8,8,  4,8,8,    8,8,8,8,  4,8,8,
    8,8,8,8,  4,8,8,    8,8,8,8,  4,8,8,
    8,8,8,8,  4,8,8,    8,8,8,8,  2,
    2,        0,0,0,0,  0,0,0,0,  0,0,0,0,
    100 // end mark, do not remove
```
There is notes marked as a numbers accordingly:

-	8 = 1/8 note / quaver
-	4 = 1/4 note / crotchet
-	2 = 1/2 note / minim
-	1 = full note / semibreve
- 0 = rest

Settings defines a length of the rest used in the whole array:

`#define REST_LENGTH = 8         // Length of the rest note, 8 = Eighth rest`

- 8 = eighth rest / quaver rest
- 4 = quarter rest / crotchet rest
- 2 = half rest / minim rest
- 1 = full rest / semibreve rest

The length of the rest have to be the same in the whole array. Find the shortest rest you need and use it in the array.

_Time signature_ is not involved in the code, as you define BPM and Note. The rest is just a visual factor.

```
#define TEMPO_NOTE = 4          // 1/4 note (crotchet) BPM
#define BPM 240                 // beats per minute for the tempo note defined above
```

Now we can compare settings and numerical notation with the real notes:

![Note example](github.com/dimamedia/arduino_beeper_music/Notation example.png)

You see in the notes that there the tempo of the 1/4-note is 240 BPM. Also numerical annotation above each note is the same as in the array above.

Controller does not do breaks between beeps. So the code adds them automatically by replacing the ends of each beeping note with the silence with a defined length:

`#define PAUSE_LENGTH 100        // Pause to separate beeps in milliseconds`

Default length of 100ms sound pretty nice and corresponds a key press on the piano. You can change it to suite your preferences. It does not affect on real timing between notes. 

And the last setting you need to set is a beeper pin, where the beeper is connected:

`#define BEEPER_PIN 4            // Beeper's pin on Arduino`


