How to set up your dev environment (Windows-specific)
-------------------

Set up Git
=============
- Download and install Git for Windows: https://git-scm.com/download/win
- Choose Use Git from Git Bash only
- Checkout using Windows-style
- Chose Mintty

Install healthcareai via these instuctions: https://github.com/HealthCatalystSLC/healthcareai-py/blob/master/README.rst

Install the IDE and clone the healthcareai-py repo
=============

1)	Install PyCharm Community Edition

2)	Set path to git.exe via File -> settings -> Version Control -> Git

3)	Clone repo (if you haven't) via PyCharm -> VCS (at top) -> Checkout from version control -> Github
 - Grab .git url from HCRTools repo in Github
 - Set parent directory to C:/Source
 - Name directory healthcareai-py

4)	File -> Open and look for the healthcareai project (if it didn’t come up already)

5) Create a destination table for the test predictions by executing this in SSMS:

CREATE TABLE [SAM].[dbo].[HCPyDeployClassificationBASE] (
       [BindingID] [int] ,
       [BindingNM] [varchar] (255),
       [LastLoadDTS] [datetime2] (7),
       [PatientEncounterID] [decimal] (38, 0),
       [PredictedProbNBR] [decimal] (38, 2),
       [Factor1TXT] [varchar] (255),
       [Factor2TXT] [varchar] (255),
       [Factor3TXT] [varchar] (255))

CREATE TABLE [SAM].[dbo].[HCPyDeployRegressionBASE] (
       [BindingID] [int],
       [BindingNM] [varchar] (255),
       [LastLoadDTS] [datetime2] (7),
       [PatientEncounterID] [decimal] (38, 0),
       [PredictedValueNBR] [decimal] (38, 2),
       [Factor1TXT] [varchar] (255),
       [Factor2TXT] [varchar] (255),
       [Factor3TXT] [varchar] (255))
       
       
6)	Verify that unit tests pass
 - Right click on tests folder under healthcareai-py/healthcareai
 - Click on Run Nosetest in test

7)	Create test branch and push it to github
 - Note the text ‘Git: master’ in bottom-right of PyCharm
 - Create new test branch via VCS -> Git -> Branches -> New Branch
 - Push branch to github (ie, create origin) via VCS -> Git -> Push (CTRL-SHIFT-K)

Code Housekeeping
=============

1)	Install the following packages via the command line: ``python -m pip install packagename``
 - pylint
 - pyflakes
    
2) Set these up via http://www.mantidproject.org/How_to_run_Pylint#PyCharm_-_JetBrains
 - If your python is installed in C:\Pythonxx, then your parameters will be:
  - Program: C:\Python34\Scripts\pylint.exe
  - Parameters: $FilePath$
  - Working dir: C:\Python34\Scripts
 - If you are using a different Python distribution, you may need to find where Pylint is installed.  For example, the same three parameters from above might be:
  - C:\Users\user.name \AppData\Local\Continuum\Anaconda3\Scripts\pylint
  - Parameters: $FilePath$
  - C:\Users\david.healey\AppData\Local\Continuum\Anaconda3\Scripts

 - Instead of using default parameter, use $FilePath$
 - For Anaconda, you may have to use C:\Users\user.name \AppData\Local\Continuum\Anaconda3\Scripts\pylint
 - Check all boxes
    
3) Make sure pylint and pyflakes work
 - Right-click on relevant directory in PyCharm (this will be where you’ve done work)
 - Navigate to external tools
 - Run both pylint and pyflakes
 - Verify that there aren’t any issues with your code; please do this before sending pull requests

4) Set maximum line width to 79 via Settings -> Editor -> Code Style -> Right margin

5) Set tabs as spaces via Edit -> Convert Indents -> To Spaces

6) Click Code -> Inspect code -> Whole project -> Look for section on Package requirements
 - Under the lines related to sklearn, click ‘Ignore Requirement’

Git config
=============
Set up your email and username for git (otherwise no attribution in github)

1) Set git user name and work email
 - git config user.name "Billy Everyteen"
 -	git config --global user.email "your_email@example.com"

2) Configure line endings for windows: ``git config core.autocrlf true``

3) Make git case sensitive for file names: ``git config core.ignorecase false``

3) Set up SSH (if desired) so you can push to topic branch without password
 - `Step1`_
 - `Step2`_
 - `Step3`_
 
 .. _Step1: https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/
 .. _Step2: https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/
 .. _Step3: https://help.github.com/enterprise/11.10.340/user/articles/changing-a-remote-s-url/
