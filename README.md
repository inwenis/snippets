# F#
```fs
#r "nuget: FSharp.Data, 3.3.3"
#r "nuget: DiffSharp-lite, 1.0.0-preview-328097867"
#load "Utils.fs"

// {<interpolationExpression>[,<alignment>][:<formatString>]}
let x = 1
printfn "|%-10s|%-10s|" "a" "b"
printfn "%8i" x   // use 8 characters
printfn $"{x:D8}" // use 8 characters, start with 0s
printfn "%08i" x  // use 8 characters, start with 0s
printfn "%8.4f"  1.12 // use 8 characters (the decimal dot counts too), 4 digits after the dot
printfn "%08.4f" 1.12 // use 8 characters (the decimal dot counts too), 4 digits after the dot, start with 0s
//|a         |b         |
//       1
//00000001
//00000001
//  1.1200
//001.1200

let n = 1_000_000
printfn $"{n:N0}" // 1,000,000
fsi.AddPrinter<DateTimeOffset>(fun dt -> dt.ToString("O"))

// tip: pin your nugets in .fsx to avoid being confused when you suddenly get a never version and sth doesn't work

let s = p.WaitForXPathAsync("//a/span[contains(text(),'Payments')]/..", opt).Result
    -> get nodes parent xpath
s.GetPropertyAsync("tagName").Result
    -> get tag name in puppeteer

type ThisWillBeAClass() =
    member this.GetOnlyProperty = 123

```

```fs
module TopLevelModule // top level module needs no = sign
// modules become static classes (sealed classes with private constructors)

let topLevelModuleFun () = ... // no need for indentations here :)

module NestedModule =
    let nestedModuleFun () = ...
```

```fs
namespace TopLevel

module ModuleName =
    let moduleFun () = ... // we need indentations here since we started with a namespace
```

```fs
// paket

// ^-paket.dependencies
// ^-paket.lock
// ^-proj folder A
//     ^-paket.references
// ^-proj folder B
//     ^-paket.references

// I have experienced issues with paket when paket.references was in the same dir as paket.dependencies and paket.lock
```

# PowerShell
```powershell
Get-item "somefile.txt" | format-list show all properties of a object

# Powershell tee output to a file but preserve colors in console
Start-Transcript out.log
# Run your app here
Stop-Transcript

Get-content -tail 20 -wait path/to/file/here
Get-EventLog application -Newest 1 | clip -> get stuff to clipboard awesome!
# source: https://blogs.technet.microsoft.com/heyscriptingguy/2014/06/15/powertip-send-output-to-clipboard-with-powershell/
```

# paket
```PowerShell
dotnet paket add Microsoft.AspNetCore.Http --project .\src\proj.fsproj # add package
dotnet paket install                                                   # install packages

# paket - github tokes
# https://github.com/settings/tokens -> here you can generate tokes
dotnet paket config add-token github_token ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
# tokens are stored here
C:\Users\inwen\AppData\Roaming\Paket\paket.config

# paket - install a github file
# https://fsprojects.github.io/Paket/github-dependencies.html
Add file in paket.dependencies and paket.references
# update github dependencies
# --filter makes paket interpret <package id> as a regex
dotnet paket update <package id> --filter
dotnet paket update github       --filter
```

# docker
```shell
docker build --build-arg ARG_NAME=value .
docker build --build-arg ARG_NAME=value -t tagGoesHere .

docker images
docker stop
docker restart
docker container ls = docker ps
docker logs a5 -> show logs from container a5...

docker run -it -p 8080:8080 myapp:tag1
docker run -it --entrypoint sh container-reg/name:latest
docker run -it --env-file c:/stuff/env.txt name:latest
    File looks like this:3
        env_var_name=123
        env_var_name=123
        env_var_name=123
        env_var_name=123
        env_var_name=123
        env_var_name=123
        env_var_name=123

docker run -p 8080:8080 ...
    Docker forwards requests from host:8080 -> container:8080

docker run -d -p 5432:5432 --name my-postgres -e POSTGRES_PASSWORD=mysecretpassword postgres

# https://stackoverflow.com/a/45359452/2377787
# delete stopped containers
docker container prune
```

# git
```
git diff master...feature - show what feature has added since it branched of from master
=
git diff $(git merge-base master feature) feature
  git diff <commit>...<commit> - any of <commit> can be omitted and will be replaced by HEAD
    git diff master...feature
    =
    git checkout master
    git diff ...feature
    https://git-scm.com/docs/git-diff#Documentation/git-diff.txt-gitdiffoptionscommitcommit--path-1
```


# misc
```
SQL
set statistics time on
-- Query 1 goes here
-- Query 2 goes here
set statistics time off

Win + shift + s -> print screen windows

Windows terminal
    Ctrl Shift T -> new tab
    Ctrl Shift W -> close current tab
    Ctrl Shift D -> duplicate currect tab

    Alt + Shift + +          → Split vertically (new pane on the right)
    Alt + Shift + -          → Split horizontally (new pane below)
    Alt + Arrow Keys         → Move focus between panes
    Alt + Shift + Arrow Keys → Resize the current pane

Claude/amp
    Ctrl G - edit prompt in editor

Notable
    Ctrl Shift X - change folder

KeePass
    Ctrl Alt D - auto type

Excel
    Ctrl+[space] - select current column
    Shift+[space] - select current row (space is long like a row)
        Ctrl+"+" - insert a new column/row (first select column/row) (can be done with multiple columns)
        Ctrl+- - delete column/row

    Ctrl+D - Fill down
        Also double click with mouse
    Ctrl+D - Get value from above
    Ctrl+R - Fill right
    Ctrl+` - Show formulas
    F4 - Anchor cell reference
    Ctrl+A - select current table
    Ctrl+; - Today

    Headers - middle aligned

    & - concat text in excel

    Select many columns, double click to autofit width all
    Select many columns, set width for one column - sets same width on all
    Select range before entering data, [enter] moves to next available cell
    Select range before entering data, Ctrl+[enter] - fill range with typed in value

    Relative references are visible in RC reference mode

