+++
title = 'What is SFML?'
date = 2024-01-25T16:44:08+01:00
draft = false
tags=["sfml","c++","game"]
summary = "After the boring summary, now for the dumdums like me, its basically something that lets you create graphical applications including everything you would interact with a modern software nowdays. Its primarily used for game development. Its also based on OpenGL, keep that in mind boys. To make an insane AAA game you just include some libraries, write some code and BOOOOM you have a game, thats it, its that easy. Anyways..."
+++

## What is SFML

SFML is short for Simple and Fast Multimedia Library and its an opensource API written in C++. Its main focus is using it with C++ but it does support multiple commonly used programming languages as well. Its designed to be simple and user friendly.The multimedia layer is the layer between you and the hardware SFML is that layer that lets you communicate with your hardware.

After the boring summary, now for the dumdums like me, its basically something that lets you create graphical applications including everything you would interact with a modern software nowdays. Its primarily used for game development. Its also based on OpenGL, keep that in mind boys. To make an insane AAA game you just include some libraries, write some code and BOOOOM you have a game, thats it, its that easy. Anyways...

## Its based on 5 core modules:
- System:
    - this is the core module, every other module is based on this
    - 2D, 3D vector classes, threads etc.

- Window:
    - lets you create app windows
    - collects user inputs such as mouse, keyboardű

- Graphics:
    - contains functionalities related to rendering

- Audio:
    - music theme (long running background musics)
    - sounds

- Network:
    - lets you send data over Lan or the Internet

Your allowed to just include the necessary modules for your current project.

So why SFML? I just wanted to make a simple game using C++ so I looked around how I could achive this, I found SFML and searched for a book. The book I choose is written by the devs of SFML and its called SFML Game Development. Pretty good so far its not only teaching you how SFML works through making a space shooter game (which I will be covering), but also giving you advice on general game programming principles and good practices.

## References
SFML: https://www.sfml-dev.org/
BOOK: https://www.amazon.com/SFML-Game-Development-Jan-Haller/dp/1849696845
