---
title: "Awk"
date: 2023-07-28T22:57:01+01:00
draft: true
---

# upper case the first letter
`awk '{for(i=1;i<=NF;i++){ $i=toupper(substr($i,1,1)) substr($i,2) }}1' file`