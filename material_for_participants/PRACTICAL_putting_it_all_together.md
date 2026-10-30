# PRACTICAL - Putting it all together
## Setup

We will continue working in the `free_fall` repository from the in person workshop.

- Open a terminal and navigate to your `free_fall` repository (it should be on your `Desktop`)
- Check that everything is in order:

```
git status
git remote -v
git log --oneline
```

`git status` should say `nothing to commit, working tree clean`, and `git remote -v` should show your GitHub repository as `origin`.

If something is off (the folder is missing, or the repo is a mess), jump to **⚠️Solution to start this PRACTICAL⚠️** at the bottom of this page and come back.


<details>
<summary>🔍 Click here for hints! </summary>

- To go to your Desktop use `cd ~/Desktop` (on some Windows setups the path to your Desktop is different, use the same path as in the workshop)
- To see which folder you are in use `pwd`
</details>

## Working directory → staging → history

- Create `energy.py` in `nano` and add:
    - a comment describing the purpose of the script
    - the mass of an object in kilograms
    - the velocity in meters per second
```
# Kinetic energy in Joules given mass and velocity
mass = 2.0
velocity = 5.0
```
- Check `status`, then stage and commit it with the message `Add energy.py with mass and velocity`
- Open `energy.py` in `nano` and add:
    - a third line with the kinetic energy formula
    - a fourth line that prints the result
```
kinetic_energy = 0.5 * mass * velocity ** 2
print(kinetic_energy)
```
- Run the script. The kinetic energy should be 25.0.
- Run `diff` to see the *unstaged* changes
- Stage the file
- Run `diff` again. Notice it shows nothing (all staged changes are compared differently, use `diff --staged`)
- Commit with the message `Implement kinetic energy formula`
- Open `energy.py` in `nano` and change the fourth line to be more human readable
```
print("The kinetic energy of an object with mass", mass ,"k and velocity", velocity, "m/s is", kinetic_energy,"J")
```
> ⚠️ **Watch out:** Make sure there are not double quotes `"` between the variables  (mass, velocity, kinetic_energy) and the commas `,`
- Run `diff` to see the *unstaged* changes
- Stage and commit with the message `Show result in human readable format`
- Run the script. The result should show human friendly text around the number 25.0

You should now have 3 new commits. Run `git log --oneline` to confirm.

<details>
<summary>🔍 Click here for hints! </summary>

- To create or edit a file use `nano name_of_file`
- To stage file use `git add name_of_file`
- To commit a file use `git commit -m "commit message"`
- To see the changes in the working directory use `git diff name_of_file`
- To see changes in the staging area use `git diff --staged name_of_file`
</details>

## Time travel: restoring old versions
- Run `status` to make sure there are changes in your working directory
- Look at your history with `log --oneline`
- Use `show HEAD` to view the previous commit
- Deliberately break the file: open `energy.py` in nano, delete the second line (definition of mass)
- Run the script and notice that Python gives an error.
- Run `diff` to see the *unstaged* changes
- Use `restore` to bring back the last **committed** version (discard your uncommitted edit)
- Run the script. The script should print the whole human readable sentence `The kinetic energy ...` like it did before.
- Now go back further: restore `energy.py` as it existed at `HEAD~1` into your working directory
- Run the script. The script should only show the number `25.0` no text around it.
- Run `diff` to see the *unstaged* changes
- Actually, we prefer the human readable version. Restore back to the latest version.
- Run the script. The script should print the whole human readable sentence `The kinetic energy ...` like it did before.

<details>
<summary>🔍 Click here for hints! </summary>

- To restore a file to the latest commit use `git restore name_of_file`
- To restore a file to a SPECIFIC commit use `git restore -s HEAD~[#] name_of_file` or `git restore -s [hash] name_of_file`
</details>

## Keep it clean

We will soon produce files that should not be tracked: log files and raw data.

- Run `status` to make sure there are changes in your working directory
- Create a new empty file named `debug.log`
- Make a new directory named `data`
- Inside the directory `data` add two files: `raw.csv` and `output.csv`
- Run `status` and notice that Git wants to track them
- Open your `.gitignore` file  with nano (it already exists from the in person session)
- Add a rule at the bottom to ignore all `log` files
- Add a rule at the bottom to ignore everything inside `data/`
- Confirm with `status` that the `log` and `data` files are ignored (only `.gitignore` should be listed as modified)
- Stage and commit the `.gitignore` file with the message `Ignore log and data files`

