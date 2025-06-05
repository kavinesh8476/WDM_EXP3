### EX3 Implementation of GSP Algorithm In Python

#### DATE: 

#### AIM: 
To implement GSP Algorithm In Python.

#### Description:

The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.

#### Steps:

1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

#### Procedure:

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

#### Program:

```
from collections import defaultdict
from itertools import combinations
import matplotlib.pyplot as plt
from prettytable import PrettyTable

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidate_counts = defaultdict(int)
    for sequence in dataset:
        for combo in combinations(sequence, k):
            candidate_counts[combo] += 1
    return candidate_counts

# GSP algorithm
def gsp(dataset, min_support):
    k = 1
    frequent_patterns = {}
    while True:
        candidate_counts = generate_candidates(dataset, k)
        current_frequent = {}
        for pattern, count in candidate_counts.items():
            if count >= min_support:
                current_frequent[pattern] = count
        if not current_frequent:
            break
        frequent_patterns.update(current_frequent)
        k += 1
    return frequent_patterns

# Pretty table display
def display_results(title, result):
    print(f"Frequent Sequential Patterns - {title}")
    if result:
        table = PrettyTable()
        table.field_names = ["Pattern", "Support"]
        for pattern, support in result.items():
            table.add_row([str(pattern), support])
        print(table)
    else:
        print("No frequent sequential patterns found in this category.\n")

# Sample dataset for each category
top_wear_data = [
    ["blouse", "t-shirt", "tank_top"],
    ["hoodie", "sweater", "top"],
    ["hoodie"],
    ["hoodie", "sweater"]
]

bottom_wear_data = [
    ["jeans", "trousers", "shorts"],
    ["leggings", "skirt", "chinos"],
    ["leggings", "jeans", "shorts"]
]

party_wear_data = [
    ["cocktail_dress", "evening_gown", "blazer"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress"],
    ["party_dress"]
]

# Minimum support
min_support = 2

# Run GSP for each category
top_wear_result = gsp(top_wear_data, min_support)
bottom_wear_result = gsp(bottom_wear_data, min_support)
party_wear_result = gsp(party_wear_data, min_support)

# Display results in table format
display_results("Top Wear", top_wear_result)
display_results("Bottom Wear", bottom_wear_result)
display_results("Party Wear", party_wear_result)
```
#### Output:

![{5B90331E-910E-488A-9BB2-F0257207A0C6}](https://github.com/user-attachments/assets/3d420f6e-f82e-47f4-b340-715d4036501f)

#### Visualization:
```
# Line plot visualization
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
# Visualize results
visualize_patterns_line(top_wear_result, "Top Wear")
visualize_patterns_line(bottom_wear_result, "Bottom Wear")
visualize_patterns_line(party_wear_result, "Party Wear")
```
#### Output:

![{3B7618CE-30DF-4F5D-ADEA-4EF728D9C54D}](https://github.com/user-attachments/assets/db235102-0448-4819-9a8e-d9f2a615391a)
![{8064E391-13C1-493C-B2A6-329D9BA42042}](https://github.com/user-attachments/assets/88f7992e-fd2e-4743-ad4b-015b129e463d)
![{A5B71A29-FDBB-4803-964F-8788D83BDF9F}](https://github.com/user-attachments/assets/63024ed6-0265-4e42-b0d1-c33c4d39e497)

#### Result:
Thus, the implementation of the GSP algorithm in Python has been successfully executed.
