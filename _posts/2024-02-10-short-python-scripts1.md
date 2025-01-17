---
layout: post
title:  "Short, kinda useful Python scripts"
date:   2024-02-08 00:00:00 -1000
categories: it python
image: lazy-python.jpg
---

These are small utilities for future me to use when I want to do things the lazy way with scripts. As with all scripts, run at your own risk. :) I don't develop or write Python for optimization; I write it enough that it works for my specific scenarios.

[Scripts found here.](https://github.com/sudoyashi/python_progress/tree/master/projects)

## Create folders with whatever is in a .csv

Wherever the script is, create a file called `directory.csv` and hard write the values 'CDs, software, drivers' in rows. Then, read that `.csv` and create folders based on those values. To create other folders, just edit the list of names in `directory.write`

```python
# Creates a list of directories if they do not exist. This creates
# the CDs, software, and drivers directories, as indicated by directory.csv
import os
import csv
from pathlib import Path

# create the file directory.csv

with open('directory.csv', 'w') as directory:
    directory.write('CDs,software,drivers')

# setup variable that loads all *.csv information
    
pathName = os.getcwd()
directoryFiles = os.listdir(pathName)
csvFiles = []
for file in directoryFiles:
    if file.endswith(".csv"):
        csvFiles.append(file)

with open('directory.csv') as csvfile:
    reader = csv.reader(csvfile, delimiter=',')
    for row in reader:
        for column in row:
            print(column)
            p = pathName + '\\' + column
            Path(p).mkdir(parents=True, exist_ok=True)
```

## Removing Title and Author metadata from .docx files

After saving a `.docx` file as an Adobe PDF, the pdf tab would show the document Title rather than the actual filename. This was a reoccuring issue because users like to copy and paste files for templates, so hundrerds of files had this Title misnomer over the years. One of our users thought this was a phishing attempt or virus. Fair enough. Thankfully, it was just a slight problem with metadata.

The script opens the current directory and checks all folders and files for `.docx` files. Then, we edit the properties to change the Author and Title. You can change any of the properties you need to, just modify the `core_properties` variable. The script does NOT cover `.doc` files; you would have to convert the `.doc` files into `.docx`.

```python
# Open all the documents and check to see if the document has a title, if so, remove it.
# Open all the documents and change the Author
import os
import fnmatch
from docx import Document

# Select all the docx
cwd = os.getcwd()
for dirpath, dirs, files in os.walk(cwd):
    for filename in fnmatch.filter(files, '*.docx'):
        # use print if you want to see what files will be modified
        # print (os.path.join(dirpath, filename)) 
        editFile = (os.path.join(dirpath, filename))
        document = Document(editFile)
        core_properties = document.core_properties
        # If the author filed is not my email, change it
        if (core_properties.author != 'joshua...email'):
            core_properties.author = 'joshua...newEmail'
        # Check if title is not empty, make it empty
        if (core_properties.title != ''):
            core_properties.title = ''
        # Save the file with the original name
        document.save(editFile)
        print ('Saved ', editFile)	
```

### You will have issues if these are server files!
If you're modifying server files, like me, the packages will not load properly because of the UNC path. You need to add the package to the server's local directory and then do a local import. The following submodules .py were affected and had to be modified:
  - `api.py`
  - `phys_pkg.py`
  - `package.py`
  - `pkgreader.py`

For each file above, append the following to the beginning list of imports:
```python
# mymodule.py
import os
import sys
# Add the parent directory of mypackage to the Python path
sys.path.append(os.path.abspath(os.path.join(os.path.dirname(__file__), '..')))
```

Then you can import the package using:

```python
from docx import Document
```
Depending on the directory setup, it may take a couple of tries to read the errors. You may also have to replace any __ init__.py with empty files. For more information, read the issue on [Attempted relative import with no known parent package](https://net-informations.com/q/py/known.html).

## Convert XML files to Excel (.xlsx)

Find all `.xml` files in the current working directory, convert them to `.xlsx`, and save the converted files in an existing folder called `.xlsx`.

Our VoIP phones use `.xml` files to create a directory; however, reading raw `.xml` is atrocious work. We can convert them to `.xlsx` for quick viewing to make sure there are no parsing or spelling errors.

```python

# This script finds all files that end with .xml and puts them into a list. In that list,
# extract the xml value pairs, remove duplicates and write the pairs into sheet1 
# of a new Excel sheet within columns B:Z
# Finally, save the XML as an XLSX into the xlsx directory.

import xml.etree.ElementTree as ETree
import pandas as pd
import os
import pathlib
from os import listdir, path
from pathlib import Path

cwd = os.getcwd()
files = []
for file in listdir(cwd):
    if file.endswith('.xml'):
        files.append(path.join(cwd, file))

for xml in files:
    fileroot = Path(xml).stem
    tree = ETree.parse(xml)
    root = tree.getroot()
    valuePairs = []  # empty list assigned to A
    for elements in root:
        valuePair = {}  # empty array; store data in key:value pair
        for element in list(elements):
            valuePair.update({element.tag: element.text})  # updating dictionary with(tag -> Columns, text -> Rowdata)
            valuePairs.append(valuePair)  # Append key:value pair to A list
        df = pd.DataFrame(valuePairs)  # Create dataframe (df)
        df.drop_duplicates(keep='first', inplace=True)  # Only keep first, ignore all others
        df.reset_index(drop=True, inplace=True)
        writer = pd.ExcelWriter(cwd + '\\' + 'xlsx' + '\\' + fileroot + '.xlsx', engine='xlsxwriter')
        df.to_excel(writer, sheet_name='sheet1')
        worksheet = writer.sheets['sheet1']
        worksheet.set_column('B:Z', 30)  # Set column char to 30 for columns from B to Z
        writer._save()
    print(df)
    print('XML file has been parsed. Open at ' + fileroot + '.xlsx...')
```

## Snakes are aight when they're on your side

I am not trying to edit 300+ files within each directory to rename the file to something else. That's why you make a script! I could optimize them, but at the tiny scale I have them, I don't need to right now. Thank goodness for modern hardware.