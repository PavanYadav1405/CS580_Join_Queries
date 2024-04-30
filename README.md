# CS580_Join_Queries
CS 580 – Project Report 

By
Pavan Kumar Yadav Dukka
Shahbaz Syed
Sai Kiran Reddy Gorla

Github Repository Link – 
https://github.com/PavanYadav1405/CS580_Join_Queries

Option – IV – Algorithms’ Implementation
Problem 01:
1.	 Dataset Creation:
Let's create a sample dataset with 10 tuples each in R1 and R2.
R1:
(1, 2)
(3, 4)
(5, 6)
(7, 8)
(9, 10)
(11, 12)
(13, 14)
(15, 16)
(17, 18)
(19, 20)

R2:
(2, 21)
(4, 22)
(6, 23)
(8, 24)
(10, 25)
(12, 26)
(14, 27)
(16, 28)
(18, 29)
(20, 30)

2.	Algorithm Implementation:
We will use a hash table to store the tuples of R2, with the values of attribute B as keys and the corresponding tuples as values.
3.	Time Complexity Analysis:
Creating the hash table:
Iterating over all tuples in R2 to create the hash table takes O(n) time, where n is the number of tuples in R2.
Performing the join:
Iterating over all tuples in R1 takes O(m) time, where m is the number of tuples in R1.
For each tuple in R1, performing a lookup in the hash table takes amortized constant time, O(1).
Joining the tuples from R1 and R2 takes constant time, O(1).
Therefore, the overall time complexity of the join operation is O(m).
The overall time complexity of Our solution is O(m + n), where m is the number of tuples in R1, and n is the number of tuples in R2. This is because creating the hash table takes O(n) time, and performing the join takes O(m) time.

4.	Correctness Explanation:
The algorithm is correct because it correctly evaluates the join query q(A, B, C) :- R1(A, B), R2(B, C) by iterating over the tuples of R1 and checking if the corresponding value of attribute B exists as a key in the hash table constructed from R2. If a match is found, all tuples in R2 with that value of attribute B are joined with the current tuple from R1 to produce the resulting tuples.
The time complexity of this algorithm is O(m + n), where m is the number of tuples in R1, and n is the number of tuples in R2. This is because we iterate over R1 once (O(m)) and perform constant-time lookups in the hash table for each tuple in R1 (amortized O(1) time for each lookup). The space complexity is O(n) since we store all tuples of R2 in the hash table.

5.	Output:
Running the algorithm on the given dataset will produce the following result:


(1, 2, 21)
(3, 4, 22)
(5, 6, 23)
(7, 8, 24)
(9, 10, 25)
(11, 12, 26)
(13, 14, 27)
(15, 16, 28)
(17, 18, 29)
(19, 20, 30)
This result correctly represents the join of R1 and R2 based on the condition q(A, B, C) :- R1(A, B), R2(B, C).















Problem 02:

1.	Implementation:
a.	First, we implemented the 4-line join specified in the Problem statement.
b.	Next, we generalized it for k-line queries.

2.	Test Cases:
a.	 Simple Line Join Query – 
i.	Input - R1 = [(1, 2), (3, 4), (5, 6)], R2 = [(2, 7), (4, 8), (6, 9)], R3 = [(7, 10), (8, 11), (9, 12)]
ii.	Output = [(1, 2, 7, 10), (3, 4, 8, 11), (5, 6, 9, 12)]

b.	Line Join Query with Empty Relations – 
i.	Input - R1 = [(1, 2), (3, 4)], R2 = [], R3 = [(7, 10), (8, 11)]
ii.	Output – []

c.	Line Join Query with No Matching Tuples – 
i.	Input - R1 = [(1, 2), (3, 4)], R2 = [(5, 6), (7, 8)], R3 = [(9, 10), (11, 12)]
ii.	Output – []

d.	Tuples with negative values – 
i.	Input - R1 = [(0, 1), (1, 2), (2, 3)], R2 = [(1, 4), (2, 5), (3, 6)], R3 = [(4, -1), (5, -2), (6, -3)]
ii.	Output – [(0, 1, 4, -1), (1, 2, 5, -2), (2, 3, 6, -3)]

e.	 Line Join Query with Duplicate Tuples – 
i.	Input - R1 = [(1, 2), (3, 4), (1, 2)], R2 = [(2, 5), (4, 6), (2, 5)], R3 = [(5, 7), (6, 8), (5, 7)]
ii.	Output – [(1, 2, 5, 7), (1, 2, 5, 7), (1, 2, 5, 7), (1, 2, 5, 7), (3, 4, 6, 8), (1, 2, 5, 7), (1, 2, 5, 7), (1, 2, 5, 7), (1, 2, 5, 7)]

3.	Time Complexity Analysis:

Our solution consists of two main parts:

