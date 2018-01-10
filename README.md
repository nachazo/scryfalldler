# scryfalldler
Simple (fast and *bad* coded) php automated script for download and zip card images using the open [scryfall.com](http://scryfall.com) API site ready for XMage.

This script is a simply php cli coded. I wanted to practice a bit with php cli scripts and this is what I made. This way, we can take advantage of php multi-platform, client executed (not web, to avoid requests and filesize limitations), easy curl (http download) and zip tools.

Use [Issues](https://github.com/nachazo/scryfalldler/issues) for feature request or bugs.

Don't forget to support [scryfall.com](http://scryfall.com).

## How to run
You only need **php** 5.3+ (instaled in your system or uncompressed, for example from [php downloads page](http://php.net/downloads.php) or LAMP folder - note: **no** web server required) with **curl extension enabled**. Normally comes installed and enabled in most lamps or similar. If not, for Debian based GNU/Unix like Ubuntu, you simply can do it with `sudo apt install php-curl`. For Windows, search over there :P

So just execute command and place the zip result in your XMage images folder. For tokens you can drag&drop to TOK.zip file.

Btw, script doesn't need php-zip extension, I'm using built-in phar to compress in zip (one requirement less) and in my tests result size is the same.

Don't forget to test results on XMage "Viewer". There you can see bad or errored named cards. With common Zip filemanagers (like 7Zip or WinRAR) you could just edit the name with it for fix.

### GNU/Unix based
Download the script where you want, for example using:
```
> wget https://raw.githubusercontent.com/nachazo/scryfalldler/master/scryfalldler
```
And then simply run it with the desired options (this is a test command):
```
> php scryfalldler -l
```
This will show a list with the avaiable sets. Bellow you have some example commands.

If you don't have php path configured in file system, you could invoke pointing php binary file, for example using:
```
> /etc/bin/php scryfalldler -l
```

### Windows based
Download the script where you want, for example using Windows PowerShell:
```
> wget https://raw.githubusercontent.com/nachazo/scryfalldler/master/scryfalldler -OutFile scryfalldler
```
And then simply run it with the desired options (this is a test command):
```
> php scryfalldler -l
```
This will show a list with the avaiable sets.

If you don't have php path configured in file system, you could invoke pointing php.exe file, for example using:
```
> C:\myPhpFolder\php scryfalldler -l
```

## Example commands
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
* This will download "Commander 2017" tokens and zip subfolder "C17", you could drag&drop to TOK.zip:
  * `php scryfalldler -set tc17 -r C17`

## Help
Command `php scryfalldler -h` shows:
```yaml
Usage:
  php scryfalldler [arguments] 

Arguments: 
  All arguments also accept "--". 
    -h, -help	Shows help (this info). 
    -l, -list	List avaiable sets for download with codes from Scryfall. 
    -s, -set	Launch download cards operation from the specified set from the site. 
    -z, -size	The size for downloaded images ("image_uris" from Scryfall API).
                Special value "gatherer" downloads Wizards Gatherer image if avaiable. 
                Default value: large. 
                Possible values: small, normal, large, png, art_crop, border_crop, gatherer.  
    -f, -folder	Destination folder for the zip file (not tested with relative ones). 
    -r, -force	Force zip and inside folder name (for tokens download, for example).
    -d, -debug	With this, script only show messages but not download or create folder. 
    -t, -test	Test your connection with Scryfall. 
    -p, -proxy	Set proxy for connections (format http://proxy:port). 

Site: 
  https://github.com/nachazo/scryfalldler 
```
