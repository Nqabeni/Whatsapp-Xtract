WhatsApp Xtract v2.2
- WhatsApp Backup Messages Extractor for Android and iPhone

Released on November 17th, 2012
(C)opyright 2012 Fabio Sangiacomo <fabio.sangiacomo@digital-forensics.it>
(C)opyright 2012 Martina Weidner  <martina.weidner@freenet.ch>
Released under MIT licence

Tested with Whatsapp (Android) 2.8.5732
Tested with Whatsapp (iPhone)  2.5.1

Last Update on November 17th, 2012 (v2.2)

------------------------

HOW TO USE:
(see also the thread at xda-dev: http://forum.xda-developers.com/showthread.php?p=24603294 )

1. You need to copy the whatsapp database. 

On Android, either get this file:

/sdcard/WhatsApp/Databases/msgstore.db.crypt
(crypted database on SD card, can be created by starting backup from whatsapp advanced settings: settings - more - Backup Chats)

or these files:
/data/data/com.whatsapp/databases/msgstore.db and wa.db
(for this you need root access. detailed instructions in the bottom of this file. the advantage is that the corresponding contact names of phone numbers will be displayed.)

On IPhone, get this file:

net.whatsapp.WhatsApp/Documents/ChatStorage.sqlite
(You can use an Iphone Backup Tool to get the file, e.g. I-Twin or Iphone Backup Extractor. Make sure to create an unencrypted backup with Itunes, as these tools can't handle encrypted backups. Another possibility are forensic tools like UFED Physical Analyzer.)

2. Extract this archive (Whatsapp_Xtract....zip) to a certain folder on your computer, e.g. C:\WhatsApp.

3. Copy the database(s) to e.g. C:\WhatsApp (on Android, you simply copy the whole folder WhatsApp on SD card to your computer e.g. to C:\WhatsApp and then copy the database file from C:\WhatsApp\Databases to C:\WhatsApp)

4. You need Python and (for Android msgstore.db.crypt decryption) the PyCrypto library

The easiest way is to install ActivePython (on Windows choose 32bit version even if you have 64bit windows): 
http://www.activestate.com/activepython/downloads

and then run !install pyCrypto.bat (contained in this archive. The best is to rightclick on it and choose "run as administrator".)

5. Now run whatsapp_xtract_android.bat or whatsapp_xtract_android_crypted.bat or whatsapp_xtract_iphone.bat 

OR simply drag and drop the database file(s) to whatsapp_xtract_drag'n'drop_database(s)_here.bat

OR run whatsapp_xtract_console.bat and then manually specify the input file with one of these commands:

COMMAND LINE OPTIONS:

For Android DB:
python whatsapp_xtract.py msgstore.db -w wa.db
OR (if wa.db is unavailable)
python whatsapp_xtract.py msgstore.db
OR (for crypted db)
python whatsapp_xtract.py msgstore.db.crypt

For iPhone DB: (-w option is ignored)
python whatsapp_xtract.py ChatStorage.sqlite

Once finished, your browser will open and show the chats. 

The resulting file size of the .html file will be slightly bigger than the size of the .db database. 

------------------------

RECENT BUGSFIXES:
- none

CHANGELOG:

v2.2 (updated by Martina Weidner - Nov 17, 2012)
- now supports new emoji smileys
- (Android Version) hotfix for TypeError in b64encode
- (Android Version) decoded file won't be deleted even if it can't be opened

v2.1 (updated by Fabio Sangiacomo and Martina Weidner - May 7th, 2012)
- improved install pyCrypto.bat
- added easy drag and drop possibility with whatsapp_xtract_drag'n'drop_database(s)_here.bat
- (Android Version) added support to fix corrupted android whatsapp database (needs sqlite3, for windows sqlite3.exe is contained in the archive)
- (Android Version) removed wrong extraction of owner in android version
- (Iphone Version) information from Z_METADATA table will be printed to shell
- (Iphone Version) fixed bug in support of older Iphone whatsapp databases
v2.1-bugsfixed-4:
- fixed .bat files again to support script execution from each external directory
- fixed .bat files if error "python" not found occurs (if you get that error, run install pyCrypto.bat first; rightclick on it and choose "run as administrator")
- updated compatibility for newer android whatsapp versions to show media files with thumbnails correctly

V2.0 (updated by Fabio Sangiacomo and Martina Weidner - Apr 28, 2012)
- supports WhatsApp DBs coming from both Android and iPhone platforms
- (Android Version) wa.db is optional
- (Android Version) now also crypted msgstore.db.crypt from the SD card can be imported
- chat list is sorted by the last sent message
- fixed some bugs (e.g. that the script didn't work with python 3)

V1.3 (updated by Martina Weidner - Apr 17, 2012)
- corrected linking of offline files (now linking according to media file size)

V1.2 (updated by Martina Weidner - Apr 5, 2012)
- media files also linked to offline files
- corrected hyperlinks

V1.1 (updated by Martina Weidner - Apr 5, 2012)
- changed database structure, Android only
- show contact names
- show smileys
- show images
- link / popup for images, video, audio, gps
- clickable links

V1.0 (created by Fabio Sangiacomo - Dec 10, 2011)
- first release, iPhone only:
  it takes in input the file "ChatStorage.sqlite",
  extracts chat sessions and the bare text 
- sortable js allows table sorting to make chat sessions easily readable

------------------------

Some Additional Information


SQLITE Editor

You also can open the "msgstore.db" and "wa.db" using SQLite Database Browser ( http://sqlitebrowser.sourceforge.net/ ). 
However it is much more confusing and the messages are ordered by date, not by conversations. Also you won't see the smileys and media files...

~

MEDIA FILES

If you want to watch the videos, audios and images, you can click on the thumbnails and media links. Popups should open displaying the media. 
However, online media files are available only for the last ~ 3 weeks. 
But you still can open the offline media files, they are linked as well. 
For this it is necessary to copy the folder "Media" from /sdcard/Whatsapp (Android) or net.whatsapp.WhatsApp (Iphone) to the certain folder of your computer where this tool is installed.

~

ROOT ACCESS TO UNENCRYPTED WHATSAPP DATABASE (Android version only)

If you want to have the contact names displayed and not only phone numbers, then (Android version only) you need the file wa.db from the internal storage. 

For that you need to get access to the folder 
/data/data/com.whatsapp/databases
For that you need root access.
For rooting, the tool Superoneclick Root might be useful:
http://forum.xda-developers.com/showthread.php?t=803682

Then you can copy the files "msgstore.db" and "wa.db" to your computer by

- using the App RootExplorer (first copy to SD, then mount phone to computer)
- or using adb: open cmd and type "adb pull /data/data/com.whatsapp/databases/msgstore.db C:\Whatsapp" (replace C:\Whatsapp by the location of the certain folder of your computer)
- or using the app Titanium Backup. Use Titanium Backup to backup the full whatsapp application together with its data, copy the backup from the folder "TitaniumBackup" on the SD card to your PC, then extract the files "wa.db" and "msgstore.db" that you will find inside the Titanium Backup archive "com.whatsapp-[Date]-[some digits].tar.gz" to the certain folder.
- or using some app like AirDroid or Webkey to access files over wifi using the PC webbrowser



