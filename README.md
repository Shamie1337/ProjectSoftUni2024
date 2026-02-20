Parallel CSV → DB → Calculator Workflow 

You will develop a concurrent automation system composed of four main automations, each responsible for a specific stage of the workflow. 

Automation 1: CSV Generator 

Every 10 seconds, create a new CSV file using File Stream / Stream Writer in the …/in directory. 

The file should have a header row (Number1, Number2) and a random number of rows (between 1 and 10) 

Each row should contain two random numbers (between 1 and 100). 

 

Automation 2: Data Gathering 

Every 20 seconds, read all the files in the …/in folder. 

Add all the number pairs into a database table. 

Insert each pair into a DB table 

For each pair, insert the following columns: (Id, Number1, Number2, Result, Operation Status, File Path/Filename) 

Define Operation Status values as: 

Generated = 1 

Started Processing = 2 

Processed = 3 

 

Automation 3: Calculator Processor 

This automation should receive a certain number of pairs and process them. 

Create a WPF Calculator (Windows Calculator cannot be used due to multitasking limitations). 

 

Launch the calculator. 

 

 

For each row:  

Input the two numbers via TestStack.White (or UIA patterns) 

Read the result 

Update DB row with the result and status Processed (3) 

Note: TestStack.White uses mouse clicks, which can cause flakiness — be mindful. 

Automation 4: Orchestrator    // main  

Starts multiple instances of Automation 1 to generate files. 

Starts one instance of Automation 2 to gather data. 

For every 10 rows that need processing, open a new instance of Automation 3 to calculate results. 

Check the DB to find out which files have all their pairs processed and move the files in …/out folder 
