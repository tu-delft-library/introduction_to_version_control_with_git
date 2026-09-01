# PRACTICAL: Getting started with Collaboration

> Adapted from *Version Control with Git — Episode 8: Collaborating*, Software Carpentry / The Carpentries, licensed [CC-BY 4.0](https://swcarpentry.github.io/git-novice/LICENSE.html). 


## PART 0: Setting up 
### Pick your roles

Get into pairs. Decide who will be:

- **Partner A — the Owner.** This person's GitHub repository (e.g. the `recipes` repo from earlier episodes) will be the shared project.
- **Partner One — the Collaborator.** This person will clone the Owner's repository and contribute changes to it.

### Granting access (Partner A)

- On GitHub, navigate to your repository's page.
- Click **Settings → Collaborators → Add people**.
- Enter your partner's (Partner One's) GitHub username and send the invite.

**Partner One** should now check <https://github.com/notifications> or their email, and accept the invitation.

### Cloning the shared repository (Partner One)

- **Partner One** downloads a copy of **Partner A**'s repository.
- Since **Partner One** already has a local repo named `recipes`, clone into a **different folder** so the two don't collide

```bash
$ cd ~/Desktop
$ git clone git@github.com:<owner-username>/recipes.git recipes-<owner-username>
```

- Replace `<owner-username>` with **Partner A**'s GitHub username.

> ⚠️ **Watch out:** if you omit the destination path at the end of `git clone`, Git will clone into a folder matching the repo's name in your current directory — which may overwrite or collide with your own repo of the same name.

## PART 1: A new recipe 

### Making and sharing a change (Partner One)

- Move into the cloned repository:

   ```bash
   $ cd ~/Desktop/recipes-<owner-username>
   ```

- Create a new recipe file named `hummus.md`

   ```bash
   $ nano hummus.md
   ```
- Add the title and ingredients in the new file
   ```
   # Hummus
   ## Ingredients
   * chickpeas
   * lemon
   * olive oil
   * salt
   ```

- Save, stage and commit the change:

   ```bash
   $ git add hummus.md
   $ git commit -m "Add ingredients for hummus"
   ```

- Push the change back to the **Owner's** repository:

   ```bash
   $ git push origin main
   ```

   Note that you didn't need to create a remote called `origin` yourself — Git names it that automatically when you clone.

### Retrieving the change (Partner A)

Back on **Partner A**'s machine, pull down the new commit:

```bash
$ git pull origin main
```

Check the repository's commit history (`git log`, or refresh the GitHub page) — you should now see Partner One's commit.

At this point, three copies of the project are back in sync: the Owner's local repo, the Collaborator's local repo, and the copy on GitHub.

### Checkpoint discussion (both partners)

Before moving on, talk through this together:

> **The basic collaborative workflow** is: `git pull` → make changes → `git add` → `git commit -m` → `git push`. Why does it matter that you pull *before* you start editing, rather than only before you push? What could go wrong if you skip that first pull?


### Making and sharing another change (Partner A)

- Edit `hummus.md`

   ```bash
   $ nano hummus.md
   ```
- Add instructions after the `Ingredients` section
   ```
   ## Instructions
   Mix the ingredients together in a food processor.
   ```

- Save, stage and commit the change:

   ```bash
   $ git add hummus.md
   $ git commit -m "Add ingredients for hummus"
   ```

- Push the change back to your remote repository:

   ```bash
   $ git push origin main
   ```

### Retrieving the change (Partner One)

Back on **Partner One**'s machine, pull down the new commit:

```bash
$ git pull origin main
```

Check the repository's commit history (`git log`, or refresh the GitHub page) — you should now see Partner A's commit.

At this point, three copies of the project are back in sync: the Owner's local repo, the Collaborator's local repo, and the copy on GitHub.

---

## PART 2: Making the repository more FAIR

### Auditing the repository

Working with your partner, spend a few minutes auditing the `recipes` repository against the checklist below

| Principle | Ask yourselves... | Look for / add |
|---|---|---|
| **Findable** | Could a stranger discover this repository and understand what it is at a glance? | A descriptive repository name and description; a README with a clear title and one-sentence summary at the top |
| **Accessible** | Can someone actually get the files and understand how to obtain them? | The repo is public (or access is documented); clear clone/install instructions in the README |
| **Interoperable** | Does it play well with standard tools and formats, and is it clear what it depends on? | Listed dependencies/requirements; standard file formats and layout (e.g., `.md` for docs) |
| **Reusable** | Could someone else legally and practically reuse this? | A `LICENSE` file; a `CITATION.cff` (or citation section in the README) so people know how to credit the work; enough documentation to run it without asking you questions  |


As you have noticed there are a few quick wins you can do to make this repository more FAIR.

### Add a README

Make these changes as **Partner One** contribution, following the same workflow you just practiced:

- Pull from remote
- Create a `README.md` using `nano`
- Copy paste the template below
```
# Nana's recipes
[Modify the title above to make it more descriptive]

## Description
I often found myself searching over and over again for certain recipes. Sometimes I would find them. Sometimes I would not. 

So I decided to start a collection of my most beloved recipes for my *future-self* to enjoy that perfect guacamole.

These recipes have been tested under the following circumstances:
* Dinner for two
* Family birthday
* PhD graduation party

[Add to the list other circumstances to test the recipes]

## Requirements
- Kitchen
- Utensils
    - Bowls
    - Spoon
- Ingredients
    - Salt

[Complete the list of requirements. Use indented lists too.]

## How to install

Click on the desired .md file in GitHub to visualize online. 
Alternatively, clone this repository locally and use your favorite text editor to preview the .md file.

[Highlight .md words using `inline code` quotes]

## License
See the `LICENSE` file in this repository

## Copyright

Copyright (c) 2026, Technische Universiteit Delft

## Citation

Use the citation in the `CITATION.CFF` file to acknowledge this work.

## Acknowlegdements
- Nana
- Raul, my mexican friend

[Name anyone who has helped this project]

```
- Inside `nano`, check the suggestions between brackets [] and make changes accordingly. 
- Save, stage and commit the `README.md`
- Push to remote
- **Partner A** `git pull` the changes and confirm they appear on GitHub.

### Add a **LICENSE** file 
Make these changes as **Partner A** contribution
- Create a `LICENSE` file using nano
- Pick any open license text from https://choosealicense.com and paste it in.
- Inside `nano` replace:
    - `[year]` with the current year 
    - `[fullname]` with `Technische Universiteit Delft`
- Save, stage and commit the `LICENSE` file
- **Partner One** `git pull` the changes and confirm they appear on GitHub.