Libre calc
    Shift + F7 - toggle spell check on/off

Visual Studio
    Ctrl m l - expand all
    Ctrl m o - collapse all to definition
    Ctrl m m - toggle fold current

Chat GPT web
    Ctrl + \         - show shortcuts
    Ctrl + Shift + O - new conversation
```

# code
```
https://code.visualstudio.com/docs/getstarted/keybindings
Ctrl+shift+space

code . -> run from console to open folder
code -> run from console

Ctrl + P          -> search for files
Ctrl + P          -> Program:20 -> go to 20th line
Ctrl + P          -> Program:@SomeMethod -> go to symbol
Ctrl + Shift + E  -> Explorer (files)
Ctrl + Shift + G  -> Git
Ctrl + Shift + F  -> Find
Ctrl + K Ctrl + S -> Keyboard shortcuts
Ctrl + N          -> New file
Ctrl + Shift + N  -> New window
Ctrl + Tab        -> switch tabs
Ctrl + S          -> Save
Ctrl + Shift + S  -> Save As
Ctrl + W          -> close window
Ctrl K I          -> show symbol information
Ctrl Shift Space  -> show symbol information
Ctrl Shift Space  -> show params

Ctrl + \          -> to split the active editor into two.
Ctrl+Shift+I      -> insert date time now (Insert Date Time now extension)
Ctrl Shift L      -> select all occurrences of selected text

Selection
    Shift + Alt + i -> add cursor to lines ends

ctrl + p - collapse folders in explorer - yay

Alt + F12 - > peek definition
F2 -> rename (js)
Refactor
    Select code and Ctrl .
        Extract function
        Extract constant
// @ts-check -> for .js files – enable type checking for just one file



Extensions:
    Rainbow CSV -> wow!
```

```
https://superuser.com/questions/889414/force-refresh-re-scan-wireless-networks-from-command-line
Wlan wifi refresh rescan

https://cheatography.com/davechild/cheat-sheets/regular-expressions/

https://www.markdownguide.org/basic-syntax/

markdown link [text](http://)

when running scripts for testing etc - always print the time the script started running
    and maybe include a timeout?
    in case a script takes for ever to run, you're likely interested in the results of several script runs
    and you don't want to comeback next day seeing that a single script has been running for 30h and you still don't have any results
```

# Python
```python
z = [1] * 5      # [1, 1, 1, 1, 1]
e = enumerate(z)
list(e)          # [(0, 1), (1, 1), (2, 1), (3, 1), (4, 1)]

# remember that if you exhaust the iterator in `e` without assigning the elements into a list
# you will not be able to iterate over it again
e = enumerate(z)
[print(x) for x in e] # prints [(0, 1), (1, 1), (2, 1), (3, 1), (4, 1)]
[print(x) for x in e] # prints nothing

# read all text
with open('filename.txt', 'r', encoding='utf-8') as f:
    content = f.read()
# with does not introduce a new scope in python
print(content)

# read all text with pathlib
from pathlib import Path
content = Path(f"path/to/{file_name}").read_text()
```

# agents
```
before coding something write a failing test first.

plan the script app in stages - a dummy mvp, add features to peaces, polish, etc. code each step, test that it works, move to next step, repeat untill app is ready, git commit at every step

if parts of sytem can be coded in parallel - use subagnets and git worktrees
if adding a feature needs the code to be refactored - refactor first in separate pr, then add feature in pr on top

in the code split pure code from side effects
do not invent use cases and do not code defensively, if it breaks we will fix it then

the app should dump logs so if it fails we can investigae what happend

when running the app should give live progress to the user so i know it's running and it didn't hang
when running the app live it should give user friendly output
there should be an option to give ai agent friendly output


code priorities:
- redable
- clean
- simple
- robust
- performace is the last concern

prefer using modules/libraries/packages to writing code yourself

create a local git repo

in the main dir there should be a build.sh, run.sh, test.sh script <- the function in self explanatory

when writing docs be short, prefer lists and points over prose. pragmatic over polished




add -fix flag to this script.
prefer readability over premature optimization.
use native powershell constructs over .net.
keep existing comments.
when needed add comments explaining WHY not WHAT.
keep existing variable names where applicable.
don't worry about memory usage.
don't worry about file churn.
apply the DRY principle.



used for chatgpt:
no fluff

give a self containing answer

When giving final answer use best fit:
1. table
    1. use `npx markdown-table-prettify` to format table
2. list and sublists
    1. use numbered lists
    2. nest lists when giving details
    3. long sentences split into list items
    4. file paths, links → put into separate list items
    5. Keep one idea per list item.
    6. Put supporting details in nested sub-lists.
    7. Split ideas into list items instead of joining them in one sentence.



```

view your distribution name and version
linux
cat /etc/os-release

