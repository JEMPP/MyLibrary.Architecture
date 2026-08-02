# .gitignore -Template für MyLibrary

``` .gitignore
# .gitignore -Template für MyLibrary

``` .gitignore
# ###################
# MyLibrary.Architecture Standard

# Secrets

appsettings.Secrets.json

# Archives

*.zip
*.7z
*.rar
*.tar
*.tar.gz

# Export files

*.bak
*.tmp
*.temp
*.orig

# Generated packages
*.nupkg
*.snupkg

# Visual Studio

.vs/

# Build

bin/
obj/

# Rider

.idea/

# User Files

*.user
*.suo

# ReSharper

_ReSharper*/
*.DotSettings.user

# Logs

*.log

# NuGet

packages/

# Certificates

*.pfx
*.snk

# Test Results

TestResults/

# Coverage

coverage/
*.coverage
*.coveragexml

# Publish

publish/

# Temporary Files

*.tmp
*.bak

# OS

Thumbs.db
Desktop.ini
.DS_Store


#######################
# Access-specific
#
# Access databases often contain
# personal data or connection information.
# Comment out only if the database
# is intentionally versioned.

*.accdb

# Access lock files
*.laccdb
*.ldb

# Legacy version history
VersionHistory.txt

# Export log
Export.log

# #####################
```
```