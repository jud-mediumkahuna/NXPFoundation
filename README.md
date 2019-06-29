# NXPFoundation
This is the common, foundation, software for Free Scale now NXP MCUs used on Teensys and Frogs
Its mostly some configuation of vendor/open software including (especially) FreeRTOS (now AmazonRTOS)
We mostly add trying to standardize configuration and application programming. 
The basic configration is two channel, one cable communication with an immediate host. 
The two channels are a bydirectional packet serial stream (serial port) and a file system (flash drive).

Executable memory is divided into three files: 
1) The RTOS and drivers, extentions, etc (that don't change often, we pray).
2) The startup program/shell.
3) The application.

Typically, only the application is changing and getting downloaded all the time.
I'm praying/assuming that application executable images are relocatable.
The start up program starts after the rtos comes up and configures itself. It looks for new files that are new versions of the three excutable files. If it's the op sys or the startup, it copies (flashes) them over the existing and deletes the new files. If there's a new application program, it deletes the old one, makes sure the new one is contiguous, renames it, and sets a pointer to the new application file.
Once the files are ok the startup program starts a task which then calls the application.
The startup program is a hook in the idle task (effectively if, I don't accually implement it that way).
If the startup program can't do what it wants or the application quits then, it becomes a shell/CLI/debug monitor or resets.

We're starting with the NXP SDK including AmazonRTOS and, for lack of a better idea, we will be Eclipsed (if you don't know what that means, you're blessed).

Drivers have at least two levels: basic communication with the Perp (peripheral) and simulating it in high fidelity. At least the basic part is considered part of the operating system (in the first executable file).

We plan to use the Workflow and Router model/method of application programming with fairly rigorous guidelines/standards for Application Workflows, Workflows and Steps. We're going to work on router guidelines but, not as persnickety as workflows.
