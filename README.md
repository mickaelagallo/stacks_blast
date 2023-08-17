# stacks_blast
## Step 1: Data verification
1. Enter this command line to enter the server

```ruby
## ssh -i [key.pem] [server][DNS] 
ssh -i keystacks2.pem ubuntu@[DNS]  ## In this case, the DNS changes every time the server is opened
```
2. Superuser permissions

```ruby
sudo su
```
3. Mounting a S3 bucket to an instance

```ruby
s3fs oreos3 bucket/ -o passwd_file=$HOME/.passwd-s3fs,allow_other,uid=1001,gid=1001
```
4. Create a folder

```ruby
mkdir micka
```
5. Move my data

```ruby
mv Stefania micka/  ## Stefania (demultiplexed files)
mv stefania_popmap.txt micka/
```
## Step 2: Using UStacks

1. Create a text file

```ruby
nano UStacks.sh 
```
2. In the text file paste this code
3. Create output files folder

```ruby
mkdir result
```

3. Run the text file

```ruby
sh UStacks.sh Stefania/ result/
```


UPDATE!!

```ruby
import pandas as pd #Para importar el dataframe
ruta_archivo = "catalog.tags.tsv.gz"
#df = pd.read_csv(ruta_archivo, sep='\t', compression='gzip') #Visualización normal del dataframe
f = pd.read_csv(ruta_archivo, sep='\t', compression='gzip', header=None, names = ['sample_id','loci_id','consensus','st_comp','seq_id','seq','fl1','fl2','fl3'])
df[1:-1]
```


## Converting tables to FASTA format ---> using the Pandas library

1. Import the library
   
```ruby
import pandas as pd
```
2. Indicate the path of the file

```ruby
ruta_archivo = "Ab_372_ACTGG-ATCACG.tags.tsv.gz"
```
3. Loading the CSV file
   
```ruby
df= pd.read_csv(ruta_archivo, sep="\t", header=None,
            names=["sample_id", "loci_id", "consensus", "st_comp", "seq_id", "seq", "fl1", "fl2", "fl3"])
df= df[1:-1] #to display the table without the first and last row
```

4. To add text/symbols to a column

```ruby
df['loci_id'] = df['loci_id'].apply(lambda x: f">{x}") #FASTA format symbol: >
fasta=df[["loci_id","seq"]]
```
5. To convert to FASTA format

```ruby
fasta.to_csv("catalogue.fasta", sep="\n", header=False, index=False)
```
6. Para visualizar solo la columna seq_id

```ruby
sin_seq_id=df["seq_id"]
fasta.iloc[0,1]
```

