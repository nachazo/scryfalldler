# Scryfalldler

A tool to quickly download Magic: The Gathering card images.   
* Download by...   
  * a list in a text file
  * set
  * spoilers from a URL
* Of Size... 
  * 6 options from the [Scryfall site](http://scryfall.com) (20%, 65%, 90%, or 100% size, 100% size Art-Crop, 100% size Border-Crop)
  * 1 option from [Wizard's Gatherer](https://gatherer.wizards.com/Pages/Default.aspx) (35% size)

## Requirements
1. __PhP version 5.3 or higher, with curl extensions enabled__     
   _Windows Users_   
   Download the latest PhP version from the [windows PhP website](https://windows.php.net/).    
   * Copy the file php.ini-development in C:\PHP7\ and rename it to php.ini   
   * Open C:\PHP7\php.ini in a text editor and make the fallowing changes   
   *   uncomment `; extension_dir = "ext"` to `extension_dir = "ext"`
   *   uncomment `;extension=curl` to `extension=curl`   
   
   Now we must add PhP to the Windows 10 system path enviornmental variables
   * Control Panel->System and Security->System->Advanced system settings->Enviornmental Variables
   * Under `System Variables` double click on `Path`
   * Select `New` and type `C:\PHP7`
   * In a command prompt type `php -v` to ensure it is working
 
2. __The Scryfalldler client__
  _Windows Users_
    Download the Client from GitHub
    * Press the green `Clone or Download` button in the upper right, fallowed by `Download Zip`   
    * Extract the archive to your desired location
  
## Usage
To run Scryfaddler, you must have a command prompt opened to the directory scryfaddler is in.

The base command that all scryfaddler processes are run off of is    
   `php scryfaddler`    
From there you add arguments to that line.

|        Arguments                | Notes |
| ------------------------------| ----- |
| ` `| No argument returns a list of all the possible arguments and a brief description |
| `-1`| Confirms Scryfaddler is working and updates it to the latest version on GitHub |
| `-file <fileName.txt>` | Declares where the images are to come from.  <br /> The text file must fallow the form outlined below|
| `-set <setAcronym>` | Declares where the images are to come from. <br /> Downloads all files from the given set, acronyms correspond to [this table](https://mtg.gamepedia.com/Template:List_of_Magic_sets) |


* Basis for all commands: `C:\<directory> php scryfaddler`
  `directory` is the directory that the scryfaddler file is in
  running this command is the same as adding the argument `-h` or `-help`

### Downloading cards from a set
    php scryfalldler -set <setAbreviation> -size <cardImageSize> -folder /home/user/xmage/myImages -proxy http://myproxy:8888
  
### Downloading cards from a text file
    php scryfalldler -file <fileName.txt> -size <cardImageSize> -folder /home/user/xmage/myImages -proxy http://myproxy:8888
  
Required    
 either    
  * `-set` or `-s`  fallowed by `<setAbreviation>`    
    * the set abreviation corresponds to the official abreviations [found here](https://mtg.gamepedia.com/Template:List_of_Magic_sets).   
      This will download the entire specified set    
  * `-file` or `-f` fallowed by `<fileName.txt>` 
     * the command prompt is in the same directory as the file
     * the file is in the form 
       <amount> <cardName>   
       <amount> <cardName>   
        ....   
     will download an image for each unique name.
  
     
     `-set` or `-s` means the source of the images will be all from a set   
     `<setAbreviation>` is the magic set abreviation        
     `-size` or `z`.  Optional.  Default is `small`.  It declares the resolution to download the card images as.
     `<cardImageSize>` The valid values are: `small`, `medium`, `large`, `png`, `art_crop`, `border_crop`.
  
     
  
 * Downloading cards from a text file
   * Open a command line in the `scryfalldler-master` folder
   * the command is `php scryfalldler -file "fileName.txt" -r archiveName`
     `-file` means the Scryfaddler will be generating cards f

* A simple (fast and probably *bad* coded) php client automated script for download and zip card images using the open [scryfall.com](http://scryfall.com) API site ready for XMage.

This script is a simply php cli coded. I wanted to practice a bit with php cli scripts and this is what I made. With php we can take advantage of expanded php multi-platform, client executed (not web server, to avoid requests and filesize limitations), easy curl (http download) and zip tools.

Use [Issues](https://github.com/nachazo/scryfalldler/issues) for feature request or bugs.

Don't forget to support [scryfall.com](http://scryfall.com).

## How to run
You only need **php** 5.3+ (instaled in your system or uncompressed, for example from [php downloads page](http://php.net/downloads.php) or LAMP folder - note: **no** web server required, noly php) with **curl extension enabled**. Normally comes installed and enabled in most lamps or similar. If not, for Debian based GNU/Unix like Ubuntu, you simply can do it with `sudo apt install php-curl`. For Windows, search over there (could be done just editing two lines in php.ini file) :P

So, just execute command and place resultant zip in your XMage images folder. For tokens you can drag&drop to TOK.zip file.

Btw, script doesn't need php-zip extension, I'm using built-in phar to compress in zip (one requirement less) and in my tests result size is the same (phar bundles with php 5.3+).

Don't forget to test set results on XMage "Viewer". There you can see bad or errored named cards. With common Zip filemanagers (like 7Zip or WinRAR) you could edit the name with it for fix.

### GNU/Unix based
Download the script where you want, for example using:
```cmd
> wget https://raw.githubusercontent.com/nachazo/scryfalldler/master/scryfalldler
```
And then simply run it with the desired options (this is a test command):
```cmd
> php scryfalldler -l
```
This example will show a list with the avaiable sets. Bellow you have some example commands.

If you don't have php path configured in file system, you could invoke pointing php binary file, for example using:
```cmd
> /etc/bin/php scryfalldler -l
```
Also, if you want, you can give execute permissions with `chmod +x scryfalldler` to use without "php" word in the commands, just `scryfalldler` (or depending your system `./scryfalldler`). Depending how you saved the file, maybe you need to convert line endings with `sed -i s/\\r//g scryfalldler`.

### Windows based
Download the script where you want, save the path to a file or, for example, using Windows PowerShell (<kbd>Win</kbd> + <kbd>r</kbd>, then `powershell`):
```cmd
> wget https://raw.githubusercontent.com/nachazo/scryfalldler/master/scryfalldler -OutFile scryfalldler
```
And then simply run the command with the desired options (this is a test command):
```cmd
> php scryfalldler -l
```
This example will show a list with the avaiable sets.

> *Note*: If you see weird symbols instead colors in the console, it's because [a problem with Windows ANSI encoding and php version](https://github.com/symfony/symfony/issues/19520). With lastest versions you will avoid it. Anyways, the image download works aswell :)

If you don't have php path configured in file system, you could invoke pointing binary php.exe file, for example using:
```cmd
> C:\myPhpFolder\php scryfalldler -l
```

## Commands
-g or -gatherer gets the card from https://gatherer.wizards.com at 72 pixels/inch
-h or -help
-v or -version
-s or -set
-z or -size
-u or -url
-f or folder
-r or -force
-d or -debug
-t or -test
-p or -proxy
-n or -no-check
-x or -ext
-i or -file
Of course you can combine parameters, also using short or large reserved words, all listed in "Help" section (or type `php scryfalldler`).
* This will download "Commander 2017" set cards (in large size) and zip to "C17.zip" in base folder:
  * `php scryfalldler -s c17`
* This will download "Commander 2017" set cards and zip to "C17.zip" in specified folder:
  * `php scryfalldler -set c17 -f /home/user/xmage/myImages`
* This will download "Commander 2017" cards art crop image set:
  * `php scryfalldler -set c17 -size art_crop`
* This will download "Commander 2017" set cards behind proxy:
  * `php scryfalldler -s c17 -p http://myproxy:8888`
* This will download "Commander 2017" card images from Wizards Gatherer:
  * `php scryfalldler -s c17 -z gatherer`
* This will download "Commander 2017" tokens and zip into a subfolder named "C17", you could drag&drop to TOK.zip:
  * `php scryfalldler -set tc17 -r C17`
* This will read each line of "My deck file.text" and search in Scryfall for cards, then save that in the script format, in a zip "MYDECKRESULT.zip". Useful for common deck files, for example:
  * `php scryfalldler -file "My deck file.txt" -r MYDECKRESULT`
* This will download "Future Sight" set from Gatherer and generate correctly with "FTS.zip" name:
  * `php scryfalldler -g "Future Sight" -r FTS`
* This will download "Exodus" set from Gatherer:
  * `php scryfalldler -g exodus`
* This will download card images from official Wizards product set images, this case for Dominaria. Missing images would be taken from Gatherer:
  * `php scryfalldler -u https://magic.wizards.com/en/products/dominaria/cards -r DOM`
* This will download token images from official Wizards product images, this case for Dominaria. As it have not names, could be unnamed (you may rename):
  * `php scryfalldler -u https://magic.wizards.com/en/articles/archive/card-preview/tokens-dominaria-2018-04-12 -r TOK`

  
## Changelog

* **1.4.1** (15/06/18):
  * Small fix for cards with foil versions causing bad exporting.
* **1.4** (27/04/18):
  * Added "-g" option for download from Wizards Gatherer without taking any info from Scryfall. Doing it searching by set name.
  * Added "-u" option for download from Wizards official set site card page. Empty cards comes from Gatherer. Also tokens, but "unnamed". Not works as good as Scryfall, needs some post-renaming, but usefull in early launched sets.
* **1.3.3** (02/04/18):
  * Configured error reporting for avoid showing in output high number of warnings and so on. Now only important errors will be shown.
* **1.3.2** (13/03/18):
  * Improved the new file list option. Now you could specify the set you want for the card edition with "card|set" (i.e: Opt|INV) (useful for lands also you can use collector number with #, i.e. Forest|bfz#273). Also, can read the XMage .dck format.
* **1.3.1** (12/03/18):
  * Fixed error saving cards with " in the name. Until now, these cards doesn't download.
  * Corrected version naming.
* **1.3** (12/03/18):
  * Added optional feature for download card images from a file list (deck file, for example).
* **1.2** (12/03/18):
  * Fixed error saving split cards (the cards with "//"). Until now, these cards doesn't download.
  * Fixed error saving cards with ":" and " * " in name. Replaced by blank, like XMage does. As strange chars in some systems, until now it caused that images with that doesn't download.
  * Added option (-x, -ext) for force the image extension for the cards.
* **1.1** (09/02/18):
  * Fixed a relevant bug with basic land naming.
* **1.0** (10/01/18):
  * Initial release.

## Help
Command `php scryfalldler -h` shows:
```yaml
Usage:
  php scryfalldler [arguments] 

Arguments: 
  All arguments also accept "--". 
    -h, -help		Shows help (this info). 
    -v, -version	Show version from your downloaded script.
    -l, -list		List avaiable sets for download with codes from Scryfall. 
    -s, -set		Launch download cards operation from the specified set from the site. 
    -z, -size		The size for downloaded images ("image_uris" from Scryfall API).
                        Special value "gatherer" downloads Wizards Gatherer image if avaiable. 
                         Default value: large. 
                         Possible values: small, normal, large, png, art_crop, border_crop, gatherer.  
    -u, -url		Download a set from the Wizards official site URL.
                        Usefull for new spoilers and for tokens pages. 
    -g, -gatherer	Download a set from Wizards Gatherer searched by name. 
    -f, -folder		Destination folder for the zip file (not tested with relative ones). 
    -r, -force		Force zip and inside folder name (for tokens download, for example).
    -d, -debug		With this, script only show messages but not download or create folder. 
    -t, -test		Test your connection with Scryfall. 
    -p, -proxy		Set proxy for connections (format http://proxy:port).
    -n, -no-check	By default, script check for updates each execution (requesting to GitHub).
                        A message will warn you on new versions. You can avoid it with this option.
    -x, -ext		Extension for card images. Instead .jpg (default value) that XMage uses,
                        you could force what will be used, for example "png" 
                         Default value: jpg.
    -i, -file		Optional file location, with cards-per-line for export a concrete group of
                        cards (a deck for example - allows XMage .dck format) like a set.
                        You could specify optionally the set for card edition (card|set) and collector
                        number (card|set#collnum) (for example, for lands). If not, last published
                        edition of the card will be downloaded. 

Site: 
  https://github.com/nachazo/scryfalldler 
```

<p align="center"><img src="https://i.imgur.com/I7QEYF6.gif" data-canonical-src="https://i.imgur.com/I7QEYF6.gif" width="500" /></p>
