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

```

# PowerShell
```powershell
Get-item "somefile.txt" | format-list show all properties of a object

Invoke-WebRequest -Method 'POST' -Body '{"Command":"\"C:/Program Files/R/R-3.5.3/bin/Rscript.exe\" C:/Services/Code/ScEntsoE_IE_SQL_DA_Price.R","Timeout":20}' -Uri "http://localhost:4000/execute" -ContentType "application/json" -UseBasicParsing

# Powershell tee output to a file but preserve colors in console
Start-Transcript out.log
# Run your app here
Stop-Transcript

Get-content -tail 20 -wait path/to/file/here
Get-EventLog application -Newest 1 | clip -> get stuff to clipboard awesome!
# source: https://blogs.technet.microsoft.com/heyscriptingguy/2014/06/15/powertip-send-output-to-clipboard-with-powershell/
```

# az keyvault
```powershell
az keyvault secret list
az keyvault secret list --vault-name "kv-it-shared-scraper"
az keyvault secret list --vault-name "kv-it-data-collection"

# IT.DataCapture key vault
az keyvault secret list --vault-name "kv-it-data-capt-scraper"
az keyvault secret show --vault-name "kv-it-data-capt-scraper" --name "tennet-production-api-key"

az keyvault secret set  --vault-name "kv-it-data-capt-scraper" --name "rnp-certificate-incommodities-ws3" --file "C:\Users\fku\Downloads\certAndKey.pem"
az keyvault secret set  --vault-name "kv-it-data-capt-scraper" --name "argusFtpPassword" --value "..."
az keyvault secret delete --vault-name "kv-it-data-capt-scraper" --name "argus-ftp-username"
```

# az acr - Azure Container Registry
```powershell
az acr repository list --name acrinco --output table # List docker images from Azure
az acr repository show-tags --name acrinco --repository it-wattsight-scraper-test --output table # List tags
az acr repository show --name acrinco --image it-wattsight-scraper-test:2
```

# paket
```PowerShell
dotnet paket add Microsoft.AspNetCore.Http --project .\src\metdesk.scraper.fsproj # add package
dotnet paket install                                                              # install packages

# paket - github tokes
# https://github.com/settings/tokens -> here you can generate tokes
dotnet paket config add-token github_token ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
# tokens are stored here
C:\Users\fku\AppData\Roaming\Paket\paket.config

# paket - install a github file
# https://fsprojects.github.io/Paket/github-dependencies.html
Add file in paket.dependencies and paket.references
# update github dependencies
# --filter makes paket interpret <package id> as a regex
dotnet paket update <package id> --filter
dotnet paket update github       --filter
```

# dotnet
```
dotnet publish ./IT.Curvie/IT.Curvie.fsproj --framework net6.0 --self-contained --runtime win-x64 -c Release -p:PublishSingleFile=true -p:IncludeNativeLibrariesForSelfExtract=true -o release_here
dotnet publish -p:PublishSingleFile=true --runtime linux-x64 --self-contained true -c Release
```

# docker
```
docker build --build-arg GITHUB_TOKEN=***REMOVED*** .
docker build --build-arg GITHUB_TOKEN=***REMOVED*** -t test .

docker images
docker stop
docker restart
docker container ls = docker ps
docker logs a5 -> show logs

docker run -it -p 8080:8080 myapp:tag1
docker run -it --entrypoint sh acrinco.azurecr.io/it-metdesk:latest
docker run -it --env-file c:/stuff/env.txt metdesk.scraper:latest
    File looks like this:3
        Secrets__kyosApiKey=123
        SECRETS__KYOSAPIKEY=123
        SECRETS__SQLPASSWORD=123
        SECRETS__TEREGAPASSWORD=123
        SECRETS__TEREGAUSERNAME=123
        SECRETS__UIOLIPASSWORD=123
        SECRETS__UIOLIUSERNAME=123

sudo docker run --env-file ./env.txt acrinco.azurecr.io/it-wattsight-scraper:164 > out.log &
sudo docker run --env-file ./env.txt -it --entrypoint sh acrinco.azurecr.io/it-wattsight-scraper:165
sudo docker run -p 8080:8080 acrinco.azurecr.io/it-metdesk-notificationreceiver:latest &
    this is the one I used to start notification receiver on dmz linux
    Nginx forwards requests from 81 -> 0.0.0.0:8080
    -p host:container
    Docker forwards requests from host:8080 -> container:8080

sudo docker pull acrinco.azurecr.io/it-wattsight-scraper:latest
docker run -d -p 5432:5432 --name my-postgres -e POSTGRES_PASSWORD=mysecretpassword postgres
```

# npm
```powershell
npm update @incom/js-scrapers-sdk
npm i github:@incomas/it.jsscraperssdk
npm i github:@incomas/it.jsscraperssdk -S # save
```

# kubectl
```
kubectl logs -l app=it-scheduler --tail=-1 > out
kubectl get namespace – list namespaces
kubectl config get-contexts
kubectl config use-context it-prod-aks
kubectl get services
kubectl get pods
kubectl logs it-pointconnect-5fc88db44f-9nbzh –n pointconnect    -n <->
kubectl logs -l app=it-continuousdatacapture
Deployment in kubectl -> that is the service
Service in kubectl -> service endpoint exposed on network
kubectl logs continuousdatacapture-84cd5756f5-tb5g9 -n data-collection > out.logs
```

# misc
```
Azure Data Studio
    Shift+Win+R - close/open results pane

SQL
set statistics time on
-- Query 1 goes here
-- Query 2 goes here
set statistics time off

Win + shift + s -> print screen windows

Windows terminal
    Ctrl Shift T -> new tab
    Ctrl Shift W -> close current tab

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

code
    https://code.visualstudio.com/docs/getstarted/keybindings
    Ctrl+shift+space

    code . -> run from console to open folder
    code -> run from console

    Ctrl + P -> search for files
    Ctrl + P -> Program:20 -> go to 20th line
    Ctrl + P -> Program:@SomeMethod -> go to symbol
    Ctrl + Shift + E -> Explorer (files)
    Ctrl + Shift + G -> Git
    Ctrl + Shift + F -> Find
    Ctrl + K Ctrl + S -> Keyboard shortcuts

    Ctrl + N -> New file
    Ctrl + Shift + N -> New window
    Ctrl + Tab -> switch tabs

    Ctrl + S -> Save
    Ctrl + Shift + S -> Save As

    Ctrl + W -> close window

    Ctrl K I -> show symbol information
    Ctrl Shift Space -> show symbol information
    Alt + F12 - > peek definition
    F2 -> rename (js)
    Refactor
        Select code and Ctrl .
            Extract function
            Extract constant
    // @ts-check -> for .js files – enable type checking for just one file

    Ctrl+\ to split the active editor into two.
    Ctrl+Shift+I -> insert date time now (Insert Date Time now extension)
    Ctrl Shift Space -> show params

    Ctrl Shift L -> select all occurrences of selected text

    Selection
        Shift + Alt + i -> add cursor to lines ends

    ctrl p - collapse folders in explorer - yay

    Extensions:
        Rainbow CSV -> wow!

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
