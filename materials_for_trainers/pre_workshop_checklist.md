# Pre-workshop checklist

## Branch
- Make a branch of this repository using the date format `yyyy-mm-dd`
- Do any modifications to files of this repo only on that branch
- Clear the `material_for_participants/command.log` file
- Make an [edu.nl](https://edu.nl/) link to point to `material_for_participants` folder of the new branch

## Prepare de vevox
- Ask @catactg for a duplicate of the vevox material and share it with you
- You will display the vevox meeting id during the workshop so that participants can join

## `Links` document
- Update the `links.md` file with any links participants will need.
- Currently we are using good-old pen and paper for roll call. So the current file does not need updating per workshop run.
- [OPTIONAL] If you have a feedback survey for this workshop, paste the link in `links.md`

## Slides
- Update the [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b)
    - Names of trainers/helpers
    - Modify schedule (if needed)
    - Modify the `edu.nl` link

## Lesson prep

- Practice teaching the material on your own (see [lesson plan spreadsheet](https://tud365.sharepoint.com/:x:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/lesson_plan.xlsx?d=we808cfe275964b25a61e1fa97fc31664&csf=1&web=1&e=tugbJr&nav=MTVfe0NGRTdFMkI5LUNEMzQtNDExRC1BQjhFLUUyMjcwMDJGMTdEMX0) for links to content)

- Prepare a separate device to have during the lesson.
    - Use it to visualize `materials_for_trainers/lesson_plan.md` file (in this repo).
    
- HEAD/TAG game:
    - Bring physical objects to be passe around (e.g. balls, fruits)
    - Prepare 2 papers per row with git short hashes (e.g.f22b25e, b36abfd) and tags (e.g. basic, spicy)

- Print a list of the participants for roll call 

## Set up autopush for live coding

- Clone the https://github.com/tu-delft-library/introduction_to_version_control_with_git repository to a `<local-repo-directory>`
- History will be saved to `material_for_participants/command.log`
- Bash doesn't automatically save the history. Set it up by adding this command to `~/.bashrc`
    ```bash
    PROMPT_COMMAND='history -a'
    ```
- On workshop day, you need to **START AUTOPUSH**. Instructions can be found in `materials_for_trainers/lesson_plan.md`
- Original instructions on setting up autopush can be found[here](https://github.com/4TUResearchData-Carpentries/workshop_notes)

## Clean up your system
- Delete the `recipes` repo from your github
- Delete `recipes` and `bio` from your `Desktop`
- Reset all global configurations by deleting the global configuration file:
```bash
rm ~/.gitconfig
```
- If you are using a mac, make the terminal not transparent: 
    - Open the terminal
    - Open settings
    - Go to background color
    - Adjust opacity to 100%
    
- Set your desktop to a color background instead of an image that can be distracting (e.g. a beach or a mountain)
