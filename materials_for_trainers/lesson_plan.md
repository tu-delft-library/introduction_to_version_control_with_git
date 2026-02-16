## Land - 10'
☕ Coffee/tea 🫖

## Installation check, housekeeping - 15'
- ✅ Roll call + 🤝 Code of Conduct
- 🖥 Did everyone install git and VSCode 
- 🙋Getting help (🆘 red  ✅ green stickers)

## Icebreaker - 5'
A short icebreaker from [resources document](https://tud365.sharepoint.com/:w:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/resources.docx?d=waea671d7fc6a46d5b5c068fc19f41940&csf=1&web=1&e=f2QYgy)


## Introduction to version control - 10'
- 🎦 introduce git using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- What is version control and why should I use it?
  - Do it for your future self
  - your computer is dead. Your code lives on!
- How does git work -> `changesets` or `snapshots`
- What is a git repo: 
    - folder with files + subfolders + `.git` hidden folder

    

## File systems - 10'
- **File browser:** demo the actions that will be covered in directory navigation using the file browser. 
    - This visual explanation should make it easier when moving to the shell.
- Explain concept of `home`
- Explain meaning of slash at the end `/`

## Symbolic link to Desktop - 10'

- Users with Windows 10 will probably save the data in `OneDrive` Desktop.  
    - First make a symolic link to make our lives easier.
    - `ln -s "/c/Users/[username]/OneDrive\ -\ Delft\ University\ of\ Technology\Desktop" "Desktop"`
    - Explain how **how spaces need special handling**

## Navigating Files and Directories

### Type along - 20'
```
pwd # (Print working directory)
ls –help  # (Ask for help about the 'ls' command) (Windows / Git-bash)
man ls  # Show the UNIX manual page for the 'ls' command (Mac / Linux)
clear # Clears the terminal screen
ls -l -h  # Long-form listing of the files in the current directory
ls -F # for MAC 
ls -F . # . means the current directory
ls -F Desktop
ls -F Desktop/shell-lesson-data
cd Desktop # Change directory to the one called "Desktop"
cd shell-lesson-data
cd exercise-data
pwd
cd shell-lesson-data # Error: no such directory
cd .. # .. means the directory above the current one
pwd
ls -a # list all files, including hidden files
cd ~
```

### Challenges `filedir` - 10'
- go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- start poll -> wait for answers -> discuss -> next question

## Break - 10'

## Working with Files and Directories
- Talk about **good names for files and directories**
- Explain: create files with `touch`

### Type along - 25'

```
pwd
cd ~/Desktop/shell-lesson-data/exercise-data/writing
ls -F
mkdir thesis
ls -F thesis # Empty directory
mkdir thesis # Directory already exists
cd thesis/
nano draft.txt # Edit the file draft.txt
touch my_file.txt # Create an empty file my_file.txt
ls
cat my_file.txt # Show the contents of a file
rm my_file.txt
ls
mv thesis/draft.txt thesis/quotes.txt # Move / rename a file
ls thesis/
mv thesis/quotes.txt .
ls
ls thesis/
cp quotes.txt thesis/quotations.txt # Copy file to a different location / name
ls thesis/
ls
cat thesis/quotations.txt
cp -r thesis/ thesis_backup # Copy recursively – will copy folder structures
ls thesis_backup/
rm -r thesis_backup/ # Remove contents and folder
```

### Challenges `create` - 10'

- continue with the same vevox
- start poll -> wait for answers -> discuss -> next question

## Using wildcards (*,?) to access multiple files

### Type along - 10'
```
clear
cd ..
cd alkanes
ls
ls *.pdb
ls p*.pdb
ls ?ethane.pdb
ls ???ane.pdb
ls *.pdf # No such file or directory
clear
```

### Challenges `wildcards` - 15'

- continue with the same vevox
- start poll -> wait for answers -> discuss -> next question

## Key points - 15'
* use the cheat sheet to make sure you revise all the commands


## Feedback - 5'
* ask participants to fill in the feeback survey