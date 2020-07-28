# Supercollider Notes

## Basics

### Hello World

```supercollider
"Hello World".postIn;
```
Press Ctrl + Enter to evaluate.

### Server and Language

![](bottomleft.png)

The interpreter is active by default. The server needs to be enabled.

The server makes sounds. The language (or client/interpreter) is used to control the server.

### Starting/Stopping A Server

#### Boot the server

Ctrl + B

### Sine Waves

```supercollider
{SinOSc.ar}.play;
```

### Stopping Sound

Ctrl + .
