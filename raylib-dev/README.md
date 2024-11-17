Install instructions:

1. Replace email/name with yours in the Dockerfile
2. Replace the .bashrc, .bash_aliases and .vimrc with your own, or remove those lines from the Dockerfile.
3. Run the command `docker build -t raylib-dev-environment .` <-this will take a while
4. Run the command `docker run -it --name raylib-dev-container c-dev-environment`
5. in the projects folder, make a file, `main.cpp`
6. copy/paste the following template

#include <raylib.h>

int main() {
    // Initialize the window
    InitWindow(1400, 800, "Raylib Game");

    // Main game loop
    while (!WindowShouldClose()) {
        // Update game state

        // Draw everything
        BeginDrawing();
        ClearBackground(RAYWHITE);
        DrawText("Hello, World!", 10, 10, 20, DARKGRAY);
        EndDrawing();
        if (IsKeyPressed(KEY_ESCAPE))
                break;
    }

    // Close the window
    CloseWindow();
    return 0;
}
                                                        
7. save it
8. From here, run the command `g++ main.cpp -o my_program -L/usr/local/lib/libraylib.a -lraylib -lGL -lGLU  -lm -lpthread -ldl -lrt -lX11`. I plan on either including all these in a makefile or making a g++ alias, this is ridiculous. 
9. if you get an error like this:

Authorization required, but no authorization protocol specified
WARNING: GLFW: Error: 65550 Description: X11: Failed to open display :0
WARNING: GLFW: Failed to initialize GLFW
Segmentation fault (core dumped)

open up a terminal on your local machine, type `xhost +local:docker` to give docker permission to engage with X11, then try again

10. if you get an error about not finding a .h file or the commands not being recognized, then the library is not linking to your file. In the compilation command, replace `-L/usr/local/lib/libraylib.a` with whatever location your libraylib.a file is (it should still be in the path somewhere).





#docker build -t raylib-dev-environment .
#docker run -it --name raylib-dev-container c-dev-environment
#g++ main.cpp -o my_program -L/usr/local/lib/libraylib.a -lraylib -lGL -lGLU  -lm -lpthread -ldl -lrt -lX11

