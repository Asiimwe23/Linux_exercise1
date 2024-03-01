# Linux_exercise1
Introduction to Linux

# Question 1: Create a project directory called Exercise. Which commands did you use?
mkdir Exercise

# Question 2: In the directory, create all the sub-directories you would need for a Bioinformatics Project
mkdir data scripts results docs
cd data
mkdir raw processed

# Question 3: With the provided dataset files, put them in the appropriate directories you created under your Bioinformatics Project.
cd Exercise
mv *.fa data/raw/
# Then use the command diff to check whether the files are not duplicates of the other
diff nrf1_seq.fa nrf1_seqtemp.fa

# Question 4: Extract the sequence headers and save into a file `sequence_names.txt` in the appropriate directory
# First you need to count how many headers you are expecting to extract from both files using the commands below
grep -c ">" nrf1_seq.fa
grep -c ">" nrf1_seqtemp.fa
# Then extract the headers using the following command
grep ">" *.fa >>sequence_names.txt
# You can toogle through your new file as well with less
less sequence_names.txt
# Then finally count the headers you have extracted in your .txt file
wc -l sequence_names.txt
# Then move the file to results
mv sequence_names.txt ../../results

# Question 5: Save the commands you used in question 4 in a script file `extract_seq.sh`
# You can use any text editor like nano or vim, but for this case I used nano to create the file
nano extract_seq.sh
# Then write the commands to the script and save them using ctrl + x then yes
# I then move the file to the scripts directory since I created it while in the raw directory
mv extract_seq.sh ../../scripts
# Then make the file executable
chmod +x extract_seq.sh

# Question 6: Count the number of mRNA.
# First its better to combine the datasets
grep -c ">" dataset
