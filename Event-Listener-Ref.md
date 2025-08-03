# Event-Listener-Reference-
Ref doc for events and their associated targets

| Event Category               | Event Names                                  | Typical Event Targets                                                   |
|-----------------------------|----------------------------------------------|-------------------------------------------------------------------------|
| **Loading & Navigation**    | load, beforeunload, unload, hashchange       | `window`, `document`                                                   |
| **Keyboard Events**         | keydown, keyup                                | `Element` (e.g. `<input>`, `<textarea>`), `document`, **`window`**     |
| **Mouse / Pointer / Wheel** | click, dblclick, mousedown, mouseup, pointerdown, wheel, etc. | `Element`, sometimes `document`                                        |
| **Touch / Gestures**        | touchstart, touchmove, pointer events, gesture events | `Element`, `document`                                                 |
| **Form & Focus**            | focus, blur, focusin/out, input, change, submit, reset | `Element` (form controls), `document`, `window`                     |
| **Clipboard**               | copy, cut, paste                              | `Element`, `document`, `window`                                        |
| **Animation & CSS**         | transitionend, animationstart/end/iteration   | `Element`, `document`, `window`                                        |
| **Media Events**            | play, pause, timeupdate, volumechange         | Media elements like `<audio>`, `<video>`                               |
| **Fullscreen & Screen**     | fullscreenchange, fullscreenerror             | `Element`, `document`                                                  |
| **Messaging & Connectivity**| message, online, offline, error               | `window`, `WebSocket`, `Worker`                                       |
| **Misc / Custom**           | custom events (`Event`, `CustomEvent`)       | Any `EventTarget`, including `document`, custom `EventTarget` objects |

