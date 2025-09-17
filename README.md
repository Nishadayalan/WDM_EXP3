### EX3 Implementation of GSP Algorithm In Python
### DATE:  15-05-2025
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```

from collections import defaultdict
from itertools import combinations

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k, min_support):
    c = defaultdict(int)
    for seq in dataset:
        # Convert each transaction to tuple so it's hashable
        items = [tuple(sorted(itemset)) for itemset in seq]
        # Flatten to single list of items
        flat = [elem for itemset in items for elem in itemset]
        for item in combinations(flat, k):
            c[tuple(sorted(item))] += 1   # store as tuple (hashable)

    # Keep only frequent patterns
    frequent = {items: support for items, support in c.items() if support >= min_support}
    return frequent

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1
    fp = dict()
    while True:
        candidates = generate_candidates(dataset, k, min_support)
        if not candidates:
            break
        fp.update(candidates)
        k += 1
    return fp

dataset1 = [
    [["b","d"], ["c"], ["b"], ["a","c"]],
    [["b","f"], ["c","e"], ["b"], ["f","g"]],
    [["a","h"], ["b","f"], ["a"], ["b"], ["f"]],
    [["b","e"], ["c","e"], ["d"]],
    [["a"], ["b","d"], ["b"], ["c"], ["b"], ["a","d","e"]]
]

dataset2 = [
    [["a","b","c"], ["b","e"], ["c"], ["f"], ["g"], ["a","b","e"]],
    [["a","d"], ["b","c"], ["c"], ["f","g"], ["c","h"]],
    [["b","c"], ["a","d"], ["e"], ["b"], ["f"], ["c","d","f","g","h"]],
    [["c"], ["e","c"], ["e","h"]]
]

# Minimum support threshold
min_support = 3

# Perform GSP algorithm for each dataset
dataset1_result = gsp(dataset1, min_support)
dataset2_result = gsp(dataset2, min_support)

# Output the frequent sequential patterns
print("Frequent Sequential Patterns - Dataset 1:")
if dataset1_result:
    for pattern, support in dataset1_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Dataset 1.")

print("\nFrequent Sequential Patterns - Dataset 2:")
if dataset2_result:
    for pattern, support in dataset2_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Dataset 2.")

```
### Output:


<img width="575" height="502" alt="image" src="https://github.com/user-attachments/assets/c6ed353d-f88d-44c0-badf-858b9ebea32c" />



### Visualization:
```


import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for dataset1 and dataset2
visualize_patterns_line(dataset1_result, 'Dataset 1')
visualize_patterns_line(dataset2_result, 'Dataset 2')



```
### Output:


<img width="1162" height="398" alt="image" src="https://github.com/user-attachments/assets/b0d56f7b-185a-4a0c-a00a-d0041402aee7" />



<img width="1262" height="402" alt="image" src="https://github.com/user-attachments/assets/01988df6-f089-498f-b11b-cd66e1778100" />



### Result:

 Thus to implement GSP Algorithm In Python is executed successfully.


  
