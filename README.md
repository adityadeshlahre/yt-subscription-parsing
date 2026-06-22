# Simple yt sub parsing using CLI tools only

- we are going to use awk and jq
- note: open only working for macOS i guess so use xdg-oppen in linux

## Parsing YT take out file using AWK

```fish
``awk -F',' '
BEGIN { print "[" }
NR > 1 && !seen[$2]++ {
    if (n++) print ","
    printf "  {\"url\":\"%s\"}", $2
}
END { print "\n]" }
' subscriptions.csv > subscriptions.json `
```

## Opening ursl using jq from parsed json

```fish
jq -r '.[].url' subscriptions.json | while read -l url
    open "$url"
    sleep 5
end
```
