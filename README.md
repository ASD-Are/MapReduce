# MapReduce
# Description
<img width="750" alt="194803849-7c4c723f-81a1-48ef-b068-12dd25496823" src="https://github.com/ASD-Are/MapReduce/assets/93379106/a8e9bfa1-92ac-486f-8968-e8256a1cdd64">
<br>
# Description
- Step 1: Generate an input file for the Pi MapReduce application.

- Step 1.1: Develop a Java program that takes two command-line arguments:
 - R: The radius
 - N: The number of (x, y) pairs to generate
 - The program then randomly creates N pairs of (x, y) coordinates and outputs them to the console.

- Step 1.2: Execute the program from Step 1.1 and save the output to a file. This file will serve as the input for Step 2's Pi MapReduce program.

- Step 2: Implement a MapReduce program to count the number of darts inside and outside the circle.

- Step 3: Utilize the file generated in Step 1.2 as the input for running the MapReduce program created in Step 2.

- Step 4: Compute the value of Pi in the driver program based on the counts of inside and outside darts.

# Implement
## Requirment
- Set Up GCP Environment
  ![image](https://github.com/ASD-Are/MapReduce/assets/93379106/677de0cc-8fe8-48bd-8970-a7fef9a65281)
- Hadoop Environment
  ![image (1)](https://github.com/ASD-Are/MapReduce/assets/93379106/db821475-42f5-4127-a455-97bcb0f8b7c1)
- Java environment
  ![image](https://github.com/ASD-Are/MapReduce/assets/93379106/e7958b31-60b7-4854-b444-632365c5c57d)

# Prepare input data
```
  $ mkdir PiCalculation
  $ cd PiCalculation
  $ vi GenerateRandomNumbers.java
  $ javac GenerateRandomNumbers.java
  $ java -cp . GenerateRandomNumbers
```
Input data will be stored in the file PiCalculationInput

# Setup passphraseless ssh
## After generating the input file let's check that we can ssh to the localhost without a passphrase:
```
  $ cd hadoop-3.3.4/
  $ ssh localhost
```
If you cannot ssh to localhost without a passphrase, execute the following commands:
```
  $ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  $ chmod 0600 ~/.ssh/authorized_keys
```
# Make the HDFS directories which are necessary to execute MapReduce (Copy input data to HDFS)
```
  $ cd ..
  $ cd hadoop-3.4.0/
  $ bin/hdfs namenode -format
  $ sbin/start-dfs.sh
  $ wget http://localhost:9870/
  $ bin/hdfs dfs -mkdir /user
  $ bin/hdfs dfs -mkdir /user/adagniew407/picalculate/input
  $ bin/hdfs dfs -put ../PiCalculation/PiCalculationInput /user/adagniew407/picalculate/input
```
If you can not copy input into hadoop dictionary, please restart the virtual machine.

# Prepare code
- Build PiCalculation java file
```
  $ cd /hadoop-3.4.0
  $ vi PiCalculation.java
```
- Compile PiCalculation.java and create a jar
```
  $ bin/hadoop com.sun.tools.javac.Main PiCalculation.java
  $ jar cf wc.jar PiCalculation*class
```
- Compile PiCalculation.java and create a jar
  ```
  $ bin/hadoop com.sun.tools.javac.Main PiCalculation.java
  $ jar cf wc.jar PiCalculation*class
  ```

# Run
- Execute the PiCalculation.java
  ```
  $ bin/hadoop com.sun.tools.javac.Main PiCalculation.java
  $ jar cf wc.jar PiCalculation*class
  ```
- Check the output on the output directory
  ```
  $ bin/hdfs dfs -ls /user/adagniew407/picalculate/output
  $ bin/hdfs dfs -cat /user/adagniew407/picalculate/output/part-r-00000
  ```

# Test Result
Test Case:

How many random numbers to generate: 1000000 Radius = 200
![image (2)](https://github.com/ASD-Are/MapReduce/assets/93379106/632a2841-5618-49fd-867e-9c37fbbd561d)

# Detail Design Presentation
[Pi calculation using MapReduce](https://docs.google.com/presentation/d/14XyJGLEx9zQwDkyTLRWt1Ab5C3h3j0y6ZUFce9LicQg/edit?usp=sharing)

# Appendix








