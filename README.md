KeepGrabbing
============

This is a collection of scripts for managing scrapers

**Summary**

- `jsongen.rb` - Generates JSONs using a schema you specify. Can be used for 
anything, but it's good for making machine-readable lists of search terms
- `linkedin.rb` - Runs the LinkedIn scraper on a set of search terms in a json
- `crypto` - Encrypt and decrypt all files in a directory with GPG
- `config` - Scripts for setup and syncing a scraping machine
- `documents.rb` - Convert document files to JSON
- `emails.rb` - Convert email files to JSON

### Detailed Instructions

1. Run `ruby jsongen.rb`

Currently this only supports single level JSONs.

To Run:

1. Run `ruby json.rb`
2. Follow the directions to manually input the schema and items
3. Stop adding items by adding an item with all blank fields

linkedin.rb

To run this, you need a JSON where every item has the following fields:
Search Term: The phrase you want to search for
Degrees: The number of degrees you want to go out with "people also viewed"

To Run:

1. Run `ruby linkedin.rb`
2. When prompted, type in the name of the file with the search terms
3. When prompted, type in the name of the directory where you want to save results
4. Wait. A new .json and .csv file will be generated for each search term

`crypto/` - Encrypt files with encrypt.rb and decrypt with decrypt.rb.

## Encrypt & Decrypting Files

**Encrypting**

1. Run `ruby encrypt.rb`
2. When prompted, type the email address of recipient (keys must be imported
into GPG already). You can add as many recipients as you want
3. Hit enter, leaving a recipient blank, when you want to stop adding
recipients
4. When prompted, enter the path to the directory where you want to save
results
5. Wait as the files are encrypted

**Decrypting**

1. Run `ruby decrypt.rb`
2. When prompted, enter the path to the directory where you want to decrypt
files.
3. Enter the password for your GPG key
4. Wait as the files are decrypted

---

`config/` - Setup and syncing scripts for a scraping machine

Setup & Sync:

```
./install.sh
./sync.sh
```

## Installing

1. Install system dependencies for Debian

```
sudo apt-get install build-essential pkg-config curl libcurl3 libcurl3-gnutls 
libcurl4-openssl-dev rmagic libmagickwand-dev imagemagick graphicsmagick 
poppler-utils poppler-data ghostscript tesseract-ocr pdftk libreoffice
```

2. Install Ruby dependencies `bundle install` from in the directory
3. Run the document converter script

By default, documents and images will be processed with the
[GiveMeText](http://givemetext.okfnlabs.org) tool, but **IS NOT GOOD FOR
SENSITIVE DOCUMENTS** as it sends normal HTTP requests over the internet. 
However, you can run a custom Tika server for converting documents yourself.

4. [Setup Local Tika](https://github.com/TransparencyToolkit/Harvester#install-tika--tesseract-optional))

## Running

You can process either emails or normal text documents using the following
scripts:

### Documents

Run the script to convert documents in JSON as well as with local Tika instance

```
ruby documents.rb path/to/your/files/
ruby documents.rb --tika=http://localhost:9998 /path/to/your/documents
```

### Emails

Run email script to convert emails to JSON

```
ruby emails.rb /path/to/your/emails
```

**Attachments**

If your emails generated an `attachments/` folder, then run the `documents.rb`
script as described above to convert attachments into JSON as well

```
ruby documents.rb --tika=http://localhost:9998 /path/to/youre/emails_output/attachments
```
