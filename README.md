# Automatic changelog generation

## Concept
### What is all about
- keepachangelog.com
- [gitchangelog](https://pypi.python.org/pypi/gitchangelog)
- [cheatsheet for current implementation](https://raw.githubusercontent.com/epfl-idevelop/gitchangelog.rc/master/cheatsheet_gitchangelog.pdf) (from https://www.cheatography.com/)


### How to Git Tag
*major*.*minor*.*patch*[-*prerelease*][+*build*]

`[0-9]+\.[0-9]+(\.[0-9]+)?(-.+.*)?(\+.+.*)?`

#### Valid Tag examples
    0.6
    0.0.1
    1.0.0
    1.1.2
    2.1.2-beta1
    1.0.0-alpha
    1.0.0-rc.2
    1.0.0+build.3.ea34fd5c
    1.0.0-beta.3+build.20.f42cbd56

### rules of thumb

- Add `user:` or `usr:` to your commit message to appear in `CHANGELOG.md`, but don't use any tag
- at least, First the action (`new:`, ...), then the audience (`user:`, ...)
- Every log between last tags (and only last two tags) are changelogged to a specific version. So you won't lose your current changelog, the new informations are added to the current.
- The "unreleased" section is dynamically generated for what is not tagged. So you can merge pull requests without any fear, the changelog should manage it.

## Install

`pip install gitchangelog pystache`

## Integration

How to make it work with your repository ?

### Prerequiste

- a file named `CHANGELOG.md` in your root folder of the repository
- at least one tag and his description in the `CHANGELOG.md` ([look here for inspiration](https://raw.githubusercontent.com/jdelasoie/gitchangelog.rc/03e5e8a3d8d5748ebcc39b9cdeafaadba2f20d94/CHANGELOG.md))

- have the .gitchangelog.rc in the root folder. Please choose your method :
    - by getting as a static file
      `curl -sSL https://raw.githubusercontent.com/jdelasoie/gitchangelog.rc/master/.gitchangelog.rc`
    - by using [a git submodule link](https://stackoverflow.com/questions/7597748/linking-a-single-file-from-another-git-repository)
    ```git submodule add git@github.com:jdelasoie/gitchangelog.rc.git .gitchangelog
    ln -s .gitchangelog/.gitchangelog.rc .gitchangelog.rc
    ```

## Usage
After committing, go into your project folder and run
`gitchangelog`

### without a tag
it may be nice to keep the new generated version of the changelog by doing a
`git add CHANGELOG.md && git commit -m "chg: pkg: Update changelog"`

Everything that is not between a tag will be put in the "Unreleased" section.

### with a tag
Say you are happy with the state of the last commit and want to tag it. If you want to include the changed changelog into the tag, do
```
git tag x.x
gitchangelog
git add CHANGELOG.md && git commit -m "chg: pkg: Update changelog post tagging"
git tag --delete x.x
git tag x.x
```

## Commit message format
`ACTION: [AUDIENCE:] COMMIT_MSG [!TAG ...]`

### Examples
```
new: usr: support of git implemented
chg: re-indentend some lines !cosmetic
fix: pkg: updated year of licence coverage.
new: test: added a bunch of test around user usability of feature X.
fix: typo in spelling my name in comment. !minor
```

### ACTION
What the change is about
#### `new:`
for new features, big improvement

#### `chg:`
for refactor, small improvement, cosmetic changes...

#### `fix:`
for bug fixes

### AUDIENCE

#### `usr:` or `user:`
for final users (UI changes). The only audience that are changelogged at the moment.

#### `dev:`
for developpers (API changes, refactors...)

#### `pkg:`
packaging changes

#### `test:`
test only related changes

#### `doc:`
doc only changes

### TAG

Adding useful informations to your messages and making it invisible

#### `!refactor`

for refactoring code only

#### `!minor`

for a very meaningless change (a typo, adding a comment)

#### `!cosmetic`

for cosmetic driven change (re-indentation, 80-col...)

#### `!wip`

for partial functionality but complete subfunctionality

## Example
[From mediatheque changelog](https://github.com/epfl-idevelop/site-diffusion-mediatheque/blob/feature/gitchangelog/CHANGELOG.md)
or
[from gitchangelog project, "sample" part](https://pypi.python.org/pypi/gitchangelog)
