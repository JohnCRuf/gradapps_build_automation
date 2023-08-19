# gradapps_build_automation
## Introduction

This file describes how to use my SOP build automation code.
The point of this code is to help eliminate most of the headache of writing ~30 tailored SOPs by using build automation to ensure that each SOP is up-to-date and consistent with the others.
For example, you may be applying to 5 programs where you want to emphasize your research interests in X, but in a different set of 5 programs you want to emphasize your research interests in Y.
Normally, you would write 10 different SOPs in 10 different word documents, and then you would have to manually update each one if you wanted to change something.
Furthermore, you would only tailor a small portion of your SOP to each program, normally about the size of a paragraph or two.
But, whenever you want to update the common introduction of your SOP, you'd have to manually update each SOP. 

When applying to ~20-30 programs, this can be a huge headache.
With this code, you can have 2 SOP `types` that have a set of common input files for the common components and a set of `program-specific` inputs for the program-specific components.
Then, to edit the `common` components, you only have to edit one file, and then you can run the code to generate all of the SOPs which will be automatically updated with the new common components.

In fact, as you will learn this code is so flexible that you can have as many SOP types as you want, and you can have as many program-specific inputs as you want.
In fact, you can use the same 

## How to Use

This system relies on two programs, `GNU-make` and `pdfLaTeX`. 
For installation of GNU-make, see [here](https://www.gnu.org/software/make/#download).
For installation of pdfLaTeX, see [here](https://www.latex-project.org/get/).

To get started, install the above programs and then navigate to this  directory in your terminal.
Then, run the following command to ensure that the code is working properly:

```bash
make
```
This tells the makefile to run and automatically generate the `test` SOPs.
You should get 4 new folders, ``programs_v1_specific_files/test_1``, `programs_v1_specific_files/test_2`, ..., `programs_v2_specific_files/test_1`, `programs_v2_specific_files/test_2`. 
Where each folder contains an SOP generated from the `test` SOP type and the `test_1` and `test_2` program-specific inputs.
When the code is working properly, you can delete these folders.

Now that everything is working, you can start to customize the code to your needs.
First, you should edit the type-specific `master` latex files, `sop_v1.tex` and `sop_v2.tex`.
You can have as many SOP types as you want, but each type must have a `master` latex file that starts with `sop_` and ends with `.tex` with the type marker in between. 
In the "test" setup, the type marker is `v1` and `v2`, but you can change this to whatever you want.
Next, you will want to add your programs for each SOP type.
To do this, you will need to create a new "programs" text file for each SOP type.
The name of the file must start with `programs_` and end with `.txt` with the type marker in between.
This type marker must match the type marker in the name of the `master` latex file.
In the "test" setup, the type marker is `v1` and `v2`, but you can change this to whatever you want.
The contents of the file should be a list of the strings that demarcate each graduate school program that you are applying to with that SOP type.

After you have edited the `master` latex files and created the `programs` text files, you can start to generate the common portions of your SOPs.
To get started you will want to run `make folders` to generate the folders for each SOP type and program you have listed in the `programs` and `master` `.tex` files.
Then to generate program name .tex files for each program you have listed in the `programs` text files, you will want to run `make names` and `make specific_paragraphs`.
You can now write your SOP normally, using the `\input{}` command to include the common components of your SOP.
Now instead of having ~30 SOPs that each need to be updated individually, you can now have 30 SOPs where you only need to update the common components once, and then run `make` to update all of the SOPs.
Make sure to put all common inputs in the `entries` folder.

If you have any issues, please feel free to create a new issue on this repository and I will try to help you out.