<details>
<summary>🔍 Click here for hints! </summary>

- To create an empty file use `touch name_of_file`
- To create a new folder use `mkdir name_of_folder`
- Use the wildcard `*.extension` to indicate all files with a specific extension (e.g. csv, log, png, pdf)
- Use wildcard `name_of_directory/` to indicate all files inside a directory
- To check the status of the local git repo use `git status`
</details>

## Push to the remote

Your GitHub repository already exists, so we only need to send the new commits.

- Push your commits to `origin`
- Refresh the GitHub page and confirm that `energy.py` and all 4 new commits made it across
- Run `git status` and confirm that your branch is up to date with `origin/main`

You are done! Your history should now look like this (hashes will differ, and you will have more commits from yesterday below):

```
xxxxxxx (HEAD -> main, origin/main) Ignore log and data files
xxxxxxx Show result in human readable format
xxxxxxx Implement kinetic energy formula
xxxxxxx Add energy.py with mass and velocity
...
```
<details>
<summary>🔍 Click here for hints! </summary>

- To push to a remote repository use `git push origin main`
- To see the status relative to the remote use `git status`
</details>


---

## ⚠️Solution to start this PRACTICAL⚠️

If for some reason the repository got messy and confusing, you can rebuild the starting point for this PRACTICAL from scratch.

Navigate to your `Desktop`. If a `free_fall` folder already exists, rename it first with `mv free_fall free_fall_old`.

Copy and paste the commands below in your terminal according to your operating system:

<details>
<summary>🔍 MacOS/Linux </summary>

```
mkdir free_fall
cd free_fall/
git init
echo "# Distance that an object free falls during a given time" > distance.py
echo "gravity = 9.81" >> distance.py
echo "time = 5" >> distance.py
git add distance.py
git commit -m "Add distance.py with variables"
echo "distance = 0.5 * gravity * time ** 2" >> distance.py
echo "print(distance)" >> distance.py
git add distance.py
git commit -m "Implement free fall distance formula"
git tag -a formula HEAD -m "First working version"
sed -i '' 's/print(distance)/print(\"After\", time,\"s the free fall distance on Earth is\", distance, \"m\")/g' distance.py
git add distance.py
git commit -m "Make output human readable"
echo "*.png" > .gitignore
echo "plots/" >> .gitignore
git add .gitignore
git commit -m "Ignore png files and plots folder"
sed -i '' 's/9.81/1.62/g' distance.py
sed -i '' 's/Earth/Moon/g' distance.py
git add distance.py
git commit -m "Use Moon gravity"
echo "# Time for an object to free fall from a given height" > time.py
echo "gravity = 9.81" >> time.py
echo "height = 10" >> time.py
git add time.py
git commit -m "Add constants for free fall time"
echo "import math" >> time.py
echo "time = math.sqrt(2 * height / gravity)" >> time.py
echo 'print("An object dropped from", height, "m reaches the ground after", time, "s")' >> time.py
git add time.py
git commit -m "Add free fall time calculation"
sed -i '' 's/time,/time_round,/g' time.py
sed -i '' '/^print/i\
time_round = round(time, 2)
' time.py
git add time.py
git commit -m "More readable rounded time value"
touch README.md LICENSE
git add README.md LICENSE
git commit -m "Add README and LICENSE"
```
</details>

<details>
<summary>🔍 Windows Git bash </summary>