1. The ‘semijoin’ function:
   - This function performs a semijoin reduction by filtering the tuples in `relation1` based on the values in `relation2`.
   - The time complexity of this function is O(M + N), where M is the size of `relation1`, and N is the size of `relation2`.

2. The ‘join’ function:
   - This function performs a hash-based join between two relations.
   - The time complexity of building the hash index is O(N), where N is the size of `relation2`.
   - The time complexity of the join operation is O(M), where M is the size of `relation1`.
   - Therefore, the overall time complexity of the `join` function is O(M + N).

3. The ‘k_line_join’ function:
   - This function performs successive joins on the list of relations.
   - The time complexity of this function is O(N * (k - 1) + OUT), where N is the size of each relation, k is the number of relations, and OUT is the size of the output.

4. The ‘process_and_join’ function:
   - This function performs semijoin reductions on the relations before calling `k_line_join`.
   - The time complexity of the semijoin reductions is O(N * (k - 1)), where N is the size of each relation, and k is the number of relations.
   - The time complexity of `k_line_join` is O(N * (k - 1) + OUT), where OUT is the size of the output.
   - Therefore, the overall time complexity of `process_and_join` is O(N * (k - 1) + OUT).

In the given problem statement, the assumption is that each relation has N tuples, and the domain of each attribute is Z (the set of integer numbers). Additionally, the focus is on k-line join queries for k ≤ 10.

Under these assumptions, the time complexity of your solution is O(N * (k - 1) + OUT), which satisfies the requirement of O(N + OUT) time complexity for k-line join queries.

4.	Correctness Analysis:

1. The `semijoin` function correctly filters the tuples in `relation1` based on the values in `relation2`.
2. The `join` function correctly performs a hash-based join between two relations, handling duplicates appropriately.
3. The `k_line_join` function correctly performs successive joins on the list of relations, using the `join` function.
4. The `process_and_join` function correctly performs semijoin reductions on the relations before calling `k_line_join`.

Our solution handles various test cases, including simple line join queries, queries with empty relations, queries with no matching tuples, tuples with negative values, and queries with duplicate tuples. The output matches the expected results in all these test cases.
















Problem 03:

Algorithm Implementation - 

The algorithm is structured into two main parts:

1.	The Join Function:
Purpose: This function performs an inner join between two relations. For each tuple in the first relation, it searches for tuples in the second relation where the join condition is met. The join condition is that the last attribute of a tuple from the first relation matches the first attribute of a tuple from the second relation.
Implementation: It iterates over each tuple in the first relation, then iterates over each tuple in the second relation. If the last element of the tuple from the first relation equals the first element of the tuple from the second relation, the tuples are joined. The join excludes the repeated attribute to avoid redundancy in the resulting tuples.

2.	Chain Join Function:
Purpose: This function sequentially applies the join operation across a series of relations, starting from the first relation and incrementally incorporating each subsequent relation through the join.
Implementation: It initializes the result with the first relation and iteratively joins this result with each subsequent relation in the list. The join operation is performed using the previously defined join function.


Time Complexity Analysis - 

1. `hash_join` function:
   - Building the hash table for R2 takes O(n) time, where n is the number of tuples in R2.
   - Performing the join operation takes O(m) time, where m is the number of tuples in R1. This is because we iterate over each tuple in R1, and for each tuple, we perform a constant-time lookup in the hash table and join operations.
   - Therefore, the overall time complexity of the `hash_join` function is O(m + n).

2. `chain_join` function:
   - The `chain_join` function iterates over the list of relations, and for each relation, it calls the `hash_join` function with the current result and the new relation.
   - Assuming there are k relations, and each relation has N tuples, the time complexity of the `chain_join` function is O(k * N^2).


Correctness Explanation – 

