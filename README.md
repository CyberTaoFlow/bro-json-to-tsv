# Bro JSON to TSV

## Purpose
Covert Bro JSON files (specifically, conn, dns, http and ssl) in the input_folder to TSV in the output_folder 

## Background
Active Countermeasures (https://www.activecountermeasures.com/) has an awesome project called RITA (https://github.com/activecm/rita) that analyzes bro, TSV, telemetry to look for beaconing, DNS tunneling, and blacklist hits.

Security Onion, by default, creates the bro telemetry as JSON.  Several vendors I used needed JSON so the easiest thing was to create a converter.

## Requirements

* python3, python3-pip
* Libraries: tqdm  (can be installed with pip3 install -r requirements.txt)

## Execution

python3 run_parser.py --input_folder /json/folder/path --output_folder /output/folder/path

## Methodology

* gunzip the files in the input folder if they are compressed
* For every file in the input folder path:
  * Check the first line of the file to see what file type it is (e.g. conn, by checking the keys in the dict)
  * Add the TSV header to the output file
  * Add each JSON line as a TSV to the output file

## Notes

* Be careful with module/make_header.py.  The header format is finicky, e.g. most items are separated by tabs, not spaces.  Modifying it (e.g. converting the tabs to 4 spaces) will break TSV readers/parsers.
