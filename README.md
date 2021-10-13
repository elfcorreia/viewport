# Framebuffer Library

This library was designed for educational purposes in such a way that:

* Enables C/C++ programming students works with graphics as early as possible
* Provides a framebuffer abstraction
* Provides multiple implementations to embrace any student's software resources
* Easier compilation and linkage

## Quick start
    
    fb_viewport(320, 240, "");
    int buffer[320][240];
    fb_buffer(buffer, 320, 240);
    buffer[100][50] = 0x0f0ff0;
    fb_sync(buffer);
    fb_finish();

## Operations

- `void fb_viewport(int viewport_width, int viewport_height, const char* options);`
  
  Initialize and prepares the viewport.

- `void fb_buffer(void* data, int pixels_width, int pixels_height);`
  
  Register a new buffer memory pointed by `data` of `width` and `height` pixels.

- `fb_sync(void* data);`
  
  Writes the buffer `data` to the internals buffers.

- `fb_finish();`
  
  Finalize the viewport.

## Details

### Framebuffer abstraction

The framebuffer abstraction consist of a piece of memory (buffer) to store pixels that will be render on a graphical device. This graphical device is platform dependent. So can be an X11 Window in a Linux, an OpenGL context, an Window in Windows.

### Pixels and colors

Each pixel color is represented by an RGB value in an `int`. Is easy to think in colors using hexadecimal literals, like HTML colors:

    int red = 0xff0000;
    int green = 0x00ff00;
    int blue = 0x0000ff;

### Viewport size and buffer size

A Viewport is an area where the buffer will be rendered. In many situations, to render an buffer of 320 by 240 in a viewport of 320 by 240 is trivial. However, you can too render an buffer of 9x9 pixels in a viewport of 100x100. In such situation there is a upsampling. 

Downsampling is not available.

### Buffers

The argument `data` can be:

- a pointer to a unidimensional array: `int screen[32*32];`
- a pointer to a bidimensional array: `int screen[32][32];`
- a pointer to a heap allocated memory: `int* screen = new int[32*32];`
- etc...      

and can be passed by: `fb_buffer(screen, 32, 32);`

### Erro handling

On errors a panic function is called. It's prints a message and terminates the program with a call for `exit(1)`.

### Global state

This library have only one, statically and globaly viewport because this is not an window library.
