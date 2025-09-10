# imroo
A simple script to show Iranian calendar events for today or next days

## Dependencies
- jdate : Iranian/Persian/Jalali/Shamsi date
- idate : Hijri date
- date : (GNU) Gregorian date
- curl
- jq

In a Debian-like distro:

```bash
sudo apt install curl jq itools
# jdate needs to be manually built, the one in Debian 13 is old/buggy
# https://github.com/persiancal/jcal
```

# Usage
Check `imroo -h`:

```console
$ imroo -h
imroo: shows Iranian/international calendar events for current day or
            future days

Usage: imroo [OPTIONS]
Options:
    -s      Sync database json by downloading files from internet
    -d      Number of days into future from today (including today)
    -V      Print script version
    -h      Display the help message

Examples:
    # sync before first use
    imroo -s
    # get events for current day
    imroo
    # get events for today, tomorrow, and the day after tomorrow
    imroo -d3
```

As another example, the script can be used with
[dunst](https://dunst-project.org/documentation/#COLORS) implementation of
`notify-send` like this:

```sh
#!/bin/sh

notify-send -i "calendar" \
    "$(jdate +%E | cut -d- -f1)" \
    "$(imroo -d1 \
    | awk '/تعطیل/{print "<span fgcolor=\"red\">" $0 "</span>"; next} {print}')"
```

# Development
- linter: `shellcheck`
- formatter: `shfmt -i 4 -bn -ci -sr`
