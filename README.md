![made-with-python](https://img.shields.io/badge/Made%20with-Python3-brightgreen)

<!-- LOGO -->
<br />
<p align="center">
  <img src="https://user-images.githubusercontent.com/1237743/125965643-35d4eefd-963f-475b-9b36-c95564329e03.png" alt="Logo" width="140" height="110">
  <h3 align="center">FastColabCopy</h3>

  <p align="center">
    Python3 script transfer files in Google Colab 10-50x faster.
    <br />
    </p>
</p>

## About The Project
FastColabCopy is a Python script for parallel (multi-threading) copying of files between two locations. Currently developed for Gooele-Drive to Google-Drive transfers using Google-Colab. This script frequently achieves 10-50x speed improvements when copying numerous small files.

## Importing

Import from GitHub.   
```
!wget https://raw.githubusercontent.com/L0garithmic/fastcolabcopy/main/fastcopy.py
import fastcopy
```

Import from Google Drive
```
!cp /gdrive/MyDrive/fastcopy.py .
import fastcopy
```


## Usage
```sh
usage: fast-copy.py [-h HELP] source destination [-d DELETE] [-s SYNC] [-r REPLACE ]

optional arguments:
  -h, --help            show this help message and exit
  source                the drive you are copying from
  destination           the drive you are copying too
  -d --delete           delete the source files after copy
  -s --sync             remove files from destination if they do not exist in source
  -r --replace          replace files if they exist
  -t --thread           set the amount of parallel  threads used
  -l --size-limit       set max size of files copied (supports gb, mb, kb) eg 1.5gb
```
The `source` and `destination` fields are required. Everything else is optional.

## Examples
```
from google.colab import drive
drive.mount('/gdrive', force_remount=False)
import os
!wget -q https://raw.githubusercontent.com/L0garithmic/fastcolabcopy/main/fastcopy.py
import fastcopy
!python fastcopy.py /gdrive/Shareddrives/SourceDrive/. /gdrive/Shareddrives/DestDrive --sync
```
If you want to see copy execution time
```
!pip install -q ipython-autotime
%load_ext autotime
```
Check out examples.md for some full scale file copy examples.

## Testing Results
Colab has wildly varying transfer speeds, because of this, the best we can offer are suggestions.
- For large groups of medium/small files, 15-40 threads seems to work best.
- For 50+ files with significantly varying sizes. Try 2 sequentially copies. `-t 15 -l 350` then `-t 2`
- Files that are hundred MB's and over, it is best to use 2 threads, it is is still faster then rsync.   

## Credits
Credit to [ikonikon](https://github.com/ikonikon/fast-copy) for the base multi-threading code.   
Thanks to [@Ostokhoon](https://www.freelancer.com/u/Ostokhoon) for ALL argument and folder hierarchy functionality.
