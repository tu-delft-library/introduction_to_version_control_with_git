# Optional Exercises

These are additional exercises for you to play with 🙂

## 1: Committing Multiple Files
When you make changes, they often belong together as one logical improvement. Git lets you group related edits into a single commit so your project stays consistent. This is something word processors can’t easily do—each suggestion is separate, even if they depend on each other.

The staging area can hold changes from any number of files that you want to commit as a single snapshot.

- Add some text to `guacamole.md` noting the rough price of the ingredients.
- Create a new file `groceries.md` with a list of products and their prices for different markets.
- Add changes from both files to the staging area and commit those changes.

## 2: Getting Rid of Staged Changes
`git restore` can be used to restore a previous commit when unstaged changes have been made, but will it also work for changes that have been staged but not committed? 

Make a change to `guacamole.md`, add that change using `git add`, then use `git restore` to see if you can remove your change.

## 3: Ignoring all data Files in the repository
Let us assume you have many `.csv` files in different subdirectories of your repository. For example, you might have:

```console
results/a.csv
data/experiment_1/b.csv
data/experiment_2/c.csv
data/experiment_2/variation_1/d.csv
```
How do you ignore all the `.csv` files, without explicitly listing the names of the corresponding folders?

## 4: The Order of Rules
Given a `.gitignore` file with the following contents:

```console
*.csv
!*.csv
```
What will be the result?
