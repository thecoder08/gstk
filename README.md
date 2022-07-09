# Graphical Shell Toolkit
This is the toolkit for the compositing graphical shell for my OS. It contains routines for creating and drawing to windows, and accepting user input from the mouse and keyboard.
## Overview
This is a simple application that uses GSTK. It creates a 40 by 30 window, and the window turns red if the left mouse button is down, and white if it is not.
```c
#include "gstk.h"
void init() {
    // create a 40 by 30 window
    unsigned char* windowBuffer = gstkCreateWindow(40, 30);
}
void draw() {
    // get mouse buttons
    unsigned char mouseButtons = gstkGetMouseButtons();
    // if left mouse button down
    if (mouseButtons & 0x4) {
        // draw red rectangle
        gstkDrawRectangle(0, 0, 40, 30, COLOR_RED, windowBuffer);
    }
    else {
        // draw white rectangle
        gstkDrawRectangle(0, 0, 40, 30, COLOR_WHITE, windowBuffer);
    }
}
```
As you can see, the overall structure of a GSTK application is an init function for initialization code, and a draw function for code that runs when its time for the application to draw. The draw function can be split into three parts: input, logic, and output. The input part reads user input from the mouse and keyboard, the logic part processes this input, and the output part draws the graphics to the window.
## Routines
This is a list of routines in the Graphical Shell Toolkit.
- `unsigned char* gstkCreateWindow(int width, int height, char* title)` - Creates a new window with the specified dimensions and title and returns its buffer.
- `unsigned char gstkGetMouseButtons()` - Returns a flag list of pressed mouse buttons.
- `unsigned char gstkGetMouseXPosition()` - Returns the X position of the mouse cursor.
- `unsigned char gstkGetMouseYPosition()` - Returns the Y position of the mouse cursor.
- `unsigned char gstkGetMouseXDelta()` - Returns the X delta/speed of the mouse.
- `unsigned char gstkGetMouseYDelta()` - Returns the Y delta/speed of the mouse.
- `unsigned char gstkGetKeyboardScancode()` - Returns the scancode of the pressed key.
- `void gstkDrawRectangle(int x, int y, int width, int height, unsigned char color, unsigned char* buffer)` - Draws a rectangle at the specified position with the specified dimensions and the specified color to the specified buffer.
- `void gstkDrawCircle(int x, int y, int radius, unsigned char color, unsigned char* buffer)` - Draws a circle at the specified position with the specified radius and the specified color to the specified buffer.
- `void gstkDrawLine(int x1, int y1, int x2, int y2, unsigned char color, unsigned char* buffer)` - Draws a line between the specified positions with the specified color to the specified buffer.
## Colors
There are a few preprocessor definitions of useful color values within the 256 color VGA pallete. They are: red, green, blue, cyan, magenta, yellow, black, and white.
## Internals
The internal render loop for the graphical shell is as follows:
1. Call draw routines for all GSTK applications (handle input and draw to window buffers)
1. Compose all windows onto the framebuffer
1. Draw window frames
1. Draw mouse cursor
1. Repeat