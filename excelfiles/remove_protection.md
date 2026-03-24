To remove protection rules we can follow the next steps:

1. Unzip your file

```bash
unzip yourfile.xlsx -d temp_folder
```

2. Remove the protection rule on every sheet:

```bash
sed -i 's/<sheetProtection[^>]*\/>//g' temp_folder/xl/worksheets/sheet*.xml
```

3. Rezip the file:

```bash
cd temp_folder
zip -r ../unprotected.xlsx *
cd ..
```
