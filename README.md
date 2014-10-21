# Digital Preservation Toolkit

*Installing Digital Preservation Tools was never so easy.*

## What does Digital Preservation Toolkit do?

The Digital Preservation Toolkit is a Debian metapackage, called digital-preservation-tools, and allows to easily install Digital Preservation tools. It does that by referencing three other metapackages:
* Migration (digital-preservation-tools-migration)
* Characterisation (digital-preservation-tools-characterization)
* Quality Assurance (digital-preservation-tools-quality-assurance)

Using these metapackages one may install all the tools (by installing digital-preservation-tools) or a specific set of related tools (by installing the one of the digital-preservation-tools-* packages).
Each of the metapackages (Migration, Characterisation and Quality Assurance) references tools wrapped with [SCAPE Toolwrapper](https://github.com/openplanets/scape-toolwrapper), in the form of Debian packages.

### Using it

#### Pre-requisites
Debian/Ubuntu system.

#### How to add OPF Debian repository
Add repository key
```bash
$> wget -O - http://ubapt.opf-labs.org/scape-components.gpg.key | sudo apt-key add -
```
Add repository information, by editing file /etc/apt/source.list and adding the following line to the end of the file
```
deb http://ubapt.opf-labs.org precise main
```
Update packages information
```bash
$> sudo apt-get update
```

#### Install Digital Preservation Toolkit
```bash
$> sudo apt-get install digital-preservation-tools
```

#### Install only tools related to Migration
```bash
$> sudo apt-get install digital-preservation-tools-migration
```

#### Install only tools related to Characterisation
```bash
$> sudo apt-get install digital-preservation-tools-characterisation
```

#### Install only tools related to Quality Assurance
```bash
$> sudo apt-get install digital-preservation-tools-quality-assurance
```

#### List all Digital Preservation Toolkit packages
```bash
$> sudo apt-cache search --names-only '^digital-preservation-'
```

#### Execute installed wrapped tool (for example for package digital-preservation-migration-image-imagemagick-image2txt). Providing no parameters cause the bash wrapper to show the usage message
```bash
$> digital-preservation-migration-image-imagemagick-image2txt
```

### Compiling it

#### Pre-requisites

1. Debian/Ubuntu system
2. Build tools (Debian packaging)
    * ```$> sudo apt-get install build-essential dh-make devscripts debhelper lintian```
3. Clone of Digital Preservation Toolkit github repository
    * ```$> git clone https://github.com/openplanets/digital-preservation-toolkit.git```

#### Project directory structure

* _**sources**_ folder with all source files
  * **metapackages** source files for the metapackages
    * **digital-preservation-tools** main metapackage
    * **digital-preservation-tools-characterisation** characterisation metapackage
    * **digital-preservation-tools-migration** migration metapackage
    * **digital-preservation-tools-quality-assurance** quality assurance metapackage
  * **others** source files for other packages (binary packages)
* **LICENSE.txt**
* _**README.md**_ 

#### How to edit and compile a metapackage (e.g. digital-preservation-tools)

In this example, one is editing the main metapackage and adding a new dummy package called **xpto** as dependency (besides the already present dependencies). Here $DPT\_GITHUB\_FOLDER denotes the path to the folder where the Digital Preservation Toolkit repository was cloned into.
```bash
$> cd $DPT_GITHUB_FOLDER/
$> cd sources/metapackages/digital-preservation-tools/digital-preservation-tools_1.0.0/
```
Edit file **debian/control** and replace the line 
```
Depends: ${misc:Depends},digital-preservation-tools-characterisation,digital-preservation-tools-migration,digital-preservation-tools-quality-assurance
```
by
```
Depends: ${misc:Depends},digital-preservation-tools-characterisation,digital-preservation-tools-migration,digital-preservation-tools-quality-assurance,xpto
```
**Note:** Please see the differences by analyzing the end of both lines.

Now, don't forget to increment the package version. To do that, edit file **debian/changelog** (as Debian processes this file to set package version) and add the following to the top of the file (assuming that previous version was 1.0.0):
```
digital-preservation-tools (1.1.0) unstable; urgency=low

  * Added xpto as a dependency

 -- Hélder Silva <hsilva@keep.pt>  Mon, 21 Jul 2014 15:31:38 +0100
```

After this changes, run the following command to generate the Debian package:
```bash
$> dpkg-buildpackage -us -uc
```

Go up one folder and notice the newly created files:
```bash
$> cd .. ; ls -lgG
total 20
drwxrwxr-x 3 4096 Jul 21 15:29 digital-preservation-tools_1.0.0
-rw-r--r-- 1 1400 Jul 21 15:38 digital-preservation-tools_1.1.0_all.deb
-rw-rw-r-- 1 1371 Jul 21 15:38 digital-preservation-tools_1.1.0_amd64.changes
-rw-rw-r-- 1  607 Jul 21 15:38 digital-preservation-tools_1.1.0.dsc
-rw-rw-r-- 1 1116 Jul 21 15:38 digital-preservation-tools_1.1.0.tar.gz
```

## More information

### Licence

Digital Preservation Toolkit is released under [Apache version 2.0 license](LICENSE.txt).

### Acknowledgements

This work was partially supported by the [SCAPE project](http://scape-project.eu). The SCAPE project is co-funded by the European Union under FP7 ICT-2009.4.1 (Grant Agreement number 270137)

### Contribute

1. [Fork the GitHub project](https://help.github.com/articles/fork-a-repo)
2. Change the code and push into the forked project
3. [Submit a pull request](https://help.github.com/articles/using-pull-requests)

To increase the changes of you code being accepted and merged into the official source here's a checklist of things to go over before submitting a contribution. For example:

* Has unit tests (that covers at least 80% of the code)
* Has documentation (at least 80% of public API)
* Agrees to contributor license agreement, certifying that any contributed code is original work and that the copyright is turned over to the project
