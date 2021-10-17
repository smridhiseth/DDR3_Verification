# DDR3_Verification

The simulator used is VCS ( Verilog compiler suite. )

$ source /apps/set_license.sh              /// 1. Point to the license server. set up shell variable pointing to license server. 
export VCS_HOME=/apps/synopsys/VCSMX_NEW  /// 2. Identify where VCS is located. set up environment variable VCS_HOME to identify the VCS simulator location.
                                         /// The export ‘shell’ command sets the variable in the shell environment. 
$ source ${VCS_HOME}/bin/environ.sh     /// 3. Run the VCS setup script. ‘environ.sh’ script from the VCS ‘bin’ directory which setups up tool specific variables
                                       /// 
 
 $ vcs -sverilog <file_name>.sv      /// 4. Compile. The parameter ‘-sverilog’ will be provided to ask the compiler to use the System Verilog language definition.
 $ ./simv                           /// 5. simulate. There will be an executable file in the current directory. The file is called ‘simv’. 
                                   /// The ‘simv’ file is commonly run by specifying ‘./simv’.
                                   
///////////////////////////////////////////////////////////////// runvcs - SCRIPT for compilation. - ./runvcs  

#!/bin/sh
source /apps/set_license.sh
export VCS_HOME=/apps/synopsys/VCSMX_NEW
source ${VCS_HOME}/bin/environ.sh
vcs -sverilog $@               ///   file to be compled is specified by $@.        
if [ $? -ne 0 ]; then          /// # check for a bad compile. If the commands didn't run successfully, they return a non zero code. code is specified by $?
    echo "= = = = = = = = = = = = ="
    echo "vcs compile didn''t work"
    exit 99
fi                           /// # end the if
./simv

 /////////////////////////////////////////////////////////////////
 
 to make runvcs executable :
 
 $chmod +x runvcs
 /////////////////////////////////////////////////////////////////////////////////
 
 the script can be run by typing on terminal :
 
 $ ./runvcs <filename>.sv
 /////////////////////////////////////////////////////////////////////////////////////
 
 Compile time options. 
 
 vcs +v2k <filename.v> -l <filename.txt> // Enables new language features. For example, multidimensiona arrays, power operator, indexed part selects, auto task, functions, always@(a,b,c) comma separated event controls, etc.  
 
 /////////////////////////////////////////////////////////////////////////////////////
 
 compiler directives used 
 
‘default_nettype none // specify that there is no default data type so all undeclared signals result in a syntax error. 

 //////////////////////////////////////////////
 
 Runtime Options
 
 ./simv -l <filename.txt> // Specifies writing all messages from simulation to the specified log file as well as displaying these messages in the standard output.
 
