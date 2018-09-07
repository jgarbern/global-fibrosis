# global-fibrosis
Global fibrosis
HOW TO USE GLOBAL FIBROSIS PROGRAM

Installing necessary things on computer 
Currently only works for python 2, which is installed on this computer as part of the Anaconda package
- To check which version of python you have: Open terminal and type python --version 

To run on your own computer, you will need to download Anaconda 2 (not 3!), and the following packages: 
- PIL (python image library)
- xlsxwriter 
- To install these: type (in terminal) condo install [package name]
- Remaining packages are a part of anaconda; if you don't have anaconda you will have to also install numpy and os  

Oh and you will also need FIJI or ImageJ with the bio-formats plugin, to convert the images to JPGs, but you can do this on a separate computer if you want. This computer has FIJI. 

Preparing images:
Images must be JPGs, specifically with the file extension .jpg (there is a line in the code that checks for this and if you have a .jpeg file you can try modifying this)

To convert czi files to jpgs: 
- Designate an "input" folder containing all the files you wish to convert 
- Designate a separate "output" folder where you want the converted files to be saved 
- Open FIJI (or imageJ with bioformats plugin installed)
- Go to Plugins -> Macros -> Run…
- When the window pops up to select a file, select the file JPGMacro.ijm.ijm.ijm 
^ I did not write this macro, rather I edited it from the imaging core's czi -> tiff macro  
- A second window will pop up again in finder, this time asking for the input folder containing the czi files you wish to convert. Select this folder and then click open 
- A third time finder will open a window, now asking for the output folder you wish to save the jpg files into. Find this folder, select and click open.
- The macro will now run and a log will pop up telling you how many "scenes" are in each file - this refers to how many planes of the image were acquired, and each plane will be saved as a jpg 
- After the macro has run, you will have in your output folder a FOLDER for each converted file, containing 2-3 JPGs each representing different "planes" in the original czi file. Pick your favorite jpg that represents each image and move this into yet another folder - your "official jpgs to be analyzed" folder. 
- Once you have a folder containing all the jpgs you want to analyze, move onto running the python program.

Setting up the python program to work with your images: 
- I recommend testing with just one image (the "test image" in this folder) to make sure everything is working properly because it can take a long time to run multiple images. 
- The file is globalfibrosis.py, and it only works in python 2 for now - python 3 has some syntax differences, someone could make a python 3 version if this if they wanted to, though 
- Open this file in any text or code editor - you will need to modify a few things to make the program find your images and run how you want it to: 
	- Change the path variable (first line under imports) to be wherever your jpg-containing folder 	lives, make sure to end this with a '/' character or it will get confused. 
	- By default, the program prints out the calculated "percent fibrosis" to the terminal via the 	command "print percent_fibrosis" which you can comment out if you want, or just leave it in 	and ignore these values that print out to the terminal.
	- When analyzing a bunch of images at once, you can have the program write the file name 	and calculated % fibrosis to an excel file. All of these commands are currently commented out, 	but the .py file tells you where to un-comment things to make it write the excel file. You will also need to specify what you 	want the excel file to be named. 

Running the program for a folder of images: 
- Open terminal and make sure you have all the necessary libraries and correct python version (described above) 
- Make sure program is edited to find your image folder and do what you want it to do (described above) 
- Navigate to the directory: Desktop > Global Fibrosis Program 
- In terminal, enter: python globalfibrosis.py 
- If program is working correctly, this is what will happen:
	- Your default image viewer will open a display of the original image so you can compare to the "analyzed" image
	- After a minute or so (depending on image size and resolution), the "analyzed" image pops up in a separate window in the 	same default image viewer. If everything went well, all of the "background" pixels will be black instead of white and all 	"blue" (aka fibrotic) pixels will be yellow. The rest of the pixels, supposedly corresponding to plain heart tissue, will remain 	the same. In addition, if you cropped out any part of the image resulting in any black space, the previously black space will 	become white. 
	- In the terminal, the program will ask: "OK? (y/n)" - if you compare the images and think that the program did a good job 	picking out what is blue and what is background, enter "y" and the program will write the % fibrosis value to an excel file. If 	you type "n" then the program will write "NO" to your excel file so you can go back and re-analyze that image with a different 	threshold. 
	- There is no way for the program to automatically close the two image 	windows it opens up while running so YOU HAVE TO CLOSE THEM YOURSELF. The program will remind you to do this in the terminal and will not continue analyzing the other images until you have entered "y". 
	- Once the program has finished with all the images, the terminal will stop executing and you can go find your excel file. It 	SHOULD save into your current directory but sometimes it just saves it in a random spot on your computer, so use spotlight 	to find it if you can't. 



 
