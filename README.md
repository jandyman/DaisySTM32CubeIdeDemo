# DaisySTM32CubeIdeDemo

How to create an STM32CubeIde project for Daisy. Example is for Mac OS, but Windows and Linux should be similar.

First, you'll need to get the Daisy project code from GitHub. I just used the DaisyExamples repo that I found there. Before you create the project, you will have to build the libraries libDaisy and DaisySP, so they can be included in the project. There are makefiles for that.

After that, open up STM32CubeIDE and New -> Create New Project from the Project Explorer pane.

![image](Screenshots/NewProject.png)

The Target Selector should open up. For MCU/MPU Selector, type 750 into the search box, then choose STM32H750IB:

<img src="Screenshots/MCU.png" width="250" >

Select the BGA package:

<img src="Screenshots/BGA.png" width="750" >

Next you'll get this pane:

<img src="Screenshots/LastProjectDialog.png" width="450">

If you select "Use default location", the project will be placed in the workspace folder. You can put it where you want. Make sure to select "Empty". At this point you'll have an empty project. There a lot of different ways to organize the project folders, I'll just use the default organization created by the wizard.

From here, the idea is to use the existing makefiles for the Blink example as a guide for filling in the project options, such as include folders and libraries. First, to make the project more portable, I create an STM32CubeIde environment variable to point to the DaisyExamples folder on my computer. In the Project Explorer, select Properties for the project, then select C/C++ Build -> Environment:

<img src="Screenshots/Environment.png" width="700"> 

Create a new variable (I called it DAISY) and point it to your DaisyExamples folder:

<img src="Screenshots/AddVariable.png" width="450"> 

Now we add the include paths found in the makefile to the project. These are in a shared included makefile in libdaisy/core. One example found in the makefile would be $(LIBDAISY_DIR)/src. To add that path, go to Project Properties -> C/C++ General -> Paths and Symbols -> Include Tab -> Add. Make sure to check Add to All Configurations and Add to All Languages

<img src="Screenshots/AddInclude.png" width="700">

Now add all the other include paths found in the makefile into the project.

In a similar manner, we add the Library Paths and Libraries for the libdaisy and DaisySP libraries. The way that GCC works is that you need to add the library paths, you can't just specify a library with a full path. Also you need to remember that GCC prepends "lib" to the library name, so you don't specify the full filename of the library file.

When you are all done, the various paths and libaries will look something like this:

<img src="Screenshots/Includes.png" width="600">

<img src="Screenshots/Libraries.png" width="600">

<img src="Screenshots/LibPaths.png" width="600">


Now all we need to do is copy the contents of the example main file (Blink.cpp) into our project. There are many ways to do this, but the way I did this was to first rename the main.c file created by the wizard to main.cpp so that it will be compiled as a c++ file, and then I just copied the contents of Blink.cpp into main.cpp, replacing the original contents.

At this point I was able to build the project without errors




