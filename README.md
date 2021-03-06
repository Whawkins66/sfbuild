sfbuild
=======

Advanced use of ANT, Salesforce Metadata API, DataLoader jars and more to facilitate Salesforce migrations

1) Allows you to build project templates (kind of maven like)
2) Then provides pre-built build.xml that can be extended to handle traditional Salesforce deployment activities through the metadata api (retrieve, deploy, etc) but also does a little more (automatically backup files on deploy, perform diffs). It also includes functionality to perform data loads through ANT by utilizing the Dataloader.jar.  

Combined, this allows you to more easily script your deployments (both metadata and data).

## Dependencies ##
Java and Ant

## Installation ##
1) Clone or download the repository to your local computer 
git clone https://github.com/timwatt/sfbuild.git
(I cloned it to ~/Code/tools/sfbuild)

2) On my Mac, I then link the main build.xml and "common" subdirectory to the root directory that I develop in as this allows me to keep this repository separate from my other code.
 ln  ~/Code/sfbuild/build.xml ~/Code/build.xml
 ln -s ~/Code/sfbuild/common ~/Code/common

## Project setup ##
ant create-new-project

Buildfile: ~/build.xml

create-new-project:
    [input] Project Name (no spaces):
client/client1
    [mkdir] Created dir: ~/client/client1
     [copy] Copying 6 files to 	~/client/client1
     [copy] Copied 6 empty directories to 5 empty directories under ~/client/client1

BUILD SUCCESSFUL
Total time: 14 seconds

## Daily Use ##
From the newly created projected folder you can run a variety of commands:
 * sf.retrieve: will perform normal metadata api retrieve from the selected package.xml
 * sf.diff: backups target files that are in package.xml and automatically runs diff to highlight changes
 * sf.check-deploy: runs sf.diff and then also does a metadata api deploy with checkOnly (ensure package is deployable), and run unit tests
 * sf.deploy-folder: runs sf.diff and then also does a metadata api deploy to target org


Also contains various targets for performing data loads, etc directly from ANT. This way you can build out a deployment script in ANT that deploys base objects, loads necessary reference data, then performs additional deploys as necessary.

