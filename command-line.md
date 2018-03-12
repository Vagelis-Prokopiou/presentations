# Command line

## Examples
```bash
# Kill Windows running processes.
process='chromedriver';
ps -W | grep -i "$process" | awk '{print $1}' | while read pid; do taskkill //PID ${pid}; done;

# Act on multitude of folders.
startingPath='/c/Users/Vangelisp';
find -type d | while read dir; do cd "$dir"; do stuff; cd "$startingPath"; done;

# Bulk text update.
find -type f -name *.php -exec sed -i 's/variable = variableValue/variable = newVariableValue/g' "{}" \;

# Create a folder for each month from 1900 to 2099.
mkdir 190{0..9}-0{1..9} \
&& mkdir 190{0..9}-{10..12} \
&& mkdir 19{10..99}-0{1..9} \
&& mkdir 19{10..99}-{10..12} \
&& mkdir 200{0..9}-0{1..9} \
&& mkdir 200{0..9}-{10..12} \
&& mkdir 20{10..99}-0{1..9} \
&& mkdir 20{10..99}-{10..12};
```
