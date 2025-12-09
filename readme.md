# Posh-Photo-Utils

> [!NOTE]
> **Legacy Showcase (2017)**
> I’m keeping this repository public as a snapshot of my scripting work from a few years back.  
> It demonstrates my early approach to writing **clean, modular, efficient, self-documenting code** and careful handling of precious digital assets,  
> all while prioritizing usability for less-technically-inclined users.
> 
> * FWIW - at the time of writing this note section (Late 2025), these scripts are still being actively used, and reported to have saved a lot of time and manual effort.  
 
This project consists of a set of bespoke utilities I've created for a photographer to improve her file management and processing workflows.

Future utilities in this context will be added to this project, as well as improvements / fixes to existing ones.

These utilities are open for everyone to use - but please note that you will be using them under your sole responsibility and at your own discretion.

At this time, they have only been tested on Windows 7 64bit and Windows 10 64bit,
and may work properly only using Powershell version 4.0 or above. 

Please feel free to get in touch if you have any comments, issues, feature-requests etc...

## Utility no. 1: "Cull-CR2Files.ps1"

### The "Why":
The motivation behind this script, derives from the way the photographer preforms her initial filtering after taking numerous photographs:

Each photograph taken is saved (originally to the camera's SD Card, later on - to local disk for processing) in both it's full sized "RAW" file (`.CR2`), and a compressed `.jpg` file.

Initial filtering is much quicker to process by just **previewing** all the lighter-weight `.jpg` files, and deleting all the "bad" images (wrong exposure, out of focus, etc...).  
In the following stop - all corresponding `.CR2` files can be deleted as well - which is what this script was born to do:

Automating this very manual (click-to-select) task of cherry-picking a subset of hundreds of files out of a vast list of thousands,  
it saves a lot of time, human-error and frustration.

### The "How":
This script looks for all existing RAW camera files (`.CR2`) and all `.jpg` files in a given directory 
(Selected by the user upon running the script using a Windows Folder Browser Dialog).

Any raw (`.CR2`) files witnout a corresponding `.jpg` file-name match in this directory, enters a "candidate for deletion" list.

Next, the user can go over the list and either approve / disapprove each file manually, or the whole list altogether.

Finally, the script will delete all files "approved for deletion" by the user.

![alt tag](/../master/Cull-CR2Files/ScreenShots/DialogBox.PNG?raw=true  "Screenshot #1: Windows Folder Browser Dialog")

![alt tag](/../master/Cull-CR2Files/ScreenShots/ApproveList.PNG?raw=true  "Screenshot #2: list of files pending approval")


## Utility no. 2: "Copy-ToBestFolder.ps1"

### The "Why":
In the later process of "final" filtering, a selection of "top/best" photos is carefully curated into a `Best.txt` file.  
The files listed in it are then copied over to a `Best` subdirectory, which, again is a highly time consuming task - involving _manually_ looking for specific filenames within a folder of hundres (or more), click-to-select each of them to highlight for the copy action.

This is where the `Best.txt` artifact of the process comes in handy, 
and I've built this script to take that list of files as an input, and use it to automate the selection/copy tasks.

### The "How":
This script looks for a `Best.txt` list of file names in the selected folder, creates a folder named `Best` and copies all corrsponding CR2 files to the "Best" folder.

* User should supply a list of file names to copy in a .txt file named `Best.txt`:
   - Naming convention should just be the file's unique ID, so for example a file named `IMG_0181.CR2` should only be listed as `181`.
   - The `Best.txt` file should reside in the same directory as the _source_ folder (Where files are to be copied from)
   - `Best` folder will be created inside the selected _source_ folder, and the listed files will be copied to it.

* The copy is performed using [RoboCopy.exe](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy), with a (currently hardcoded) default of 16 multiple threads, to allow for a relatively fast parallel copy without heavily taxing the computer's resources.

![alt tag](/../master/Copy-ToBestFolder/ScreenShots/Dialog.PNG?raw=true  "Screenshot #1: Windows Folder Browser Dialog")

![alt tag](/../master/Copy-ToBestFolder/ScreenShots/CopySummary.PNG?raw=true "Screenshot #2: summary of copied files")
