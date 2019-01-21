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

### web-scraper
```shell
echo '' > ./greek-names-temp.txt;

baseUrls=(
    "https://el.wiktionary.org/w/index.php?title=%CE%9A%CE%B1%CF%84%CE%B7%CE%B3%CE%BF%CF%81%CE%AF%CE%B1:%CE%91%CE%BD%CE%B4%CF%81%CE%B9%CE%BA%CE%AC_%CE%BF%CE%BD%CF%8C%CE%BC%CE%B1%CF%84%CE%B1_(%CE%B5%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)" "https://el.wiktionary.org/wiki/%CE%9A%CE%B1%CF%84%CE%B7%CE%B3%CE%BF%CF%81%CE%AF%CE%B1:%CE%93%CF%85%CE%BD%CE%B1%CE%B9%CE%BA%CE%B5%CE%AF%CE%B1_%CE%BF%CE%BD%CF%8C%CE%BC%CE%B1%CF%84%CE%B1_(%CE%B5%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)"
    );

for baseUrl in "${baseUrls[@]}"; do
    curl $baseUrl 2> /dev/null | sed 's/">/">\n/g' | sed 's/ href=/\nhref=/g' | sed 's/&amp;/\&/g' | perl -ne 'if( /href="(.*?mw-pages)"/ ) { print "https:${1}\n" }' > ./urls.txt;

    while read url; do
        curl "$url" 2> /dev/null | perl -ne 'if( /title="(.*?)"/ ) { print "$1\n" }' | sed 's/ (όνομα)//g;s/ (αποσαφήνιση)//g' >> ./greek-names-temp.txt;
    done <./urls.txt

    rm ./urls.txt;
done

cat ./greek-names-temp.txt | sort | uniq > ./greek-names.txt;
rm ./greek-names-temp.txt;

# Clean non names.
sed -i "/^$/d; \
/Add/Id; \
/wmf/Id; \
/Βικιλεξικό/Id; \
/Εκτυπώσιμη/Id; \
/Επεξεργασία/Id; \
/Επίσκεψη/Id; \
/Κατάλογος/Id; \
/Κατηγορία/Id; \
/Λίστα/Id; \
/πολεμοποιός/Id; \
/Προβολή/Id; \
/Συζήτηση/Id; \
/Το μέρος/Id; \
/Τυπογραφικές/Id; \
/Φόρτωση/Id;" \
./greek-names.txt;
```

### Refactoring: Providing new variable to test case.
```shell
find Scripts/Company/DD_Regular/Risk_High/ -type f | while read file; do sed -i "s/\(Activities\/1.9.2.*targetRisk\)\]/\1, ('calculatedRisk') : 2.25]/" $file; done;
```

### Counting available tests.
```shell
echo "$(($(find Scripts/ -type f | wc -l) - $(find Scripts/Base_tests/ -type f | wc -l))) tests";
```

### Removing argument from test
```shell
Command:
grep -irnl "1.11.1')," Scripts | while read file; do sed -Ei "s/(^.*1.11.1'\),\s*\[)\('transitionName'\)\s*:\s*'Yes, permit'/\1:/gi" $file; done;

Result (with spaces):
-WebUI.callTestCase(findTestCase('Daimler/Base_tests/Activities/1.11.1'), [('transitionName') : 'Yes, permit'], FailureHandling.STOP_ON_FAILURE)
+WebUI.callTestCase(findTestCase('Daimler/Base_tests/Activities/1.11.1'), [:], FailureHandling.STOP_ON_FAILURE)

Result (without spaces):
-WebUI.callTestCase(findTestCase('Daimler/Base_tests/Activities/1.11.1'), [('transitionName'):'Yes, permit'], FailureHandling.STOP_ON_FAILURE)
+WebUI.callTestCase(findTestCase('Daimler/Base_tests/Activities/1.11.1'), [:], FailureHandling.STOP_ON_FAILURE)
```

### Get all activities that do not expect any parameters.
```shell
grep -irn '\[:\]' Scripts/Daimler/ | cut -d':' -f3 | sort | uniq | sed "s/WebUI.callTestCase(findTestCase('Daimler\/Base_tests//g; s/\/Activities\///; s/TC\///; s/'),\s*\[//; s/\s*//g";
```

### Get all users from the Profiles.
```shell
grep -rn User Profiles/ | cut -d':' -f3 | sed 's/\s*//g; s/<name>//; s/<\/name>//; s/<init.*//' | sort | uniq;
```

### Get all available DFE items.
```shell
grep -r 'public class DFE' Items/ | sed 's|Items.*class DFE||g; s| :.*||';
```
