**Linux_exercise1**
**Introduction to Linux**

**Question 1: Create a project directory called Exercise. Which commands did you use?**
```
mkdir Exercise 
```

**Question 2: In the directory, create all the sub-directories you would need for a Bioinformatics Project**

```
mkdir data scripts results docs 
cd data
mkdir raw processed
```

**Question 3: With the provided dataset files, put them in the appropriate directories you created under your Bioinformatics Project.**

```
cd Exercise
mv *.fa data/raw/
```

# Then use the command diff to check whether the files are not duplicates of the other
```
diff nrf1_seq.fa nrf1_seqtemp.fa 

```

**Question 4: Extract the sequence headers and save into a file sequence_names.txt**

```
# First you need to count how many headers you are expecting to extract from both files

grep -c ">" nrf1_seq.fa 
grep -c ">" nrf1_seqtemp.fa
 ```
# Then extract the headers using the following command
``` 
grep ">" *.fa >>sequence_names.txt
```
# You can toogle through your new file as well with less
``` 
less sequence_names.txt
```
# Then finally count the headers you have extracted in your .txt file
``` 
wc -l sequence_names.txt
```
# Then move the file to results
``` 
mv sequence_names.txt ../../results
```

**Question 5: Save the commands you used in question 4 in a script file `extract_seq.sh`**

# You can use any text editor like nano or vim, but for this case I used nano to create the file
``` 
nano extract_seq.sh
```
# Then write the commands to the script and save them using ctrl + x then yes
# I then move the file to the scripts directory since I created it while in the raw directory
``` 
mv extract_seq.sh ../../scripts
```
# Then make the file executable
``` 
chmod +x extract_seq.sh
```

**Question 6: Count the number of mRNA.**

# We shall use the file where we saved the headers then save to another output file
``` 
grep -c "mRNA" sequence_names.txt > mRNA_count.txt
```
# Make the file executable
``` 
chmod +x mRNA_count.txt
```
# We then count the other sequences
``` 
grep -v "mRNA" sequence_names.txt | wc -l  > other_sequences.txt
```
# Make the file executable
``` 
chmod +x other_sequences.txt
```

**Question 7: How many organisms (create a file with the organisms without duplicates)**

# we extract the unique organisms with the following command
```
cut -d "," -f 2  sequence_names.txt | sort | uniq > unique_organisms.txt- 
```
# then count the extracted unique organisms
```
wc -l unique_organisms.txt 
```

**Question 8: How many are predicted?**

# Exctracted from file with headers with the use of this command
```
grep -c "PREDICTED" sequence_names.txt  > predicted_sequences.txt 
```

**Question 9: How many nucleotides are in the file? How many of each of the bases are there?**

# Combine the sequences in one dataset
```
cat *.fa > dataset.fa 
```
# Prove the combined the dataset 
```
grep -c ">" dataset 
```
# Create a bash file called count_nucleotides using a text editor
``` 
nano count_nucleotides.sh
```
# Write a script to execute the task
```
#!/bin/bash 
```
# remove the headers from the dataset
```
grep -v ">" datase.fa > dataset_no_headers.fa 
```

# Count the occurrence of each base
```
count_A=$(grep -o 'A' dataset.fa | wc -l)
count_C=$(grep -o 'C' dataset.fa | wc -l)
count_G=$(grep -o 'G' dataset.fa | wc -l)
count_T=$(grep -o 'T' dataset.fa | wc -l)
```

# Calculate the total number of nucleotides
```
total_nucleotides=$((count_A + count_C +  count_G + count_T)) 
```

# Print the results
```
echo "Total number of nucleotides (excluding headers): $total_nucleotides"
echo "Number of A bases: $count_A"
echo "Number of C bases: $count_C"
echo "Number of G bases: $count_G"
echo "Number of T bases: $count_T"
```

# Make the file executable
```
chmod +x count_nucleotides.sh
```
# Then run the file to see the results
```
./count_nucleotides.sh 
```
