<<<<<<< HEAD
# rsicv-opcodes-matrix

for matrix instructions merge with office

## Getting started

To make it easy for you to get started with GitLab, here's a list of recommended next steps.

Already a pro? Just edit this README.md and make it your own. Want to make it easy? [Use the template at the bottom](#editing-this-readme)!

## Add your files

- [ ] [Create](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#create-a-file) or [upload](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#upload-a-file) files
- [ ] [Add files using the command line](https://docs.gitlab.com/ee/gitlab-basics/add-file.html#add-a-file-using-the-command-line) or push an existing Git repository with the following command:

```
cd existing_repo
git remote add origin http://code.streamcomputing.com/simulator/rsicv-opcodes-matrix.git
git branch -M master
git push -uf origin master
```

## Integrate with your tools

- [ ] [Set up project integrations](http://code.streamcomputing.com/simulator/rsicv-opcodes-matrix/-/settings/integrations)

## Collaborate with your team

- [ ] [Invite team members and collaborators](https://docs.gitlab.com/ee/user/project/members/)
- [ ] [Create a new merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html)
- [ ] [Automatically close issues from merge requests](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically)
- [ ] [Enable merge request approvals](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/)
- [ ] [Automatically merge when pipeline succeeds](https://docs.gitlab.com/ee/user/project/merge_requests/merge_when_pipeline_succeeds.html)

## Test and Deploy

Use the built-in continuous integration in GitLab.

- [ ] [Get started with GitLab CI/CD](https://docs.gitlab.com/ee/ci/quick_start/index.html)
- [ ] [Analyze your code for known vulnerabilities with Static Application Security Testing(SAST)](https://docs.gitlab.com/ee/user/application_security/sast/)
- [ ] [Deploy to Kubernetes, Amazon EC2, or Amazon ECS using Auto Deploy](https://docs.gitlab.com/ee/topics/autodevops/requirements.html)
- [ ] [Use pull-based deployments for improved Kubernetes management](https://docs.gitlab.com/ee/user/clusters/agent/)
- [ ] [Set up protected environments](https://docs.gitlab.com/ee/ci/environments/protected_environments.html)

***

# Editing this README

When you're ready to make this README your own, just edit this file and use the handy template below (or feel free to structure it however you want - this is just a starting point!). Thank you to [makeareadme.com](https://www.makeareadme.com/) for this template.

## Suggestions for a good README
Every project is different, so consider which of these sections apply to yours. The sections used in the template are suggestions for most open source projects. Also keep in mind that while a README can be too long and detailed, too long is better than too short. If you think your README is too long, consider utilizing another form of documentation rather than cutting out information.

## Name
Choose a self-explaining name for your project.

## Description
Let people know what your project can do specifically. Provide context and add a link to any reference visitors might be unfamiliar with. A list of Features or a Background subsection can also be added here. If there are alternatives to your project, this is a good place to list differentiating factors.

## Badges
On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Visuals
Depending on what you are making, it can be a good idea to include screenshots or even a video (you'll frequently see GIFs rather than actual videos). Tools like ttygif can help, but check out Asciinema for a more sophisticated method.

## Installation
Within a particular ecosystem, there may be a common way of installing things, such as using Yarn, NuGet, or Homebrew. However, consider the possibility that whoever is reading your README is a novice and would like more guidance. Listing specific steps helps remove ambiguity and gets people to using your project as quickly as possible. If it only runs in a specific context like a particular programming language version or operating system or has dependencies that have to be installed manually, also add a Requirements subsection.

## Usage
Use examples liberally, and show the expected output if you can. It's helpful to have inline the smallest example of usage that you can demonstrate, while providing links to more sophisticated examples if they are too long to reasonably include in the README.

## Support
Tell people where they can go to for help. It can be any combination of an issue tracker, a chat room, an email address, etc.

## Roadmap
If you have ideas for releases in the future, it is a good idea to list them in the README.

## Contributing
State if you are open to contributions and what your requirements are for accepting them.

For people who want to make changes to your project, it's helpful to have some documentation on how to get started. Perhaps there is a script that they should run or some environment variables that they need to set. Make these steps explicit. These instructions could also be useful to your future self.

You can also document commands to lint the code or run tests. These steps help to ensure high code quality and reduce the likelihood that the changes inadvertently break something. Having instructions for running tests is especially helpful if it requires external setup, such as starting a Selenium server for testing in a browser.

## Authors and acknowledgment
Show your appreciation to those who have contributed to the project.

## License
For open source projects, say how it is licensed.

## Project status
If you have run out of energy or time for your project, put a note at the top of the README saying that development has slowed down or stopped completely. Someone may choose to fork your project or volunteer to step in as a maintainer or owner, allowing your project to keep going. You can also make an explicit request for maintainers.
=======
# riscv-opcodes

This repo enumerates standard RISC-V instruction opcodes and control and
status registers.  It also contains a script to convert them into several
formats (C, Scala, LaTeX).

Artifacts (encoding.h, latex-tables, etc) from this repo are used in other 
tools and projects like Spike, PK, RISC-V Manual, etc. 

## Project Structure

```bash
├── constants.py    # contains variables, constants and data-structures used in parse.py
├── encoding.h      # the template encoding.h file
├── LICENSE         # license file
├── Makefile        # makefile to generate artifacts
├── parse.py        # python file to perform checks on the instructions and generate artifacts
├── README.md       # this file
├── rv*             # instruction opcode files
└── unratified      # contains unratified instruction opcode files
```

## File Naming Policy

This project follows a very specific file structure to define the instruction encodings. All files
containing instruction encodings start with the prefix `rv`. These files can either be present in
the root directory (if the instructions have been ratified) or the `unratified` directory. The exact
file-naming policy and location is as mentioned below:

1. `rv_x` - contains instructions common within the 32-bit and 64-bit modes of extension X.
2. `rv32_x` - contains instructions present in rv32x only (absent in rv64x e.g.. brev8)
3. `rv64_x` - contains instructions present in rv64x only (absent in rv32x, e.g. addw)
4. `rv_x_y` - contains instructions when both extension X and Y are available/enabled. It is recommended to follow canonical ordering for such file names as specified by the spec.
5. `unratified` - this directory will also contain files similar to the above policies, but will
   correspond to instructions which have not yet been ratified.

When an instruction is present in multiple extensions and the spec is vague in defining the extension which owns the instruction, the instruction encoding must be placed in the first canonically ordered extension and should be imported(via the `$import` keyword) in the remaining extensions.

## Encoding Syntax


The encoding syntax uses `$` to indicate keywords. As of now 2 keywords have been identified : `$import` and `$pseudo_op` (described below). The syntax also uses `::` as a means to define the relationship between extension and instruction. `..` is used to defined bit ranges. We use `#` to define comments in the files. All comments must be in a separate line. In-line comments are not supported.

Instruction syntaxes used in this project are broadly categorized into three:

- **regular instructions** :- these are instructions which hold a unique opcode in the encoding space. A very generic syntax guideline 
  for these instructions is as follows:
  ```
  <instruction name> <arguments>
  ```
  where `<argument>` is either `<bit encoding>` or `<variable argument>`.

  Examples:
  ```
  lui     rd imm20 6..2=0x0D 1..0=3
  beq     bimm12hi rs1 rs2 bimm12lo 14..12=0 6..2=0x18 1..0=3
  ```
  The bit encodings are usually of 2 types: 
    - *single bit assignment* : here the value of a single bit is assigned using syntax `<bit-position>=<value>`. For e.g. `6=1` means bit 6 should be 1. Here the value must be 1 or 0.
    - *range assignment*: here a range of bits is assigned a value using syntax: `<msb>..<lsb>=<val>`. For e.g. `31..24=0xab`. The value here can be either unsigned integer, hex (0x) or binary (0b). 

- **pseudo_instructions** (a.k.a pseudo\_ops) - These are instructions which are aliases of regular instructions. Their encodings force 
  certain restrictions over the regular instruction. The syntax for such instructions uses the `$pseudo_op` keyword as follows:
  ```
  $pseudo_op <extension>::<base-instruction> <instruction name> <instruction args> <bit-encodings>
  ```
  Here the `<extension>` specifies the extension which contains the base instruction. `<base-instruction>` indicates the name of the instruction 
  this pseudo-instruction is an alias of. The remaining fields are the same as the regular instruction syntax, where all the args and the fields 
  of the pseudo instruction are specified.
  
  Example:
  ```
  $pseudo_op rv_zicsr::csrrs frflags rd 19..15=0 31..20=0x001 14..12=2 6..2=0x1C 1..0=3
  ```

  If a ratified instruction is a pseudo\_op of a regular unratified
  instruction, it is recommended to maintain this pseudo\_op relationship i.e.
  define the new instruction as a pseudo\_op of the unratified regular
  instruction, as this avoids existence of overlapping opcodes for users who are
  experimenting with unratified extensions as well.
  
- **imported_instructions** - these are instructions which are borrowed from an extension into a new/different extension/sub-extension. Only regular instructions can be imported. Pseudo-op or already imported instructions cannot be imported. Example:
  ```
  $import rv32_zkne::aes32esmi
  ```

### RESTRICTIONS

Following are the restrictions one should keep in mind while defining $pseudo\_ops and $imported\_ops

- Pseudo-op or already imported instructions cannot be imported again in another file. One should
  always import base-instructions only.
- While defining a $pseudo\_op, the base-instruction itself cannot be a $pseudo\_op

## Flow for parse.py

The `parse.py` python file is used to perform checks on the current set of instruction encodings and also generates multiple artifacts : latex tables, encoding.h header file, etc. This section will provide a brief overview of the flow within the python file.

To start with, `parse.py` creates a list of all `rv*` files currently checked into the repo (including those inside the `unratified` directory as well). 
It then starts parsing each file line by line. In the first pass, we only capture regular instructions and ignore the imported or pseudo instructions. 
For each regular instruction, the following checks are performed :

  - for range-assignment syntax, the *msb* position must be higher than the *lsb* position
  - for range-assignment syntax, the value of the range must representable in the space identified by *msb* and *lsb*
  - values for the same bit positions should not be defined multiple times.
  - All bit positions must be accounted for (either as args or constant value fields)
 
Once the above checks are passed for a regular instruction, we then create a dictionary for this instruction which contains the following fields:
  - encoding : contains a 32-bit string defining the encoding of the instruction. Here `-` is used to represent instruction argument fields
  - extension : string indicating which extension/filename this instruction was picked from
  - mask : a 32-bit hex value indicating the bits of the encodings that must be checked for legality of that instruction
  - match : a 32-bit hex value indicating the values the encoding must take for the bits which are set as 1 in the mask above
  - variable_fields : This is list of args required by the instruction

The above dictionary elements are added to a main `instr_dict` dictionary under the instruction node. This process continues until all regular 
instructions have been processed. In the second pass, we now process the `$pseudo_op` instructions. Here, we first check if the *base-instruction* of 
this pseudo instruction exists in the relevant extension/filename or not. If it is present, the the remaining part of the syntax undergoes the same 
checks as above. Once the checks pass and if the *base-instruction* is not already added to the main `instr_dict` then the pseudo-instruction is added to 
the list. In the third, and final, pass we process the imported instructions.

The case where the *base-instruction* for a pseudo-instruction may not be present in the main `instr_dict` after the first pass is if the only a subset 
of extensions are being processed such that the *base-instruction* is not included. 


## Artifact Generation and Usage

The following artifacts can be generated using parse.py:

- instr\_dict.yaml : This is file generated always by parse.py and contains the
  entire main dictionary `instr\_dict` in YAML format. Note, in this yaml the
  *dots* in an instruction are replaced with *underscores*
- encoding.out.h : this is the header file that is used by tools like spike, pk, etc
- instr-table.tex : the latex table of instructions used in the riscv-unpriv spec
- priv-instr-table.tex : the latex table of instruction used in the riscv-priv spec
- inst.chisel : chisel code to decode instructions
- inst.sverilog : system verilog code to decode instructions
- inst.rs : rust code containing mask and match variables for all instructions
- inst.spinalhdl : spinalhdl code to decode instructions
- inst.go : go code to decode instructions

Make sure you install the required python pre-requisites are installed by executing the following
command:

```
sudo apt-get install python-pip3
pip3 install -r requirements.txt
```

To generate all the above artifacts for all instructions currently checked in, simply run `make` from the root-directory. This should print the following log on the command-line:

```
Running with args : ['./parse.py', '-c', '-go', '-chisel', '-sverilog', '-rust', '-latex', '-spinalhdl', 'rv*', 'unratified/rv*']
Extensions selected : ['rv*', 'unratified/rv*']
INFO:: encoding.out.h generated successfully
INFO:: inst.chisel generated successfully
INFO:: inst.spinalhdl generated successfully
INFO:: inst.sverilog generated successfully
INFO:: inst.rs generated successfully
INFO:: inst.go generated successfully
INFO:: instr-table.tex generated successfully
INFO:: priv-instr-table.tex generated successfully
```

By default all extensions are enabled. To select only a subset of extensions you can change the `EXTENSIONS` variable of the makefile to contains only the file names of interest.
For example if you want only the I and M extensions you can do the following:

```bash
make EXTENSIONS='rv*_i rv*_m' 
```

Which will print the following log:

```
Running with args : ['./parse.py', '-c', '-chisel', '-sverilog', '-rust', '-latex', 'rv32_i', 'rv64_i', 'rv_i', 'rv64_m', 'rv_m']
Extensions selected : ['rv32_i', 'rv64_i', 'rv_i', 'rv64_m', 'rv_m']
INFO:: encoding.out.h generated successfully
INFO:: inst.chisel generated successfully
INFO:: inst.sverilog generated successfully
INFO:: inst.rs generated successfully
INFO:: instr-table.tex generated successfully
INFO:: priv-instr-table.tex generated successfully
```

If you only want a specific artifact you can use one or more of the following targets : `c`, `rust`, `chisel`, `sverilog`, `latex`

You can use the `clean` target to remove all artifacts.

## Adding a new extension

To add a new extension of instructions, create an appropriate `rv*` file based on the policy defined in [File Structure](#file-naming-policy). Run `make` from the root directory to ensure that all checks pass and all artifacts are created correctly. A successful run should print the following log on the terminal:

```
Running with args : ['./parse.py', '-c', '-chisel', '-sverilog', '-rust', '-latex', 'rv*', 'unratified/rv*']
Extensions selected : ['rv*', 'unratified/rv*']
INFO:: encoding.out.h generated successfully
INFO:: inst.chisel generated successfully
INFO:: inst.sverilog generated successfully
INFO:: inst.rs generated successfully
INFO:: instr-table.tex generated successfully
INFO:: priv-instr-table.tex generated successfully
```

Create a PR for review.

## Enabling Debug logs in parse.py

To enable debug logs in parse.py change `level=logging.INFO` to `level=logging.DEBUG` and run the python command. You will now see debug statements on 
the terminal like below:
```
DEBUG:: Collecting standard instructions first
DEBUG:: Parsing File: ./rv_i
DEBUG::      Processing line: lui     rd imm20 6..2=0x0D 1..0=3
DEBUG::      Processing line: auipc   rd imm20 6..2=0x05 1..0=3
DEBUG::      Processing line: jal     rd jimm20                          6..2=0x1b 1..0=3
DEBUG::      Processing line: jalr    rd rs1 imm12              14..12=0 6..2=0x19 1..0=3
DEBUG::      Processing line: beq     bimm12hi rs1 rs2 bimm12lo 14..12=0 6..2=0x18 1..0=3
DEBUG::      Processing line: bne     bimm12hi rs1 rs2 bimm12lo 14..12=1 6..2=0x18 1..0=3
```

## How do I find where an instruction is defined?

You can use `grep "^\s*<instr-name>" rv* unratified/rv*` OR run `make` and open
`instr_dict.yaml` and search of the instruction you are looking for. Within that
instruction the `extension` field will indicate which file the instruction was
picked from.

>>>>>>> d3fcce5c25ab2ed5343516175182de8357c57f07