```
mkdir free_fall
cd free_fall/
git init
echo "# Distance that an object free falls during a given time" > distance.py
echo "gravity = 9.81" >> distance.py
echo "time = 5" >> distance.py
git add distance.py
git commit -m "Add distance.py with variables"
echo "distance = 0.5 * gravity * time ** 2" >> distance.py
echo "print(distance)" >> distance.py
git add distance.py
git commit -m "Implement free fall distance formula"
git tag -a formula HEAD -m "First working version"
sed -i 's/print(distance)/print("After", time, "s the free fall distance on Earth is", distance, "m")/g' distance.py
git add distance.py
git commit -m "Make output human readable"
echo "*.png" > .gitignore
echo "plots/" >> .gitignore
git add .gitignore
git commit -m "Ignore png files and plots folder"
sed -i 's/9.81/1.62/g' distance.py
sed -i 's/Earth/Moon/g' distance.py
git add distance.py
git commit -m "Use Moon gravity"
echo "# Time for an object to free fall from a given height" > time.py
echo "gravity = 9.81" >> time.py
echo "height = 10" >> time.py
git add time.py
git commit -m "Add constants for free fall time"
echo "import math" >> time.py
echo "time = math.sqrt(2 * height / gravity)" >> time.py
echo 'print("An object dropped from", height, "m reaches the ground after", time, "s")' >> time.py
git add time.py
git commit -m "Add free fall time calculation"
echo "# Time for an object to free fall from a given height" > time.py
echo "gravity = 9.81" >> time.py
echo "height = 10" >> time.py
git add time.py
git commit -m "Add constants for free fall time"
echo "import math" >> time.py
echo "time = math.sqrt(2 * height / gravity)" >> time.py
echo 'print("An object dropped from", height, "m reaches the ground after", time, "s")' >> time.py
git add time.py
git commit -m "Add free fall time calculation"
sed -i 's/time,/time_round,/g' time.py
sed -i '/^print/i time_round = round(time, 2)' time.py
git add time.py
git commit -m "More readable rounded time value"
touch README.md LICENSE
git add README.md LICENSE
git commit -m "Add README and LICENSE"

```
</details>



## ⚠️Solution to solve this PRACTICAL ⚠️


<details>
<summary>🔍 MacOS/Linux </summary>

```
cd ~/Desktop/free_fall
echo "# Kinetic energy in Joules given mass and velocity" > energy.py
echo "mass = 2.0" >> energy.py
echo "velocity = 5.0" >> energy.py
git add energy.py
git commit -m "Add energy.py with mass and velocity"
echo "kinetic_energy = 0.5 * mass * velocity ** 2" >> energy.py
echo "print(kinetic_energy)" >> energy.py
git add energy.py
git commit -m "Implement kinetic energy formula"
git tag -a formula HEAD -m "First working version"
sed -i '' 's|print(kinetic_energy)|print("The kinetic energy of an object with mass", mass, "k and velocity", velocity, "m/s is", kinetic_energy, "J")|g' energy.py
git add energy.py
git commit -m "Show result in human readable format"
echo "*.log" > .gitignore
echo "data/" >> .gitignore
git add .gitignore
git commit -m "Ignore log and data files"
```
</details>

<details>
<summary>🔍 Windows Git bash </summary>

```
echo "# Kinetic energy in Joules given mass and velocity" > energy.py
echo "mass = 2.0" >> energy.py
echo "velocity = 5.0" >> energy.py
git add energy.py
git commit -m "Add energy.py with mass and velocity"
echo "kinetic_energy = 0.5 * mass * velocity ** 2" >> energy.py
echo "print(kinetic_energy)" >> energy.py
git add energy.py
git commit -m "Implement kinetic energy formula"
git tag -a formula HEAD -m "First working version"
sed -i 's|print(kinetic_energy)|print("The kinetic energy of an object with mass", mass, "k and velocity", velocity, "m/s is", kinetic_energy, "J")|g' energy.py
git add energy.py
git commit -m "Show result in human readable format"
echo "*.log" > .gitignore
echo "data/" >> .gitignore
git add .gitignore
git commit -m "Ignore log and data files"
```
</details>

The above script should generate a local repository with a commit history. But you still need to add the remote repository:

- Create a new empty repository on GitHub called `free_fall` (no README/license, you already have those). If you already have one with that name, delete it on GitHub first (Settings, at the bottom of the page) or pick another name.
- Connect your local repo to it and push all your commits.

```
git remote add origin git@github.com:<your-user-name>/free_fall.git
```

Replace `<your-user-name>` with your GitHub user name

```
git remote -v
git push origin main
```

- Refresh the GitHub page and confirm every file and all commits made it across.
