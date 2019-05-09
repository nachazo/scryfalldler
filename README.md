```
----------  THIS IS MOCK-UP DOCUMENTATION ----------------------
--------- THE ACTUAL PROJECT CAN BE FOUND AT -------------------
 ------ https://github.com/nachazo/scryfalldler ----------------
```

<h1 align="center">Scryfalldler</h1>

<p align="center"> A simple fast tool to get Magic: The Gathering card images. </p>

Scryfalldler is a PhP based client automated script for downlaoding and zipping card images based off of the Scryfall API site.

This script is a simply php cli coded. I wanted to practice a bit with php cli scripts and this is what I made. With php we can take advantage of expanded php multi-platform, client executed (not web server, to avoid requests and filesize limitations), easy curl (http download) and zip tools.

For feature requests and bugs use: [Issues](https://github.com/nachazo/scryfalldler/issues)

Don't forget to support [scryfall.com](http://scryfall.com)!

## Features

Fetch cards in bulk  

-   through a text file or Xmage .dck file
-   by set, get 1 of every card in a set
-   through an [official Wizards product page](https://magic.wizards.com/en/products/warofthespark/cards)

Extras  

-   6 options for image size, including Art Crop and Border Crop
    
-   Multiple choices in image types (jpg, png).
    
-   Able to declare which set's art to use for each individual card in text or Xmage .dck files. For cards with multiple images within a set, such as basic lands, you can add a collectors number to identify specifically which one.
    

* * *

## Requirements

2.  **PhP version 5.3 or higher, with curl extensions enabled**
    
    -   _Installing on Windows_
        1.  Download the latest PhP version from the
            
            [windows PhP website](https://windows.php.net/).
            
            -   Copy the file php.ini-development in C:\PHP7\ and rename it to php.ini
            -   Open C:\PHP7\php.ini in a text editor and make the fallowing
                 changes
            -   uncomment `; extension_dir = "ext"` to `extension_dir = "ext"`
            -   uncomment `;extension=curl` to `extension=curl`
        2.  Add PhP to the Windows 10 system path enviornmental variables
            
            -   Control Panel->System and Security->System->
                Advanced system settings->Enviornmental Variables
            -   Under `System Variables` double click on `Path`
            -   Select `New` and type `C:\PHP7`
            -   In a command prompt type `php -v` to ensure it is working.
                 If working, version and copyright information should show up.
3.  **The Scryfalldler client**
    
    -   _Installing on Windows_
        1.  Download the Client from GitHub
            -   Press the green `Clone or Download` button in the upper right,
                 fallowed by `Download Zip`
            -   Extract the archive to your desired location
            -   In a command prompt, change the directory to the scryfalldler
                 folder and type `php scryfalldler` to ensure it is working.
                 You should see a list of commands and brief descriptions.

* * *

## Usage

Jump To: [Examples](#examples)

* * *

`php scryfalldler`

* * *

All scryfalldler functionality begins with (1) a command prompt opened to the directory scryfalldler is in and (2) the above phrase typed into that command prompt.

From there arguments can be added to declare which card names need to be fetched, in what size, and more.

#### Argument Definitions

* * *

A command can have _at most 1_ argument that declares the card images to be downloaded.

<table>
    <tr>
        <th colspan="3">Declare the card images to download</th>
    </tr>
    <tr>
        <th>Arguments<img width=100/></th>
        <th>Notes</th>
    </tr>
    <tr>
        <td> <code>-file [fileName].txt</code> </td>
        <td>Uses a file of name <code>[filename].txt</code> as the list of cards to download. <br /> The text file must fallow the form outlined below in <a href="https://github.com/tenbom/scryfalldler#text-file-format"> Text File Format</a>.</td>
    </tr>
    <tr>
        <td> <code>-set [setAcronym]</code> </td>
        <td>Downloads all cards from a set corresponding to 
        <code>[setAcronym]</code>. <br/> Set names and acronyms can be found in <a href="https://mtg.gamepedia.com/Template:List_of_Magic_sets"> This Table</a>.</td>
    </tr>
    <tr>
        <td> <code>-url [url location]</code> </td>
        <td>Only for wizards official spoilers and recent releases. <br/> <code>-url</code> only downloads images at <code>gatherer</code> image size <br/>
 <code>[url location]</code> should be of the form <br/> 
https://magic.wizards.com/en/products/[set]/cards <br/>
for example <br/> https://magic.wizards.com/en/products/warofthespark/cards 
        </td>
    </tr>
    <tr>
        <td> <code>-gatherer [set name]</code> </td>
        <td>Broken. <br/> Downloads all cards from a given set. <br/>
        Downloads images at only <code>gatherer</code> image size.<br/> 
        <code>[set name]</code> should be of the form 
        <code>"Future Sight"</code>. </td>
    </tr>
</table>

* * *

A command to download card images can have _any number_ of arguments modifying the default values.

<table>
    <tr>
        <th colspan="3">Modify the default values</th>
    </tr>
    <tr>
        <th>Arguments <img width=100/> </th>
        <th>Default</th>
        <th>Notes</th>
    </tr>
    <tr>
        <td> <code>-size [sizeKeyword]</code> </td>
        <td> <code>large</code> </td>
        <td>Declare the size of image to download in a    <code>set</code> or <code>-file</code> command. <br/> <code>-url</code> commands always use <code>gatherer</code> size. <br/>Valid values: <code>small</code>, <code>medium</code>, <code>large</code>, <br/> <code>png</code>, <code>art_crop</code>, and <code>border_crop</code> <br/>  See <a href="https://github.com/tenbom/scryfalldler#size-keyword-details">Size Keyword Details</a>for more information. 
        </td>
    </tr>
    <tr>
        <td> <code>-folder [folder]</code> </td>
        <td> Scryfalldler<br/>Directory </td>
        <td>Downloads the images into a zip file of default name 
        <code>1</code> <br/> and then places it in a folder named 
        <code>[folder]</code> within <br/> the scryfalldler directory
        </td>
    </tr>
    <tr>
        <td> <code>-force [zipName]</code> </td>
        <td> <code>FILE</code> </td>
        <td>Forces the zip file name to be <code>[zipName]</code></td>
    </tr>
    <tr>
        <td> <code>-ext [imgExtension]</code> </td>
        <td> <code>jpg</code> </td>
        <td>Force the extension of each image downloaded to be 
            <code>[imgExtension]</code> <br /> Valid Values: 
            <code>jpg</code> and <code>png</code>
        </td>
    </tr>
    <tr>
        <td> <code>-proxy [proxySite]</code> </td>
        <td> <code>None</code> </td>
        <td>Downloads the images through a proxy. <br /> 
            <code>[proxySite]</code> should be of the form: 
            http://proxy:port
        </td>
    </tr>
    <tr>
        <td> <code>-no-check</code> </td>
        <td> Update <br/> Scryfalldler </td>
        <td> If this argument is added, do not download the latest <br/> 
            version of scryfalldler from GitHub on this execution 
        </td>
    </tr>
</table>

* * *

Special commands

These are solitary commands, they must be used alone after `php scryfalldler`.

<table>
    <tr>
        <th colspan="3">Solitary Arguments</th>
    </tr>
    <tr>
        <th>Arguments</th>
        <th>Notes</th>
    </tr>
    <tr>
        <td> <code> </code> </td>
        <td>No argument returns help information, all the possible arguments 
            and a brief description 
        </td>
    </tr>
    <tr>
        <td> <code>-help</code> </td>
        <td>Returns help information, all the possible arguments and a brief 
            description 
        </td>
    </tr>
    <tr>
        <td> <code>-test</code> </td>
        <td>Returns whether scryfalldler can successfully connect to 
            Scyfall 
        </td>
    </tr>
    <tr>
        <td> <code>-version</code> </td>
        <td> Displays the version of scryfalldler you are running  </td>
    </tr>
    <tr>
        <td> <code>-list</code> </td>
        <td>From Scryfall, lists all available sets for download, their 
            acronyms, and card count.  <br />  The output is fallowed by 
            the option to enter a set acronym to download the entire set 
            at the default `large` image size. <br /> Entering nothing and 
            then pressing `ENTER` ends the process without downloading 
            anything
        </td>
    </tr>
</table>

* * *

### Examples

Return to: [Usage](#usage)

The fallowing are example commands typed into a command prompt pointed at the
 scryfalldler directory.

* * *

`php scryfalldler -file myDeck.txt`

-   Creates a zip file of card images, the amounts and names of each card to
     download are listed in the text file, `myDeck.txt`
    -   The card images are of default size, `large`
    -   The zip file is placed in the default location, the scryfalldler
         directory
    -   The zip file's name is defaulted to `FILE`
    -   The extension on each image in the zip file is defaulted to `jpg`
    -   On this run, by default, scryfalldler checks for and downloads any
         GitHub updates
    -   On this run, by default, scryfalldler will not download through a proxy

`php scryfalldler -file myDeck.txt -size png -folder decks/deck1/archive
 -force Deck1Archive -ext png -no-check`

-   as above except...
    -   The card images are of size `png`
    -   The zip file is placed in the folder
         `.../scryfalldlerDirectory/decks/deck1/archive/`
    -   The zip file's name is changed to `Deck1Archive`
    -   The extension on each image in the zip file is changed to `png`
    -   On this run, scryfalldler will not check for github updates

* * *

`php scryfalldler -set C17`

-   Creates a zip file of cards images, this will contain 1 of each card from
     the set `C17`
    -   The card images are of default size, `large`
    -   The zip file is placed in the default location, the scryfalldler
         directory
    -   The zip file's name is defaulted to `C17`
    -   The extension on each image in the zip file is defaulted to `jpg`
    -   On this run, by default, scryfalldler checks for and downloads any
         GitHub updates
    -   On this run, by default, scryfalldler will not download through a proxy

`php scryfalldler -set C17 -size art_crop -force C17ArtCrop -ext png`

-   As above except...
    -   The zip file's name is changed to `C17ArtCrop`
    -   the card image size is changed to `art_crop`
    -   the extension on each image in the zip file is changed to `.png`

* * *

`php scryfalldler -url https://magic.wizards.com/en/products/dominaria/cards`

-   Creates a zip file of card images from Wizard's web page of `dominaria`
     cards
    -   The card images are of default size, `gatherer`
    -   The zip file is placed in the default location, the scryfalldler
         directory
    -   The zip file's name is defaulted to `WZR`
    -   The extension on each image in the zip file is defaulted to `jpg`
    -   On this run, by default, scryfalldler checks for and downloads any
         GitHub updates
    -   On this run, by default, scryfalldler will not download through a proxy

`php scryfalldler -url https://magic.wizards.com/en/products/dominaria/cards
 -folder cards/dominaria`

-   As above except...
    -   The zip file is placed in the folder
         `.../scryfalldlerDirectory/decks/deck1/archive/`

* * *

`php scryfalldler`

-   returns help information, all the possible arguments and a brief description
    `php scryfalldler -list`
-   in the command window, lists all of the card sets on Scryfall and the number
     of cards in each of those sets.
-   then it asks for a set to name to download all the cards of
    -   no additional arguments can be added
    -   the result is the same as a `php scryfalldler -set <setName>` call
    -   entering no text then pressing `ENTER` ends the process without
         downloading

* * *

### Size Keyword Details

Return to: [Usage](#usage)

**This section further explains the keywords of the argument
 `-size [sizeKeyword]`**

Each keyword will download cards at a particular size and resolution. <br />  

That size does not match actual card size. The image size downloaded is
 typically the size of a whole 8.5 by 11 sheet of paper, or larger. <br />  

So next to the image size information is the `pixels/inch if edited to real
 card size` column which shows the resolution of the card image if image
 editing software is used to adjust the resolution so the card image is the
 size of an actual card. For example, with Paint.Net, if you open the card
 with Paint.Net and then go to `Image->Canvas Size` and change the `Resolution`
 to the appropriate `pixels/inch if edited to real card size` value, it will be
 the size of an actual magic card.

<table>
    <tr>
        <th>Image Size</th>
        <th>Size in Inches</th>
        <th>Pixels/Inch</th>
        <th>Pixels/Inch if edited to real card size</th>
    </tr>
    <tr>
        <td>Real Magic Card</td>
        <td>2.45 by 3.42</td>
        <td> --- </td>
        <td> --- </td>
    </tr>
    <tr>
        <td> <code>small</code> </td>
        <td>2 by 2.83</td>
        <td> 72 </td>
        <td> 60 </td>
    </tr>
    <tr>
        <td> <code>normal</code> </td>
        <td>6.9 by 9.6</td>
        <td> 72 </td>
        <td> 195 </td>
    </tr>
    <tr>
        <td> <code>large</code> </td>
        <td>9.5 by 13</td>
        <td> 72 </td>
        <td> 275 </td>
    </tr>
    <tr>
        <td> <code>png</code> </td>
        <td> 10.3 by 14.4 </td>
        <td> 72 </td>
        <td> 300 </td>
    </tr>
    <tr>
        <td> <code>border_crop<sup>1</sup> </code> </td>
        <td>6.8 by 9.6</td>
        <td> 72 </td>
        <td> 210~ </td>
    </tr>
    <tr>
        <td> <code>art_crop<sup>2</sup> </code> </td>
        <td> --- </td>
        <td> 72 </td>
        <td> 300 </td>
    </tr>
    <tr>
        <td> <code>gatherer<sup>3</sup> </code> </td>
        <td> 2.76 by 3.85 </td>
        <td> 96 </td>
        <td> 108 </td>
    </tr>
</table>

<sub>1 - `border_crop` is a 105% scaled `normal` card image cropped back down
 to roughly `normal` size, removing a large portion of the black border.</sub>
 <sub>2 - `art crop` is only the art of a `png` sized card image. It is
 imprecise and the size varies from card to card.</sub>
 <sub>3 - `gatherer` is the image size downloaded through the `-url`
 argument </sub>

* * *

### Text File Format

Return to: [Usage](#usage)

**This section further explains the file format required by the argument
 `-file <[fileName].txt`**

Text files used to declare the cards to download should have each line in the
 form...

-   `[amount] [card name]`
     For Example
     `1 Rhystic Study`
     `2 Faithless Looting`
     `1 Gitaxian Probe`

There are optional parameters to add after the name, declaring which set to
 get the image from, and for cards with multiple images in a set (like lands)
 which collector number to use.

-   `[amount] [card name]|[setAcronym]#[collectorNumber]`
     For Example
     `1 Island|GK2#132`

Scryfalldler will ignore any entries of an already declared `<card name>`.

-   For Example
     `1 Island|GK2#132`
     `1 Island|GK2#131`
     Scryfalldler will ignore the second entry for Island.

* * *

## Further Information

Return to: [Usage](#usage)

Each command has a shortened, 1 letter, abreviation and short functional
 description. These are built into Scryfalldler and can be found through a
 `php scryfallder` or `php scryfallder -help` command, or found below.

```yaml
Usage:
  php scryfalldler [arguments] 

Arguments: 
  All arguments also accept "--". 
    -h, -help        Shows help (this info). 
    -v, -version    Show version from your downloaded script.
    -l, -list        List avaiable sets for download with codes from Scryfall. 
    -s, -set        Launch download cards operation from the specified set from the site. 
    -z, -size        The size for downloaded images ("image_uris" from Scryfall API).
                        Special value "gatherer" downloads Wizards Gatherer image if avaiable. 
                         Default value: large. 
                         Possible values: small, normal, large, png, art_crop, border_crop, gatherer.  
    -u, -url        Download a set from the Wizards official site URL.
                        Usefull for new spoilers and for tokens pages. 
    -g, -gatherer    Download a set from Wizards Gatherer searched by name. 
    -f, -folder        Destination folder for the zip file (not tested with relative ones). 
    -r, -force        Force zip and inside folder name (for tokens download, for example).
    -d, -debug        With this, script only show messages but not download or create folder. 
    -t, -test        Test your connection with Scryfall. 
    -p, -proxy        Set proxy for connections (format http://proxy:port).
    -n, -no-check    By default, script check for updates each execution (requesting to GitHub).
                        A message will warn you on new versions. You can avoid it with this option.
    -x, -ext        Extension for card images. Instead .jpg (default value) that XMage uses,
                        you could force what will be used, for example "png" 
                         Default value: jpg.
    -i, -file        Optional file location, with cards-per-line for export a concrete group of
                        cards (a deck for example - allows XMage .dck format) like a set.
                        You could specify optionally the set for card edition (card|set) and collector
                        number (card|set#collnum) (for example, for lands). If not, last published
                        edition of the card will be downloaded. 

Site: 
  https://github.com/nachazo/scryfalldler 
```

<p align="center"><img src="https://i.imgur.com/I7QEYF6.gif" 
data-canonical-src="https://i.imgur.com/I7QEYF6.gif" width="500" /></code>

* * *

## Changelog

-   **1.4.1** (15/06/18):
    
    -   Small fix for cards with foil versions causing bad exporting.
-   **1.4** (27/04/18):
    
    -   Added "-g" option for download from Wizards Gatherer without taking
         any info from Scryfall. Doing it searching by set name.
    -   Added "-u" option for download from Wizards official set site card
         page. Empty cards comes from Gatherer. Also tokens, but "unnamed".
         Not works as good as Scryfall, needs some post-renaming, but usefull
         in early launched sets.
-   **1.3.3** (02/04/18):
    
    -   Configured error reporting for avoid showing in output high number of
         warnings and so on. Now only important errors will be shown.
-   **1.3.2** (13/03/18):
    
    -   Improved the new file list option. Now you could specify the set you
         want for the card edition with "card|set" (i.e: Opt|INV) (useful for
         lands also you can use collector number with #, i.e. Forest|bfz#273).
         Also, can read the XMage .dck format.
-   **1.3.1** (12/03/18):
    
    -   Fixed error saving cards with " in the name. Until now, these cards
         doesn't download.
    -   Corrected version naming.
-   **1.3** (12/03/18):
    
    -   Added optional feature for download card images from a file list
         (deck file, for example).
-   **1.2** (12/03/18):
    
    -   Fixed error saving split cards (the cards with "//"). Until now, these
         cards doesn't download.
    -   Fixed error saving cards with ":" and " * " in name. Replaced by blank,
         like XMage does. As strange chars in some systems, until now it caused
         that images with that doesn't download.
    -   Added option (-x, -ext) for force the image extension for the cards.
-   **1.1** (09/02/18):
    
    -   Fixed a relevant bug with basic land naming.
-   **1.0** (10/01/18):
    
    -   Initial release.

* * *

documentation is fallowing [Carwin's Style Guide](https://github.com/carwin/markdown-styleguide)
