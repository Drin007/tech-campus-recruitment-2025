Solutions Considered

Given the constraints of efficiently extracting logs from a 1 TB log file, we explored multiple approaches:

1. Line-by-Line File Scanning (Implemented)
	•	Approach: Open the log file and read it line by line, filtering logs that match the given date.
	•	Pros: Efficient memory usage since only one line is loaded at a time.
	•	Cons: Slower than indexed methods, but necessary for very large files.

2. Binary Search on a Sorted Log File
	•	Approach: If logs were sorted by timestamp, a binary search could quickly locate the starting position for a given date.
	•	Pros: Extremely fast lookups.
	•	Cons: Requires pre-sorted logs, which is not guaranteed.

3. Pre-Indexing Logs by Date
	•	Approach: Create an index mapping dates to byte offsets in the file. Seek directly to the relevant portion.
	•	Pros: Near-instant log retrieval.
	•	Cons: Requires preprocessing and additional storage for the index.

Final Choice: Line-by-Line Scanning

We chose Approach #1 (line-by-line scanning) because:
	•	It works on any log file structure without needing sorting or pre-indexing.
	•	It is memory efficient, processing logs without loading the entire file.
	•	It ensures correctness and simplicity while handling edge cases (e.g., logs missing for a date).

 Final Solution Summary

The final solution:
	1.	Dynamically selects the correct log file based on the year (e.g., logs_2024.log for 2024-12-01).
	2.	Reads the file line by line, checking if the line starts with the given date.
	3.	Saves matching logs into output/output_YYYY-MM-DD.txt.

 
 Steps to Run

1. Compile the C++ Program

g++ sol.cpp -o sol -std=c++17

2. Execute the Program
 ./sol 2024-12-01

3. Check the Output

cat output/output_2024-12-01.txt
