---
title: "My ergonomic 40% keyboard layout for German developers"
date: 2021-06-05
draft: true
tags: [
"setup",
"keyboard",
"downloads",
"tutorials"
]
---

## Introduction

I recently bought the ["Atreus" from Keyboardio](https://shop.keyboard.io/products/keyboardio-atreus) after wanting to dive into customizable, ergonomic keyboards for a while.
The folks from Keyboardio even provide their own plug-and-play software called [Chrysalis](https://github.com/keyboardio/Chrysalis) for modifying your layout.
While the software (v.0.8.4) provides some great features already, I wanted even more customization options for my layout to be more suitable for the needs of a German software developer, 
so I downloaded the [Arduino IDE](https://www.arduino.cc/en/software), added the "Kaleidoscope Keyboards" plugin and got to work.
You can read the docs for Kaleidoscope [here](https://kaleidoscope.readthedocs.io/en/latest/). 

What I came up with is a layout on the basis of colemak-DHm that includes easy to access German Umlauts, a more convenient symbol layout,
a num-pad, usable mouse controls, space for function keys, and it even makes common shortcuts easier to access.
If you're not a fan of colemak maybe this blogpost can at least give you some ideas for your own custom layout.

I provide a full copy of my layout at the bottom of this post and will try to keep it up-to-date.

## Why the Atreus?

![Atreus](/atreus.jpg)

It's relatively affordable, it's tiny/portable, it's fully programmable, it's ortholinear and it eliminates wrist rotation by being angled and
therefore it's not such a big deal that it is not split.

When I first looked at ergonomic keyboards I didn't even know of the Atreus' existence. It was only by 
coincidence that I stumbled upon a picture of it when I was just about to give up my search for the
perfect ergonomic keyboard. One thing the moonlander, ergodox, planck, dygma raise and most other keyboards
have in common is that they are really expensive! And that's okay, since manual labor has its price and all
but for me spending 300€+ on a keyboard felt a bit extreme and there were also import taxes to worry about.
So finding this minimalist looking gem was a true calling and I immediately went and ordered one.
When it arrived a few weeks later (and sooner than expected) I had already planned out most of my layout on paper
but now it was finally time to test it out and refine it. Eventually I settled on the layout described below and I'm
very happy with it thus far.

Since the Atreus is so different from your standard keyboard I actually find it easy to switch between layouts.
I can comfortably type 80-90 WPM on most QWERTZ keyboards out there and when I sit at the Atreus my brain
just switches gears and I'm fully into colemak dhm again, typing at a steady pace of around 50 WPM at
the point of writing this article. I still improve everyday and am looking forward to seeing where my
upper limit will be.


## The five layer system

Five layers may sound like a lot, but coming from QWERTZ where having three different characters on the same key is a common occurrence
(Normal, Shift and AltGr), it is actually pretty easy to use.

The layers are the following:

{{< highlight arduino >}}
enum {
    BASE,
    SHIFT,
    SUB,
    SUPER,
    MOUSE
};
{{< /highlight >}}

The BASE layer provides you with your standard alphabetic characters as well as some punctuation and quotation options.

{{< highlight arduino >}}
[BASE] = KEYMAP_STACKED
(
Key_de_Q,           Key_de_W,       Key_de_F,   Key_de_P,  Key_de_B,
Key_de_A,           Key_de_R,       Key_de_S,   Key_de_T,  Key_de_G,
Key_de_Z,           Key_de_X,       Key_de_C,   Key_de_D,  Key_de_V,        Key_de_Backtick,
Key_de_LeftControl, Key_de_LeftGui, Key_de_Tab, MO(SUPER), Key_de_Spacebar, Key_de_Enter,

                  Key_de_J,         Key_de_L, Key_de_U,      Key_de_Y,      Key_de_Quote,
                  Key_de_M,         Key_de_N, Key_de_E,      Key_de_I,      Key_de_O,
    Key_de_Slash, Key_de_K,         Key_de_H, Key_de_Comma,  Key_de_Period, Key_de_Minus,
    MO(SHIFT),    Key_de_Backspace, MO(SUB),  Key_de_Delete, XXX,           Key_de_LeftAlt
),
{{< /highlight >}}

On the SHIFT layer you find the shifted counterparts of these characters. Pretty standard so far. 
As far as modifier-keys go there is nothing special going on. My spacebar is on the left (I'm left-handed)
and since I don't rely heavily on the escape key I put it on the SHIFT layer.

{{< highlight arduino >}}
[SHIFT] = KEYMAP_STACKED
(
LSHIFT(Key_de_Q),      LSHIFT(Key_de_W),       LSHIFT(Key_de_F),   LSHIFT(Key_de_P), LSHIFT(Key_de_B),
LSHIFT(Key_de_A),      LSHIFT(Key_de_R),       LSHIFT(Key_de_S),   LSHIFT(Key_de_T), LSHIFT(Key_de_G),
LSHIFT(Key_de_Z),      LSHIFT(Key_de_X),       LSHIFT(Key_de_C),   LSHIFT(Key_de_D), LSHIFT(Key_de_V),        Key_de_Tick,
LSHIFT(Key_de_Escape), LSHIFT(Key_de_LeftGui), LSHIFT(Key_de_Tab), XXX,              LSHIFT(Key_de_Spacebar), LSHIFT(Key_de_Enter),

                      LSHIFT(Key_de_J),         LSHIFT(Key_de_L), LSHIFT(Key_de_U),  LSHIFT(Key_de_Y), Key_de_DoubleQuote,
                      LSHIFT(Key_de_M),         LSHIFT(Key_de_N), LSHIFT(Key_de_E),  LSHIFT(Key_de_I), LSHIFT(Key_de_O),
    Key_de_Backslash, LSHIFT(Key_de_K),         LSHIFT(Key_de_H), Key_de_Semicolon,  Key_de_Colon,     Key_de_Underscore,
    XXX,              LSHIFT(Key_de_Backspace), XXX,              ___,               ___,              LSHIFT(Key_de_LeftAlt)
),
{{< /highlight >}}
Sidenote: "xxx" is for dead keys, while "___" acts as a transparent key, meaning the key defined one (or multiple) layers below will be executed when pressed.


## The QWERTZ symbols optimized for programming

As you could probably see, when it comes to punctuation I went a non-standard route. What I actually
like about the QWERTZ layout is the use of the bottom right row for punctuation. For me it just makes sense
to group comma ( , ) and semi-colon ( ; ) as well as dot ( . ) and colon ( : ) together. So I left it like that even though I use semi-colons quite a lot.
I feel like it's not a big enough deal to change it, but I will show you a potential solution for this later on.
I use hyphen ( - ) and underscore ( _ ) more than slash ( / ) and questionmark ( ? ), so I also left the German variant for the bottom right-most key.

Looking at the two "inside-keys" of the Atreus I decided to put an inverted symbol grouping on the left, that is backtick ( \` ) shifting into a normal tick ( ´ ).
This order makes it less of a pain for me to do my string-interpolation.
On the ride side we have a slash ( / ) shifting into a back-slash ( \\ ). You will see the pipe ( | ) in a much more "logical" place later on.

Last but not least you have probably noticed that I have my backspace key on the right thumb's resting position.
I tried having it in the upper right but I personally find it a much more useful key for the thumb to press.
Instead I put the single-quote ( ' ) shifting into double quotes ( " ) up there. For typing in English this makes it very easy to 
write things like "we're", "we've" and "it's". This also minimizes pinky-finger movements.

## Grouping characters and other useful things for developers

Next is the SUB layer. Technically it is on top of the SHIFT layer but since the
Atreus comes with a Super-key it felt logical to also add a SUB-layer.
However, if you copy from this layout, you can name it whatever you want.
You activate the layer by pressing the key to the right of where I put my backspace (the key with the keyboardio butterfly icon). It only shifts to the layer, so
be sure to keep your thumb down. Doing a layer lock often resulted in me forgetting I was still on another layer, 
so I don't use layer locks at all. Again, feel free to change things to your liking.


{{< highlight arduino >}}
[SUB] = KEYMAP_STACKED
(
Key_de_ExlamationMark, Key_de_At,        Key_de_Circumflex,  Key_de_Dollar,      Key_de_Percent,
Key_de_Asterisk,       Key_de_LeftParen, Key_de_RightParen,  Key_de_LeftBracket, Key_de_RightBracket,
XXX,                   Key_de_LessThan,  Key_de_GreaterThan, Key_de_LeftCurly,   Key_de_RightCurly,   XXX,
XXX,                   XXX,              XXX,                XXX,                XXX,                 XXX,

         Key_de_Ampersand, Key_de_Pipe, Key_de_Equals, Key_de_QuestionMark, Key_de_Circle,
         XXX,              Key_de_Tilde, Key_de_Euro,   Key_de_Plus,         Key_de_Minus,
    XXX, XXX,              Key_de_Hash,  XXX,           XXX,                 XXX,
    XXX, XXX,              XXX,          XXX,           XXX,                 XXX
),
{{< /highlight >}}

The top left resembles the US-layout for the most part, except the hashtag ( # ) got replaced by
the circumflex ( ^ ) and was put on H.
Going on to the top right you have a logic operator cluster consisting of the ampersand ( & ) the pipe ( | ) and the equals ( = ).
The circle ( ° ) on the pinky is pretty useless, but sometimes you just need to complain about the temperature
(that's not just a German thing, is it?).
Below you have access to a plus ( + ) and minus ( - ) sign as well as the tilde ( ~ ) on N and the euro symbol ( € ) on E,
because that makes them easy to remember.

Going on to the interesting part which is the grouping character cluster on the left side. 
Since you activate this layer with your right thumb you now have the freedom to choose between conveniently placed
parentheses (), brackets [], less than and greater than <> as well as your curly braces {} with your left hand. 

I did not forget the (A)sterisk ( * ). 

If you have the need for even more symbols there is still plenty of space left for you to experiment with.

## Qukeys are where the magic happens (Umlauts + Shortcuts)

You've probably asked yourself many times by now where your beloved "ä, Ä, ö, Ö, ü, Ü and ß" went.
Well, see for yourself:

{{< highlight arduino >}}
//Qukey(layer, key_addr, alternate_key)

//umlaute
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 2),  Key_de_SS),           // s -> ß
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 0),  Key_de_AUml),         // a -> ä
kaleidoscope::plugin::Qukey(SHIFT, KeyAddr(1, 0),  LSHIFT(Key_de_AUml)), // A -> Ä
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 11), Key_de_OUml),         // o -> ö
kaleidoscope::plugin::Qukey(SHIFT, KeyAddr(1, 11), LSHIFT(Key_de_OUml)), // o -> Ö
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 9),  Key_de_UUml),         // u -> ü
kaleidoscope::plugin::Qukey(SHIFT, KeyAddr(0, 9),  LSHIFT(Key_de_UUml)), // U -> Ü
{{< /highlight >}}

A qukey is (as far as I understood it) a reference to quantum computing, because one key can have
multiple states, depending on the situation.
In practice this simply means that you can hold down a key for at least some predefined amount of time
(e.g. 250ms) and therefore trigger the defined qukey action.

When I want to write about how relatively (that's "verhältnismäßig" in German) easy it is to learn this layout I would
type "verhaltnismasig" and hold down my a's for ä's and the second s for ß. It's verhältnismäßig easy. In fact, it is actually
the same way most German's are already used to typing on their smartphones!

And the magic doesn't stop there. Since you can basically execute anything as a qukey, why not use it for
simplifying shortcuts? Holding down C for 250ms executes Ctrl+C and when you want to paste you copied text

just hold down V for ctrl+V. just hold down V for ctrl+V.

{{< highlight arduino >}}
//common special characters
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 0),  Key_de_At),           // q -> @
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 9),  Key_de_Euro),         // e -> €
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 8),  Key_de_Tilde),        // n -> ~

//layer shifts/switches
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 7),  MO(MOUSE)),           // shift to mouse controls

//hold for "ctrl+" version of the key
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 2),  LCTRL(Key_de_C)),     // c copy
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 4),  LCTRL(Key_de_V)),     // v paste
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 1),  LCTRL(Key_de_X)),     // x cut
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 0),  LCTRL(Key_de_Z)),     // z undo
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 10), LCTRL(Key_de_Y)),     // y redo
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 3),  LCTRL(Key_de_F)),     // f find
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 8),  LCTRL(Key_de_L)),     // l select address bar
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 1),  LCTRL(Key_de_R)),     // r reload page
{{< /highlight >}}

Since I promised you a way to more easily acces the semi-colon ( ; ), why not put it on color ( , ) and add a
Qukey action? Or, if you don't like that, how about adding a [tap-dance](https://kaleidoscope.readthedocs.io/en/latest/plugins/Kaleidoscope-TapDance.html) 
key where you execute colon ( , ) on a
single press and when you double press the key it is instead executed as semi-colon ( ; )? The are many
possible ways to modify things to your liking.

## The numpad

Now that we've covered the German alphabet and your most used symbols, we can take a look at the SUPER layer,
because we're still missing some components from your standard full-size keyboard.

{{< highlight arduino >}}
[SUPER] = KEYMAP_STACKED
(
Key_de_Insert,      Key_de_Home,      Key_de_UpArrow,   Key_de_End,        Key_de_PageUp,
Key_de_Delete,      Key_de_LeftArrow, Key_de_DownArrow, Key_de_RightArrow, Key_de_PageDown,
Key_de_PrintScreen, XXX,              Key_de_VolumeUp,  Key_de_VolumeDown, Key_de_Mute,     XXX,
XXX,                XXX,              XXX,              XXX,               XXX,             XXX,

         Key_de_Backspace, Key_7,        Key_8, Key_9,        Key_de_Asterisk,
         XXX,              Key_4,        Key_5, Key_6,        Key_de_Minus,
    XXX, XXX,              Key_1,        Key_2, Key_3,        Key_de_Plus,
    XXX, XXX,              Key_de_Slash, Key_0, Key_de_Comma, Key_de_Enter
),
{{< /highlight >}}

You can access the SUPER layer by pressing (and holding down) the key to the left of the space key.
This layer allows you to use your arrow keys on the right hand (using "FRST", acting like "WASD" does on QWERTZ/QWERTY)
as well as your number keys on the left hand.

I've also added the six keys from the little block that is usually above your arrow keys on a full sized keyboard.
I only really use the delete key (which I've already added to my BASE layer) but if you need them, they are there.

Personally, I've always disliked the number row for typing numbers and always found it easier to just use the numpad instead.
That's why I was very happy too see that it was possible to move my beloved numpad to my right hand, so I won't have to lift my fingers.
The only downside is, that you have to hold down the SUPER key with your left thumb, but that's totally worth it for me.

## Mouse Controls

I'll be honest. I like to use my mouse. Maybe because it's a nice mouse that cost a lot of money or maybe it's because I used to play a lot of [osu!](https://osu.ppy.sh/home)
when I was younger, which drastically improved my mouse precision and speed... but sometimes it would be nice to not have to lift your right hand from the keyboard.
With this layout, you can now do that! Holding down "M" (for "mouse" - but if you don't need your tilde ( ~ ) on N
you can put it there to have it directly on your right pointer finger) you access the MOUSE layer - again by shifting, not toggling -
and this gives you access to some nice functionality.

{{< highlight arduino >}}
[MOUSE] = KEYMAP_STACKED
(
XXX, Key_mouseBtnP, Key_mouseUp, Key_mouseBtnN, XXX,
XXX, Key_mouseL, Key_mouseDn, Key_mouseR, XXX,
XXX, XXX, XXX, XXX, XXX, XXX,
XXX, XXX, XXX, Key_mouseBtnL, Key_mouseScrollUp, Key_mouseScrollL,

         XXX, XXX, XXX, XXX, XXX,
         XXX, XXX, XXX, XXX, XXX,
    XXX, XXX, XXX, XXX, XXX, XXX,
    Key_mouseScrollR, Key_mouseScrollDn, Key_mouseBtnR, XXX, XXX, XXX
)
{{< /highlight >}}

Your thumb now acts as your scroll wheel (vertical and horizontal) as well as your left and right mouse buttons. 
That is honestly the most useful thing about this layer. If you really don't want to lift your fingers you also can move 
your mouse pointer using "FRST" and also navigate back and forth between web-pages using W and P respectively.

In the full file you will see some configuration options for the mouseKeys. I suggest you [read the docs](https://kaleidoscope.readthedocs.io/en/latest/plugins/Kaleidoscope-MouseKeys.html) and change them to your liking.

## Function keys

If you need them simply add them to where there is still some space (I have a few on the SUPER layer already). Or
maybe you want to create a whole new layer or some more qukeys. It's up to you.

I myself will probably add some (like F11) in the future whenever I miss one.

## Where to go from here?

I hope this article gave you some inspiration to go out there and try to find your own perfect little layout.
There is still a lot of optimization to be done and that's honestly the most fun aspect of the whole procedure.
Go out and experiment. Try [tap-dance](https://kaleidoscope.readthedocs.io/en/latest/plugins/Kaleidoscope-TapDance.html)
or defining your own [macros](https://kaleidoscope.readthedocs.io/en/latest/plugins/Kaleidoscope-Macros.html). Read the
damn documentation, and - of course - have a great day!

## Get the file

The full file:

{{< highlight arduino >}}
#ifndef BUILD_INFORMATION
#define BUILD_INFORMATION "locally built"
#endif

#include "Kaleidoscope.h"
//#include "Kaleidoscope-Macros.h"
#include "Kaleidoscope-Qukeys.h"
#include "Kaleidoscope-MouseKeys.h"
/* put the contents in your plugins folder: 
 * https://github.com/keyboardio/Kaleidoscope-Languages */
#include "Kaleidoscope-Languages.h"
#include "kaleidoscope/lang/de-qwertz.h"

#define MO(n) ShiftToLayer(n)
#define TG(n) LockLayer(n)

enum {
BASE,
SHIFT,
SUB,
SUPER,
MOUSE
};

/* *INDENT-OFF* */
KEYMAPS(
[BASE] = KEYMAP_STACKED
(
Key_de_Q,           Key_de_W,       Key_de_F,   Key_de_P,  Key_de_B,
Key_de_A,           Key_de_R,       Key_de_S,   Key_de_T,  Key_de_G,
Key_de_Z,           Key_de_X,       Key_de_C,   Key_de_D,  Key_de_V,        Key_de_Backtick,
Key_de_LeftControl, Key_de_LeftGui, Key_de_Tab, MO(SUPER), Key_de_Spacebar, Key_de_Enter,

                  Key_de_J,         Key_de_L, Key_de_U,      Key_de_Y,      Key_de_Quote,
                  Key_de_M,         Key_de_N, Key_de_E,      Key_de_I,      Key_de_O,
    Key_de_Slash, Key_de_K,         Key_de_H, Key_de_Comma,  Key_de_Period, Key_de_Minus,
    MO(SHIFT),    Key_de_Backspace, MO(SUB),  Key_de_Delete, XXX,           Key_de_LeftAlt
),

[SHIFT] = KEYMAP_STACKED
(
LSHIFT(Key_de_Q),      LSHIFT(Key_de_W),       LSHIFT(Key_de_F),   LSHIFT(Key_de_P), LSHIFT(Key_de_B),
LSHIFT(Key_de_A),      LSHIFT(Key_de_R),       LSHIFT(Key_de_S),   LSHIFT(Key_de_T), LSHIFT(Key_de_G),
LSHIFT(Key_de_Z),      LSHIFT(Key_de_X),       LSHIFT(Key_de_C),   LSHIFT(Key_de_D), LSHIFT(Key_de_V),        Key_de_Tick,
LSHIFT(Key_de_Escape), LSHIFT(Key_de_LeftGui), LSHIFT(Key_de_Tab), XXX,              LSHIFT(Key_de_Spacebar), LSHIFT(Key_de_Enter),

                      LSHIFT(Key_de_J),         LSHIFT(Key_de_L), LSHIFT(Key_de_U),  LSHIFT(Key_de_Y), Key_de_DoubleQuote,
                      LSHIFT(Key_de_M),         LSHIFT(Key_de_N), LSHIFT(Key_de_E),  LSHIFT(Key_de_I), LSHIFT(Key_de_O),
    Key_de_Backslash, LSHIFT(Key_de_K),         LSHIFT(Key_de_H), Key_de_Semicolon,  Key_de_Colon,     Key_de_Underscore,
    XXX,              LSHIFT(Key_de_Backspace), XXX,              ___,               ___,              LSHIFT(Key_de_LeftAlt)
),

[SUB] = KEYMAP_STACKED
(
Key_de_ExlamationMark, Key_de_At,        Key_de_Circumflex,  Key_de_Dollar,      Key_de_Percent,
Key_de_Asterisk,       Key_de_LeftParen, Key_de_RightParen,  Key_de_LeftBracket, Key_de_RightBracket,
XXX,                   Key_de_LessThan,  Key_de_GreaterThan, Key_de_LeftCurly,   Key_de_RightCurly,   XXX,
XXX,                   XXX,              XXX,                XXX,                XXX,                 XXX,

         Key_de_Ampersand, Key_de_Pipe, Key_de_Equals, Key_de_QuestionMark, Key_de_Circle,
         XXX,              Key_de_Tilde, Key_de_Euro,   Key_de_Plus,         Key_de_Minus,
    XXX, XXX,              Key_de_Hash,  XXX,           XXX,                 XXX,
    XXX, XXX,              XXX,          XXX,           XXX,                 XXX
),

[SUPER] = KEYMAP_STACKED
(
Key_de_Insert,      Key_de_Home,      Key_de_UpArrow,   Key_de_End,        Key_de_PageUp,
Key_de_Delete,      Key_de_LeftArrow, Key_de_DownArrow, Key_de_RightArrow, Key_de_PageDown,
Key_de_PrintScreen, XXX,              Key_de_VolumeUp,  Key_de_VolumeDown, Key_de_Mute,     XXX,
XXX,                XXX,              XXX,              XXX,               XXX,             XXX,

         Key_de_Backspace, Key_7,        Key_8, Key_9,        Key_de_Asterisk,
         XXX,              Key_4,        Key_5, Key_6,        Key_de_Minus,
    XXX, XXX,              Key_1,        Key_2, Key_3,        Key_de_Plus,
    XXX, XXX,              Key_de_Slash, Key_0, Key_de_Comma, Key_de_Enter
),

[MOUSE] = KEYMAP_STACKED
(
XXX, Key_mouseBtnP, Key_mouseUp, Key_mouseBtnN, XXX,
XXX, Key_mouseL, Key_mouseDn, Key_mouseR, XXX,
XXX, XXX, XXX, XXX, XXX, XXX,
XXX, XXX, XXX, Key_mouseBtnL, Key_mouseScrollUp, Key_mouseScrollL,

         XXX, XXX, XXX, XXX, XXX,
         XXX, XXX, XXX, XXX, XXX,
    XXX, XXX, XXX, XXX, XXX, XXX,
    Key_mouseScrollR, Key_mouseScrollDn, Key_mouseBtnR, XXX, XXX, XXX
)
)
/* *INDENT-ON* */

KALEIDOSCOPE_INIT_PLUGINS(
Qukeys,
MouseKeys
);

void setup() {
QUKEYS(
//Qukey(layer, key_addr, alternate_key)

//umlaute
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 2),  Key_de_SS),           // s -> ß
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 0),  Key_de_AUml),         // a -> ä
kaleidoscope::plugin::Qukey(SHIFT, KeyAddr(1, 0),  LSHIFT(Key_de_AUml)), // A -> Ä
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 11), Key_de_OUml),         // o -> ö
kaleidoscope::plugin::Qukey(SHIFT, KeyAddr(1, 11), LSHIFT(Key_de_OUml)), // o -> Ö
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 9),  Key_de_UUml),         // u -> ü
kaleidoscope::plugin::Qukey(SHIFT, KeyAddr(0, 9),  LSHIFT(Key_de_UUml)), // U -> Ü

//common special characters
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 0),  Key_de_At),           // q -> @
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 9),  Key_de_Euro),         // e -> €
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 8),  Key_de_Tilde),        // n -> ~

//layer shifts/switches
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 7),  MO(MOUSE)),           // shift to mouse controls

//hold for "ctrl+" version of the key
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 2),  LCTRL(Key_de_C)),     // c copy
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 4),  LCTRL(Key_de_V)),     // v paste
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 1),  LCTRL(Key_de_X)),     // x cut
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(2, 0),  LCTRL(Key_de_Z)),     // z undo
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 10), LCTRL(Key_de_Y)),     // y redo
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 3),  LCTRL(Key_de_F)),     // f find
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(0, 8),  LCTRL(Key_de_L)),     // l select address bar
kaleidoscope::plugin::Qukey(BASE,  KeyAddr(1, 1),  LCTRL(Key_de_R)),     // r reload page
/* suggestions: 
 * p = print
 * s = save or leave ß
 * t = new tab
 * n = new page/browser window/doc or leave ~
 */
)

//Qukey settings
Qukeys.setHoldTimeout(250);
Qukeys.setOverlapThreshold(80);

//MouseKey settings
MouseKeys.speed = 8;
MouseKeys.speedDelay = 0;
MouseKeys.accelSpeed = 0;

Kaleidoscope.setup();
}

void loop() {
Kaleidoscope.loop();
}
{{< /highlight >}}
