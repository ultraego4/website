+++
title = 'Learning SFML through making a space shooter game: Game loop, FPS, events'
date = 2024-01-26T12:20:34+01:00
draft = false
tags=["sfml","c++","game"]
categories=["projects"]
summary= "So in my previous post i went through what SFML is in a nutshell, in this one im gonna talk about some basic game concepts such as game loops, FPS, fixed time step."
+++

So in my previous post i went through what SFML is in a nutshell, in this one im gonna talk about some basic game concepts.

## Game loop

The main loop, often called the game loop is for to process events, update and render things on the screen.

It could look like something like this:

```
while(window.isOpen()){

    processEvents(); #process user inputs

    update(); #update the logic

    render(); #render the game to the screen
}
```


The processEvents function is waiting for some kind of event, key pressed, exit etc. and the render() cleans the screen, draws and then render the things on the screen.

Usually 1 iteration of the main game loop is considered 1 tick or 1 FPS (but FPS more commonly references the rendering time not really the 1 iteration of the game loop).

## Vectors

When making games, vectors are soooo powerful. SFML has a class template for it sf::Vector2. In graphics everyting is float so the sf::Vector2 is instantiated as sf::Vector2<float>.

Vectors are useful for storing 2 points (absolute or relative), direction or flow. Normalizations, unit vectors, vector algebra all that stuff is pretty important, and you will have to get used to it in game making.

```
void Game::update(sf::Time deltaTime){

    sf::Vector2f movement(0.f,0.f);

    if (mIsMovingUp) {
        movement.y -= PlayerSpeed;
    }
    if (mIsMovingDown) {
        movement.y += PlayerSpeed;
    }
    if (mIsMovingLeft) {
        movement.x -= PlayerSpeed;
    }
    if (mIsMovingRight) {
        movement.x += PlayerSpeed;
    }

    mPlayer.move(movement * deltaTime.asSeconds()); // v = s*t
}
```

We are using += because when the player presses 2 opposite keys the player wont move. 

## Fixed time step

At this point in the game loop the update is executing as fast as it can, now if we start the game and move we would fly off the map. Changing the PlayerSpeed wouldnt be enough since the change differs from compute powers to compute powers. We want the speed based on frames, we can you use the classic `v= s*t` where we introduce a delta time, using SFML's Clock and Time class.

Now this approach seems good but has another flaw. Lets say one iteration differs heavily from the previous one, faster or slower, if its faster the delta time would be 3x the delta time and it means the player would move 3x times as much, potencially going through a wall or something.

Now this where fixed time step comes in, it guaranties that the delta time is always the same.

```
void Game::run(){

    sf::Clock clock;
    sf::Time timeSinceLastUpdate = sf::Time::Zero; // intialize to 0

    while (mWindow.isOpen()) {
 
        processEvents();
        timeSinceLastUpdate += clock.restart(); // time elapsed while processEvents() did its thing

        while (timeSinceLastUpdate > TimePerFrame) { // ~0.0166666667
            timeSinceLastUpdate -= TimePerFrame;
            processEvents();
            update(TimePerFrame);
        }
        render();
    }
}
```

If the render is slow, the update could run multiplies times, the game could stutter because not every update is rendered, but the game wont be slow itself.

## Real time rendering

When doing real time rendering we ignore the frame requests, and we continuously blindly draw on the screen as fast as we can. Since our eyes dont really process more than 60FPS or 30FPS we can limit the FPS to that in order to save more processing power.

Double buffering also a thing connected to this, we dont have to check if something happend to stay on the screen from the previous frame. We have a front and back buffer, the front is displayed and in the back we are drawing, preparing the next frame.



## References
Book: https://www.amazon.com/SFML-Game-Development-Jan-Haller/dp/1849696845