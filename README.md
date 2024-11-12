# Systems Lab - Structs Files and Input

## Requirements

You should have a makefile with compile and run target.

`make compile` : should create a binary called `structrw` for ease of scripting on my end. That is compile *must* use `-o structrw`

You will find a csv file of NYC census population values in the class notes called `nyc_pop.csv`. Place this in the same directory as your code/makefile but don't add it to your repo! I will provide my own with the same name.

The header of the file is this: 
    
    Year,Manhattan,Brooklyn nine-nine,Queens,The Bronx,Staten Island

An example line of data is this: 

    1790,33131,4549,6159,1781,3827
    
You should support comma separated headers of boroughs with spaces in them. (e.g.) Staten island does not have to be the last entry. I modified the names to include some spaces like The Bronx.

Your goal: write a program that will perform the following actions based on a command line argument:

## -read_csv

Read the contents of the nyc_pop.csv file (this is text).

Store each piece of data using the following struct (exactly) :

    struct pop_entry {
      int year;
      int population;
      char boro[15];
    };

Create & write a new file nyc_pop.dat containing the population data using struct pop_entry . This file should contain byte data.

If the file already exists, overwrite the existing one.

## -read_data

Read the contents of the data file into an array of struct pop_entry values. This array should be dynamically allocated based on the file size.

Display the data in human-readable format, provide a number for each data entry when displaying.

Create a new file & write Or over-write any existing file named `nyc_pop.dat`. It should contain all of the data in your array of `struct pop_entry` . This file should contain the data directly, not text.
        

## -add_data

Ask the user for new data to put into a struct pop_entry value.

The data is entered into stdin in the format:  Year Population Borough

`1999 24025 The Bronx`

NOTE: The borough is last, so that you can have spaces in the name such as Staten Island or The Bronx. 

Update the entry in the data file (not the csv).

## -update_data

Start like -read_data 

Then prompt the user to enter the corresponding index of an entry to modify.

Then prompt the user for new data.

The data is entered into stdin in the format:  Year Population Borough

Update the entry in the data file (not the csv).

## Sample output: -read_csv
            
    $ ./structrw -read_csv
    reading nyc_pop.csv
    wrote 2760 bytes to nyc_pop.data

          
Year,Manhattan,Brooklyn nine-nine,Queens,The Bronx,Staten Island
## Sample output: -read_data

This is only the fist 11 entries, there should be 115 at the start.
            
    $ ./structrw -read_data
    0: year: 1790	boro: Manhattan	pop: 33131
    1: year: 1790	boro: Brooklyn nine-nine	pop: 4549
    2: year: 1790	boro: Queens	pop: 6159
    3: year: 1790	boro: The Bronx	pop: 1781
    4: year: 1790	boro: Staten Island	pop: 3827
    5: year: 1800	boro: Manhattan	pop: 60515
    6: year: 1800	boro: Brooklyn nine-nine	pop: 5740
    7: year: 1800	boro: Queens	pop: 6642
    8: year: 1800	boro: The Bronx	pop: 1755
    9: year: 1800	boro: Staten Island	pop: 4563
    10: year: 1810	boro: Manhattan	pop: 96373

          

## Sample output: -add_data

    $ ./structrw -add_data
    Enter year population borough: 2020 1390450 The Bronx
    Appended data to file: year: 2020	boro: The Bronx	pop: 1390450

"2020 1390450 Bronx" Was entered into stdin at the time of the program running. If you then -read_data that new entry will appear.

## Sample output:  -update_data

Only showing the last few lines of output, but all the data should be displayed.

"108" and "9999 4000 Stuy" where entered into stdin at the time of the program running..

            
    $ ./structrw -update_data
    107: year: 2000	boro: Queens	pop: 2229379
    108: year: 2000	boro: The Bronx	pop: 1332650
    109: year: 2000	boro: Staten Island	pop: 443728
    110: year: 2010	boro: Manhattan	pop: 1585873
    111: year: 2010	boro: Brooklyn nine-nine	pop: 2504700
    112: year: 2010	boro: Queens	pop: 2230722
    113: year: 2010	boro: The Bronx	pop: 1385108
    114: year: 2010	boro: Staten Island	pop: 468730
    115: year: 2020	boro: The Bronx	pop: 1390450
    entry to update: 108
    Enter year population borough: 9999 4000 Stuy
    File updated.

          

