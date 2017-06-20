# Wallpaperer

Our project is a program that will accept user created scripts in order to control
desktop wallpapering and general information display. The user will be able to designate
specific sets of wallpapers as well as which monitors those sets will be displayed
on in order to create advanced slideshows.

## Getting Started

### Prerequisites
* Python3
* Antlr4 for Python3
```
See "github.com/antlr/antlr4/blob/master/doc/python-target.md" and "antlr.org" for details
```
* PIL
```
pip install image
```

### Installing
Simply clone the project
```
git clone https://github.com/JacobJinTheAsian/Wallpaperer.git
```

### Writing a script
Overwrite test.txt with your own. Use the following structure:

Sources would be folders that contain an arbitrary number of images.
Set up a SOURCE variable that binds the path of a directory to itself:
~~~~
SOURCE name dirPath;
~~~~

Groups are specific sets of images that would be targeted at specific monitors.
Set up a GROUP variable that binds the path of images to itself:
~~~~
GROUP name:
	1 imagePath1 ## for monitor 1
	2 imagePath2 ## for monitor 2
;
~~~~
The composite image will be built with each image in order of the specified numbers, building the image from left to right.
Monitor 1 then is on the left and monitor 2 is on the right.  If a third image was specified, that would go further right still.



Overlay Text can be used to display information on top of the desktop background.  It executes a bash script and prints the stdout stream to the screen.  The position and justification of the text control where it will appear.
Set up text overlay:
~~~~
## A/B means A or B
OVERLAY TEXT name:
	COMMAND bashScriptPath
	LEFT/RIGHT 50% ## text horizontal location on screen
	TOP/BOTTOM 50% ## text vertical location on screen
	JUSTIFY LEFT/RIGHT ## text justify left or right
;
~~~~

Set up image overlay:
~~~~
## A/B means A or B
OVERLAY IMAGE name:
	path ## the full path of the image
	LEFT/RIGHT 50% ## image horizontal location on screen
	TOP/BOTTOM 50% ## image vertical location on screen
	JUSTIFY LEFT/RIGHT ## image justify left or right
;
~~~~

Wallpaper Slideshows can be defined.  Images will be cycled through for each monitor either alphabetically or randomly.
Set up slideshow:
~~~~
## A/B means A or B
SLIDESHOW name:
	1 sourceA ## takes a SOURCE variable
	2 sourceB ## takes another SOURCE variable
	## Any number of sources can be specified targeting any number of monitors.
	TIME N SECONDS/MINUTES/HOURS ## N can be any positive integer
	ORDER ALPHABETICAL/SHUFFLE; ## display slides based on the file name or randomly
;
~~~~

Some additional notes:
- Each declaration must be terminated in a semicolon ';'
- The script as a whole must also be terminated with a semicolon.
- names must start with a letter and can only include letters and numbers.
- don't try naming two different things the same.  It will explode.
- Paths must be the full path from root.  Relative paths will not work.
- The included test script will need rewriting to account for the above.

Include any combination of the code above in test.txt to create your costume wallpaper, and run the below command in terminal:
~~~~
python3 BackgroundManager.py test.txt ## Will run and query you for a group or slideshow to be displayed.
python3 BackgroundManager.py test.txt GROUPNAME ## Will display the user defined group.
python3 BackgroundManager.py test.txt SLIDESHOWNAME ## Will run the user defined slideshow.

python3 BackgroundManager.py text.txt GROUPNAME/SLIDESHOWNAME False ## will run the group or slideshow without any overlays.
~~~~


## Authors
* Eric Krauss
* Yage (Jacob) Jin

## License:
This project is licensed under the MIT License
