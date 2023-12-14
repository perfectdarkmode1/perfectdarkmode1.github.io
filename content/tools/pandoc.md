---
title: "Pandoc Guide"
date: 2023-04-22T06:37:25-07:00
draft: true
---
# Pandoc
Used for converting file formats

https://ins3cure.com/pandoc-on-rhel-8/

Go to https://github.com/jgm/pandoc/releases/latest, download the latest tarball (currently pandoc-2.17.0.1-linux-64.tar.gz) and run:
```
sudo tar xvzf pandoc-2.17.0.1-linux-64.tar.gz --strip-components 1 -C /usr/local/
```

install TeX to be able to generate PDF output:
```
sudo yum -y install texlive
```
## Basic useage
```
pandoc inputfile -f inputfiletype -t outputfiletype -o outputfile
```

## Convert full folder
```
for f in *; do pandoc "$f" -s -o "../bloghtml/${f%}.html"; done
```
