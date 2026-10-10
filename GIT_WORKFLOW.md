# Git and GitHub workflow

Repository: https://github.com/dkmanenzhe/Msc_Stats_and_Data_Science
Website: https://dkmanenzhe.github.io/Msc_Stats_and_Data_Science/

Run the commands below in a terminal (the RStudio Terminal tab works) inside the
repository folder.

## 1. First push (Dakalo)

The local folder is already connected to the GitHub repository (`origin`, branch `main`).
`.gitignore` keeps earlier versions of the assignment out of the repository, so this adds
only the current project:

```bash
git add .
git status            # check: the .qmd, _quarto.yml, data/, results/, images/, docs/ ... and nothing else
git commit -m "Add report, analysis code and rendered website"
git push -u origin main
```

If `git push` reports that the remote already has commits, run `git pull --rebase origin main`
first, then push again.

## 2. Give Troy access (Dakalo)

GitHub repository → **Settings → Collaborators → Add people** → Troy's GitHub username.

## 3. Turn on GitHub Pages (Dakalo)

**Settings → Pages → Build and deployment → Source: Deploy from a branch**, branch `main`,
folder `/docs`. After a minute or two the site is live at the address above.

GitHub Pages works on a **public** repository with a free account. For a private
repository you need GitHub Pro, which is free for students through the GitHub Student
Developer Pack. If the repository is private and you do not have Pro, make it public under
**Settings → General → Danger Zone → Change visibility**.

## 4. Get a copy (Troy)

```bash
git clone https://github.com/dkmanenzhe/Msc_Stats_and_Data_Science.git
cd Msc_Stats_and_Data_Science
```

## 5. Every change: branch, commit, pull request (both)

Work on a branch, never directly on `main`. For example, to revise the Siamese section:

```bash
git switch main
git pull                              # start from the latest version
git switch -c siamese-section         # new branch with a descriptive name
# ... edit STA5073Z_Assignment2.qmd ...
quarto render                         # rebuild docs/ so the website matches
git add STA5073Z_Assignment2.qmd docs/
git commit -m "Revise Siamese pair construction discussion"
git push -u origin siamese-section
```

On GitHub, open a **pull request** from `siamese-section` into `main`. The other person
reviews it (comments or approves) and merges it. Then both run:

```bash
git switch main
git pull
```

The website updates automatically once the merged `docs/` folder is on `main`.

## 6. When both of you edit the same file

Git merges changes to different parts of the `.qmd` automatically. If two branches change
the same lines, the pull request shows a conflict. To resolve it:

```bash
git switch your-branch
git pull origin main
# open the .qmd and keep the right text between the <<<<<<< and >>>>>>> markers
quarto render
git add STA5073Z_Assignment2.qmd docs/
git commit -m "Resolve merge conflict with main"
git push
```

## Notes

- Always run `quarto render` before committing, so `docs/` matches the `.qmd`.
- `git push` is the programmatic publishing the brief asks for; do not upload files
  through the GitHub web page.
- `models/` is not committed; `quarto render -P retrain:true` recreates it.
