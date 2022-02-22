# DMassjava


Apriori and FP-tree
This project is an assignemnt of the Data Mining Course(COL761) at IIT Delhi.

Apriori Algorithm and FP-tree are used to mine frequent itemsets on this dataset: http://fimi.ua.ac.be/data/retail.dat Details about the dataset can be found at http://fimi.ua.ac.be/data/retail.pdf It is assumed that all items are integers.

The repository contains the following files:

(1) <rollnumber>.sh and compile.sh:
Executing the command: sh <rollnumber>.sh retail.txt X -apriori output generates a file output.txt containing the frequent itemsets at >=X% support threshold with the Apriori algorithm. Similarly, executing the command sh <rollnumber>.sh retail.txt X -fptree output generates a file output.txt containing the frequent itemsets using FP-tree algorithm. X is in percentage and not the absolute count. Our implementations ensure that the transactions are not loaded into main memory. However, the frequent patterns and candidate sets are stored in memory.

output.txt follows the following format:

Each frequent itemset is on a new line.
The items in each itemset are space separated.

(2) FPTree.java
(3) Apriori.java
(4) Test.java: Contains the main function. Executes fp-growth or apriori depending on the arguments given. Call to this is made by the bash file
(5) plot.py
Generates a plot using matplotlib where the x-axis varies the support threshold and y-axis shows the corresponding running times. It plots the running times of apriori and fptree at support thresholds of 1%, 5%, 10%, 25%, 50%, and 90%

The performance of Apriori algorithm is compared with FP-tree in the report.

Executing the command: sh <rollnumber>.sh retail.txt -plot generates a plot using plot.py The results obtained are explained as follows.

Performance of FP-growth v/s Apriori
We observe that the running time of FP-growth is lesser than Apriori algorithm. Also, with increase in support threshold, the running time of both Apriori and FP-growth decrease. The decrease for FP-growth is less as compared to Apriori.

In Apriori, the pattern matching operation of comparing candidate sets with transactions becomes expensive due to the increasing size of candidate sets. As large number of candidates are generated, they require more memory space. The breadth first search approach can be quite costly in terms of memory as it requires at any moment to keep in the worst case all k and k − 1 itemsets in memory (for k > 1).

On the other hand, for fp-tree, there is no candidate generation and hence it requires less memory. It removes the need to calculate the pairs to be counted (which requires expensive computation). The FP-Growth algorithm stores in memory a compact version of the database. A major advantage of fp-growth algorithm is that it only explores the frequent itemsets in the search space, thus avoiding considering many itemsets not appearing in the database, i.e., infrequent itemsets.

With the increase in number of items, more search space is needed and I/O will also increase for Apriori. Apriori requires more database scans as compared to fp-growth; whenever new candidates are generated, DB scan is required. However, FP- tree requires only 2 DB scans. Thus, fp-growth is much better computationally.

Another limitation of Apriori is that the time complexity is O(m^2 * n), where m is the number of distinct items and n is the number of transactions. On the other hand, fp-growth algorithm is O(n) which is much faster than Apriori.