1. Compliance with Join Conditions: Each step of the join ensures that tuples are combined only when they meet the specified join condition (matching attributes as per the chain's requirements). This ensures that no invalid tuple combinations are included in the result.
2. Sequential Processing: The chain join operation processes the relations in a sequential manner, preserving the logical order of joins as specified. This maintains the relational model's integrity, where each join builds upon the last, aligning with how SQL and other relational databases process multi-table joins.
3. No Data Loss or Duplication: The join excludes the repeated attribute from the second tuple, preventing redundancy in the output. Moreover, since every tuple that meets the join condition is included, no valid data is lost.
4. Generality and Flexibility: The implementation is general and flexible, working with any number of relations as long as they are connected by compatible join attributes. This simulates a real-world scenario where different database tables might be joined based on common keys.


















Problem 04:

1. Dataset Generation:
   - The datasets R1, R2, and R3 are generated according to the specifications provided in the problem statement.
   - R1 contains 100 tuples of the form (i, random_value), where i ranges from 1 to 100, and random_value is a random integer between 1 and 5000.
   - R2 contains 100 tuples of the form (random_value, j), where j ranges from 1 to 100, and random_value is a random integer between 1 and 5000.
   - R3 contains 100 tuples of the form (l, l), where l ranges from 1 to 100.

2. Running the Algorithm from Problem 2 (K_Line_Joins):
   - The `K_Line_Joins` class is used to perform semijoin reductions and k-line joins on the given relations (R1, R2, and R3).
   - The `process_and_join` method is called with the list of relations [R1, R2, R3].
   - The final result is printed, showing 4 tuples of the form (value1, value2, value3, value3), where value1 and value2 are from R1, value3 is from R2, and the last value3 is from R3.

3. Running the Algorithm from Problem 3 (Chain_Joins):
   - The `Chain_Joins` class is used to perform a chain join on the given relations (R1, R2, and R3).
   - The `chain_join` method is called with the list of relations [R1, R2, R3].
   - The final result is printed, showing the same 4 tuples as the result from the algorithm in Problem 2.

4. Performance and Result Comparison:
Performance: The code includes the profiling of both the k-line join and chain join methods, sorting the results by cumulative time, which would provide insights into the efficiency of each method.
Result Equality: There is a conditional check in the code to compare the results of the k-line joins and the chain joins to see if they produce identical outputs.

In summary, the provided code generates the specified datasets (R1, R2, and R3) and runs the algorithms from Problems 2 and 3 on these datasets for a 3-line join query. Both algorithms produce the same result, which is a set of 4 tuples representing the join of the three relations. The algorithm from Problem 2 (K_Line_Joins) has a better time complexity of O(IN + OUT), while the algorithm from Problem 3 (Chain_Joins) has a higher time complexity of O(k * n^2), where k is the number of relations.


Problem 05:
Dataset Description - 
R1: Consists of 2001 tuples. The first 1000 tuples are in the form (i, 5) where i ranges from 1 to 1000. The next 1000 tuples are in the form (i, 7) where i ranges from 1001 to 2000. The final tuple is (2001, 2002).
R2: Contains 1001 tuples. The first 1000 tuples are (5, i) where i ranges from 1 to 1000. The next 1000 tuples are (7, i) where i ranges from 1001 to 2000. The final tuple is (2002, 8).
R3: Contains 2001 tuples. 2000 tuples are randomly generated with x values ranging from 2002 to 3000, and y values ranging from 1 to 3000. The last tuple is (8, 30).

Implementations and Results - 
Method from Problem 2
- Implementation: This method likely employs a modified Yannakakis algorithm designed for efficient line join queries. It should run in O (N + OUT) time, where N is the number of tuples and OUT is the number of output tuples.
- Results: This method would be particularly efficient for large N, as it avoids unnecessary computational overhead by progressively filtering and joining tuples.
Method from Problem 3
- Implementation: Uses a simpler, step-by-step join approach starting with smaller join results and incrementally joining them with the next relation in the sequence.
- **Results**: This approach might result in larger intermediate results, especially if there are many potential joining tuples, thus consuming more memory and potentially leading to slower performance compared to the optimized method from Problem 2.

Performance Comparison - 
- Speed: The method from Problem 2 is designed to be faster as it directly reduces the unnecessary intermediate results and computations. It should be more scalable when dealing with large datasets. K-line joins – 0.002 sec, Chain join – 0.512 sec
- Memory Usage: Problem 3's method, depending on the distribution and number of joining tuples, might consume more memory due to larger intermediate join results.
Conclusion
Both methods should ideally return the same final join results if implemented correctly. However, the method from Problem 2 is expected to be faster and more memory-efficient due to its optimized design. This efficiency is particularly evident in scenarios where the dataset and potential output size are large.

Problem 06:
MySQL Query:
CREATE TABLE R1 (A INT, B INT);
CREATE TABLE R2 (B INT, C INT);
CREATE TABLE R3 (C INT, D INT);
 
INSERT INTO R1 (A, B) VALUES
(178, 5), (957, 5), (412, 5), … , (1730, 7), (1263, 7), (897, 5);

INSERT INTO R2 VALUES
(7, 1077), (7, 1152), (5, 907), …  , (7, 1646), (7, 1453), (7, 1461);

INSERT INTO R3 VALUES
(2775, 2347), (2800, 1590), … , (2018, 1128), (2548, 1730), (2292, 1881);

SELECT *
FROM R1
JOIN R2 ON R1.B = R2.B
JOIN R3 ON R2.C = R3.C;
Output:
The MySQL gave the exact same output as problem 5 output.
Analysis:
Correctness: The fact that MySQL gave the same results as your other implementations validates the correctness of your algorithms, ensuring that all implementations conform to the expected behavior of the 3-line join.
Performance Comparison:
MySQL's performance is closer to that of the implementation from Problem 2. It suggests that optimizations similar to those in the Yannakakis algorithm (like join order optimization, minimal intermediate result generation) are effective.
![image](https://github.com/PavanYadav1405/CS580_Join_Queries/assets/78838313/8a6f3549-fa49-45f2-9dda-000402217505)
