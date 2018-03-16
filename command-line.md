# Command line

## Examples

### Kill Windows running processes.
```shell
process='chromedriver';
ps -W | grep -i "$process" | awk '{print $1}' | while read pid; do taskkill //F //PID ${pid}; done;
```

### Bulk image processing.
```shell
startingPath=$(pwd);
find -type d | while read dir; do
    cd "$dir";
    find \( -iname "*.jpg" -o -iname "*.jpeg" -o -iname "*png"  \) | while read file; do
        convert -resize 1024x -density 72 -strip "$file" "$file";
    done;
    cd "$startingPath";
done;
```

### Bulk text update.
```shell
find -type f -name *.php -exec sed -i 's/variable = variableValue/variable = newVariableValue/g' "{}" \;
```

### Bulk folder creation.
```shell
mkdir 190{0..9}-0{1..9} \
&& mkdir 190{0..9}-{10..12} \
&& mkdir 19{10..99}-0{1..9} \
&& mkdir 19{10..99}-{10..12} \
&& mkdir 200{0..9}-0{1..9} \
&& mkdir 200{0..9}-{10..12} \
&& mkdir 20{10..99}-0{1..9} \
&& mkdir 20{10..99}-{10..12};
```
