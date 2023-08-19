##DEFINITIONS

SOP_types := $(shell ls sop_*.tex | sed 's/sop_//g' | sed 's/.tex//g') #list of all SOP types
type_folders := $(foreach type,$(SOP_types),programs_$(type)_specific_files)
program_folders := $(foreach type,$(SOP_types),$(addprefix programs_$(type)_specific_files/,$(shell cat programs_$(type).txt)))
names := $(foreach folder, $(program_folders), $(folder)/name.tex) #program name tex files to be edited
specific_paragraph := $(foreach folder, $(program_folders), $(folder)/specific_paragraph.tex) #type-graduate school program specific paragraph tex files to be edited
#all other inputs are all .tex files in the current directory except for any files that start with "sop"
all_other_inputs = $(shell ls entries/*.tex | grep -v sop)
#total SOPs
sops := $(foreach folder, $(program_folders), $(folder)/$(shell echo $(folder)| grep -o '[^/]*$$')_sop.pdf)
all: $(sops)
folders: $(type_folders) $(program_folders)
names: $(names)
specific_paragraph: $(specific_paragraph)

.SECONDEXPANSION:
$(sops): %_sop.pdf: sop_$$(shell echo $$* | sed 's/.*programs_\([^_]*\)_specific_files.*/\1/').tex $$(shell dirname $$*)/name.tex $$(shell dirname $$*)/specific_paragraph.tex $(all_other_inputs)
	cp $<  $*_$<
	pdflatex -draftmode -output-directory=$(dir $@) $*_$<
	pdflatex -output-directory=$(dir $@) $*_$<
	rm -f $(dir $@)/logbook.log $(dir $@)/logbook.out $(dir $@)/logbook.toc $(dir $@)/logbook.aux

.PHONEY: type_folders program_folders echo_sops

$(program_folders): $(type_folders)
	mkdir -p $@
$(type_folders):
	mkdir -p $@
$(names): $(program_folders)
	touch $@ 
$(specific_paragraph): $(program_folders)
	touch $@