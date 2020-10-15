
# UNIX
### General
#### rename all files in directory
example:
```
for filename in Islet_123.*; do mv "$filename" \
"${filename//Islet_123./islet.}"; done
```
#### how to kill a process using a port
```
To list any process listening to the port 8080:
lsof -i:8080
To kill any process listening to the port 8080:
kill $(lsof -t -i:8080)
or more violently:
kill -9 $(lsof -t -i:8080)
(-9 corresponds to the SIGKILL - terminate immediately/hard kill signal: see List of Kill Signals and What is the purpose of the -9 option in the kill command?. If no signal is specified to kill, the TERM signal a.k.a. -15 or soft kill is sent, which sometimes isn't enough to kill a process.).
kill $(lsof -t -i:1113)
kill -9 $(lsof -t -i:1113)
```
#### count number of files in current directory
`ls | wc -l`





## Grep
__get matching lines between 2 files__
`grep -Ff file1 file2 > file3`
__get mismatching lines between 2 files__
`grep -Fxvf file1 file2 > file3`
__remove lines from one file using pattern__
`LC_ALL=C fgrep -v PATTERN infile > outfile`
__get lines containing patterns in file__
`fgrep -Ff PATTERN_file infile > outfile`
__remove empty lines from file__
`grep . infile > outfile`


## Awk
#### Save specific columns from one file to another
`awk '{print $1,$2,$3,$4,$8}' infile > outfile`
#### Replace values in column with single value
`awk '{$35 = $35"$"; print}' infile > outfile`
`awk '$[column]="[replace]"' FS=, OFS=, inputfile > outputfile`
`awk '{$4 = "all"; print}' inputfile > outputfile`
#### Get unique Counts
`awk '{a[$5]++;} END{for(i in a) print a[i]"  "i}' inputfile`
#### command to save lines containing either matching pattern to file
`awk '/pattern1/ || /pattern2/{print}' file > outFile`
#### replace 1st occurance of string in file
```
awk '{sub(/blue/,"azure")}1' infile > outfile
# replaces first occurance in line of blue with azure
```
#### remove duplicates (based on whole line)
``awk '!seen[$0]++' ``

#### remove duplicates (based on single column value)
``awk '!seen[$1]++' ``


#### replace values in column with single value
`awk '{$1 = "value_you_want"; print}' inputfile > outputfile`

#### comparison operator, one argument
`awk '{ if ($4 >=0.05) { print } }' ${inputFile} > ${outputPosFile}`  
`awk '{ if ($4 <=-0.05) { print } }' ${inputFile} > ${outputNegFile}`


## Sed
__replace pattern in file__
`sed -i -e 's/FromPattern/ToPattern/g' infile`


## Bash
__loop over lines in file__
```
#!/bin/bash  
IFS= read -r line  
do  
echo "$line"  
done < "$infile"
```
__loop over list__



# PYTHON
## Dataframes
#### create empty dataframe
`dfObj  =  pd.DataFrame(columns=['User_ID',  'UserName',  'Action'])`
#### append rows to dataframe
`dfObj  =  dfObj.append({'User_ID':  25,  'UserName':  'Jack',  'Action':  'Login'},  ignore_index=True)`

#### append columns to dataframe
```
dfObj['UserName'] = ['Riti', 'Aadi', 'Jack']
dfObj['Name'] = ['Riti', 'Aadi', 'Jack']
```
#### Add rows to an empty dataframe at existing index
```
dfObj.loc['a'] = [23, 'Riti', 'Login']
dfObj.loc['b'] = [24, 'Aadi', 'Logout']
dfObj.loc['c'] = [25, 'Jack', 'Login']
```


#### getting the dimensions
```
In  [5]: df.shape
Out[5]:  (4,  3)
```
#### selecting with row numbers
'If you have a dataframe like':
```
df = pd.DataFrame(data={
'X': [1.5, 6.777, 2.444, pd.np.NaN],
 'Y': [1.111, pd.np.NaN, 8.77, pd.np.NaN], 
 'Z': [5.0, 2.333, 10, 6.6666]})
```
'Instead of iloc,you can use .loc with row index and column name like':
```
df.loc[row_indexer,column_indexer]=value
df.loc[[0,3],'Z'] = 3
```
Output:
```
     X       Y        Z
0    1.500   1.111    3.000
1    6.777   NaN      2.333
2    2.444   8.770    10.000
3    NaN     NaN      3.000
```
#### iterate over rows 
```
for row in df.rows:
   print row['c1'], row['c2']
```

#### get column as series
`s = pd.Series(df['c1'])`
#### get absolute value of series
`s.abs()`

#### exclude indices from series
`s = s[~s.index.isin([0, 3, 4])]`

#### List unique values in the df['name'] column
`df.name.unique()`
#### get number of unique values in the df['name'] column
`len(df['name].unique()) `
#### get value counts
`s.value_counts(dropna=False)`
`s.value_counts()`
#### normalized value counts:
With normalize set to True, returns the relative frequency by dividing all values by the sum of values.
`s.value_counts(normalize=True)`
#### column to list
`s = pd.Series(df['name']).tolist()`





### Matplotlib
#### Add subplots to figure
in the parens: 1st digit = number of rows , 2nd digit = number of columns, 3rd digit = index of the subplot
```
fig = plt.figure(figsize=(20,15))
a1 = fig.add_subplot(431)
a2 = fig.add_subplot(432)
a3 = fig.add_subplot(433)
a4 = fig.add_subplot(434)
a5 = fig.add_subplot(435)
a6 = fig.add_subplot(436)
a7 = fig.add_subplot(437)
a8 = fig.add_subplot(438)
a9 = fig.add_subplot(439)
a10 = fig.add_subplot(4,3,10) 
```


# R



# BASH
#### loop over array
```
for element in  ${arrayName[@]}; do  
echo "do stuff with ${element}"  
done
```
#### array format
`arrayName=(element1 element2 element3)`

#### concatenate multiple variables together
`var4="${var1}${var2}${var3}"`

#### merge files together using filenames
```
ls ${dir} > ${fileListFile}

for pattern in  ${arrayName[@]}; do  
matchingFiles="Name this"  
mergedFile="Name this ${pattern}.suffix"  
LC_ALL=C fgrep ${pattern} ${fileListFile} > ${matchingFiles}  
xargs < ${matchingFiles} cat > ${mergedFile}  
done
```




# Unsorted



__sorting stuff to separate files quickly:__
```
for chrom in  ${chromList[@]}; do  
echo "splitting ${chrom} tagalign"outfile="${outDir}${chrom}${outSuffix}"  
echo "    infile = ${inputTagAlign}"  
echo "    outfile = ${outfile}"  
LC_ALL=C fgrep ${chrom} ${inputTagAlign} > ${outfile}  
echo "    done splitting ${chrom}"  
done
```

__bedtools intersect, keep all stuff__
`bedtools intersect -a infile1 -b infile2 -wa -wb > outfile`
__bedtools sort__
`bedtools sort -i infile > outfile`



> Written with [StackEdit](https://stackedit.io/).
