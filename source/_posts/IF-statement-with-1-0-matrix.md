title: 'IF statement with {1,0} matrix'
date: 2021-03-02 14:45:12
tags:
---

Today, I was trying to use VLookup function in excel to find a particular item in one column with multiple criteria in other columns. It can be done with adding extra columns first to create one real column to look up for and attach the data column you are looking for after that artificial column. For example, you can combine column A&B&C to merge them into one column, so that you can use VLOOKUP(item_A&item_B&item_C, A&B&C&data_column, 2, 0) to find the result.

To avoid making extra columns, in this case, A&B&C&data_column, I found we can also use IF({1, 0}, A&B&C, data_column) to make such matrix instead of actually copying & pasting to create one. Because IF function can work with array {1, 0} as logical tests, so basically it runs the first test with 1 (i.e. True) and then again with 0 (i.e False), in the end, it generates the result matrix A&B&C & data_column. Really impressive because it looks simple and elegant.