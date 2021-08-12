# Disable bash history

Add the following line to `~/bash.rc`

```
HISTFILE=/dev/null
```


# Add timestamp to prompt

"When did I run that command?"

Modified from [@redandblack.io](http://redandblack.io/blog/2020/bash-prompt-with-updating-time/). Improved colours, and changed formatting preferences.

Thanks friends!

```
Directory="\w"
User="\u"
Host="\h"
DoubleSpace="  "
SingleSpace=" "
NewLine="\n"
NoColour="\e[00m"
PrintingOff="\["
PrintingOn="\]"
PromptColour="\e[0;33m"
DirectoryColour="\e[1;34m"
UserHostColour="\e[1;32m"
PS1prompt="\$"
PS2prompt=">"
RestoreCursorPosition="\e[u"
SaveCursorPosition="\e[s"
Timestamp="\A"
TimestampPlaceholder="--:--"

MoveCursorToTimestampPlaceholder() {
    CommandRows="$(history 1 | wc -l)"
    if [[ "$CommandRows" -gt 1 ]]; then
        VerticalMovement="$((CommandRows+1))"
    else
        Command="$(history 1 | sed 's/^\s*[0-9]*\s*//')"
        CommandLength="${#Command}"
        PS1promptLength="${#PS1prompt}"
        TotalLength="$((CommandLength+PS1promptLength))"
        Lines="$((TotalLength/COLUMNS+1))" # use environment variable
        VerticalMovement="$((Lines+1))"
    fi
    tput cuu "$VerticalMovement"
}

PS0elements=(
    "$SaveCursorPosition" "\$(MoveCursorToTimestampPlaceholder)"
        "$PromptColour" "$Timestamp" "$NoColour"
        "$RestoreCursorPosition"
)
# build the prompt using the layout of variables as above
PS0="$(IFS=; echo "${PS0elements[*]}")"

PS1elements=(
    # insert a new line after last timestamp and command
    "$NewLine"
    # first line of prompt
    "$PrintingOff" "$PromptColour" "$PrintingOn"
    "$TimestampPlaceholder" "$DoubleSpace" "$DirectoryColour" "$Directory"
        "$PrintingOff" "$NoColour" "$PrintingOn" "$NewLine"
    # second line of prompt
    "$PrintingOff" "$UserHostColour" "$PrintingOn"
        "${User}@${Host}" "$PrintingOff" "$NoColour" "$PrintingOn" ':' "$PrintingOff" "$PromptColour" "$PrintingOn" "$PS1prompt" "$SingleSpace"
        "$PrintingOff" "$NoColour" "$PrintingOn"
)
# build the prompt using the layout of variables as above
PS1="$(IFS=; echo "${PS1elements[*]}")"

PS2elements=(
    "$PrintingOff" "$PromptColour" "$PrintingOn"
        "$PS2prompt" "$SingleSpace"
        "$PrintingOff" "$NoColour" "$PrintingOn"
)
# build the prompt using the layout of variables as above
PS2="$(IFS=; echo "${PS2elements[*]}")"

shopt -s histverify
```
