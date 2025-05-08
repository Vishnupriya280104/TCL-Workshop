# TCL-Workshop
From Introduction to Advanced Scripting Techniques in VLSI Design and Synthesis
The workshop equips participants with advanced TCL scripting skills for automating digital design flows. The journey begins with TCL fundamentals and extends into complex topics such as constraints parsing, memory module synthesis with Yosys, and quality of results (QOR) analysis.

<details>
    <summary>
      
## Module-1: Introduction to TCL and VSDSYNTH Toolbox usage 
    </summary>
   This module deals with TCL task and sub-task fundamentals, VSDSYNTH Toolbox scenarios and help flow,and handling user input and CSV formats. 
   
  In VLSI (Very Large Scale Integration), TCL stands for Tool Command Language. It's a popular scripting language used to automate and control various tasks within the design flow of integrated circuits.

  ### Sub-Task and Tools needed: ###
  + Create command (vsdsynth) and pass (.csv) from UNIX shell to TCL script
  + Convert all inputs to format[1] and sdc format, and pass to synthesis tool 'Yosys'
  + Convert format[1] and sdc to format[2] and pass to timing tool 'Opentimer'
  + Generate output report
    
  **Create command (vsdsynth) and pass (.csv) from UNIX shell to TCL script**
    General Scenarios - From user point of view
    + Not provide .csv file as input
      
 ```bash
    $./vsdsynth
    # if($argv !=1) then
          #echo "Info: Please provide the csv file"
          #exit 
```
  + Provide a .csv file which doesn't exist
    
```bash
    $./vsdynth my.csv
    # if(! -f $argv[1] || $argv[1] == "-help") then
        #if ($argv[1] != "-help") then
          #echo "Error: Cannot find csv file $argv[1]. Exiting..."
          #exit
```
  + Type "-help" to find out usage

```bash
    $./vsdsynth -help
    # if(! -f $argv[1] || $argv[1] == "-help") then
        #if ($argv[1] != "-help") then
          #echo "Error: Cannot find csv file $argv[1]. Exiting..."
          #exit 1
        #else
          #echo USAGE: ./vsdsynth\<csv.file>
          #echo ...
          #echo ...
          #exit 1
    #endif
```

</details>

<details>
  
  <summary> 
    
##  Module-2: Variable creation and CSV/SDC constraint processing
  </summary>
 
  This module includes creating variables using matrix and array methods, checking for design file existence, and complex CSV row/column processing. 

  **Convert all inputs to format[1] and sdc format, and pass to synthesis tool 'Yosys'**  
  Tasks involved:
  + Create variable
  + Check if directories and files mentioned in .csv exists or not
  + Read "Constraints File" for above .csv and convert to sdc format
  + Read all files in "Netlist Directories"
  + Create main synthesis script in Format[2]
  + Pass this script to Yosys

  **Create Variables**
  Various steps involved in creating variables are, first converting the excel(csv file) data into a matrix and then convert the matrix into an array.

  Commands used are:

```bash
    set filename [lindex $argv 0]           ;# Get the filename from the first command-line argument
    pakage require csv                      ;# (Typo) Should be 'package'; load the csv package
    package require struct::matrix          ;# Load the struct::matrix package for matrix operations
    struct :: matrix m                      ;# Create a new matrix named 'm'
    set f [open $filename]                  ;# Open the input CSV file for reading
    csv::read2matrix $f m, auto             ;# Read CSV content into matrix 'm' with auto-detected format
    close $f                                ;# Close the file after reading
    set columns [m columns]                 ;# Get the number of columns in the matrix
    m add columns $columns                  ;# Add the same number of columns again (likely unnecessary or incorrect)
    m link my_arr                           ;# Link the matrix 'm' to an array variable 'my_arr'
    set num_of_rows [m rows]                ;# Get the number of rows in the matrix
    set i 0                                 ;# Initialize index variable i to 0
```
    
    
    
  </details>
  
