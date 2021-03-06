##----------------------------------------------------------------------------##
##
##   CARLsim3 Project Makefile
##   -------------------------
##
##   Authors:   Michael Beyeler <mbeyeler@uci.edu>
##              Kristofor Carlson <kdcarlso@uci.edu>
##
##   Institute: Cognitive Anteater Robotics Lab (CARL)
##              Department of Cognitive Sciences
##              University of California, Irvine
##              Irvine, CA, 92697-5100, USA
##
##   Version:   03/04/2017
##
##----------------------------------------------------------------------------##

################################################################################
# Start of user-modifiable section
################################################################################

# In this section, specify all files that are part of the project.

# Name of the binary file to be created.
# NOTE: There must be a corresponding .cpp file named main_$(proj_target).cpp!
proj_target1   := smooth
proj_target2   := dog

# Directory where all include files reside. The Makefile will automatically
# detect and include all .h files within that directory.
proj_inc_dir   := .

# Directory where all source files reside. The Makefile will automatically
# detect and include all .cpp and .cu files within that directory.
proj_src_dir   := .

################################################################################
# End of user-modifiable section
################################################################################


#------------------------------------------------------------------------------
# Include configuration file
#------------------------------------------------------------------------------

# NOTE: If your CARLsim5 installation does not reside in the default path, make
# sure the environment variable CARLSIM5_INSTALL_DIR is set.
ifdef CARLSIM5_INSTALL_DIR
	CARLSIM5_INC_DIR  := $(CARLSIM5_INSTALL_DIR)/include
else
	CARLSIM5_INC_DIR  := $(HOME)/CARL/include
endif

# include compile flags etc.
include $(CARLSIM5_INC_DIR)/configure.mk


#------------------------------------------------------------------------------
# Build local variables
#------------------------------------------------------------------------------

main_src_file1 := $(proj_src_dir)/main_$(proj_target1).cpp
main_src_file2 := $(proj_src_dir)/main_$(proj_target2).cpp

# build list of all .h files
inc_files  := $(wildcard $(proj_inc_dir)/*.h)

# compile .cpp files to -cpp.o, and .cu files to -cu.o

# handled by clean and distclean
clean_files := $(proj_target1).out $(proj_target2).out
distclean_files := $(clean_files) results/* *.dot *.dat *.csv *.log


#------------------------------------------------------------------------------
# Project targets and rules
#------------------------------------------------------------------------------

.PHONY: $(proj_target1) $(proj_target2) clean distclean help
default: $(proj_target1)


$(proj_target1): $(main_src_file1) $(inc_files)
	$(eval CARLSIM5_FLG += -Wno-deprecated-gpu-targets)
	$(eval CARLSIM5_LIB += -lcurand)
	$(NVCC) $(CARLSIM5_FLG) $(obj_files) $< -o $@.out $(CARLSIM5_LIB)

$(proj_target2): $(main_src_file2) $(inc_files)
	$(eval CARLSIM5_FLG += -Wno-deprecated-gpu-targets)
	$(eval CARLSIM5_LIB += -lcurand)
	$(NVCC) $(CARLSIM5_FLG) $(obj_files) $< -o $@.out $(CARLSIM5_LIB)

clean:
	$(RM) $(clean_files)

distclean:
	$(RM) $(distclean_files)

help:
	$(info CARLsim5 Project options:)
	$(info )
	$(info make               Compiles test suite
	$(info make clean         Cleans out all object files)
	$(info make distclean     Cleans out all object and output files)
	$(info make help          Brings up this message)
