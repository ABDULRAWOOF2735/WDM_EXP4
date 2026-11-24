### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 24.11.26
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("clustervisitor.csv")

X = df["Age"].values
k = 3

centroids = list(X[:k])

while True:
    clusters = [[] for _ in range(k)]
    labels = []

    for value in X:
        distances = [abs(value - c) for c in centroids]
        cluster = distances.index(min(distances))
        clusters[cluster].append(value)
        labels.append(cluster)

    new_centroids = []

    for cluster in clusters:
        if len(cluster) > 0:
            new_centroids.append(sum(cluster) / len(cluster))
        else:
            new_centroids.append(0)

    if new_centroids == centroids:
        break

    centroids = new_centroids

df["Cluster"] = labels

print("\nComplete Dataset\n")
print(df)

for i in range(k):
    print(f"\nCluster {i}\n")
    print(df[df["Cluster"] == i])

```
### Output:
<img width="945" height="752" alt="Screenshot 2026-11-23 181752" src="https://github.com/user-attachments/assets/5c324915-f652-4552-ac87-a7b4dc89f05a" />
<img width="675" height="310" alt="Screenshot 2026-11-23 181801" src="https://github.com/user-attachments/assets/0b5c1df4-34ed-4ae2-9940-60efceca38cd" />
<img width="677" height="332" alt="Screenshot 2026-11-23 181807" src="https://github.com/user-attachments/assets/f8827905-ee40-4e3d-bd34-6fb98276d53e" />
<img width="742" height="290" alt="Screenshot 2026-11-23 181818" src="https://github.com/user-attachments/assets/748fb3b8-ef4d-4539-b18f-2d1973217f3c" />


### Visualization:
```python
colors = ["red", "blue", "green"]

plt.figure(figsize=(8,5))

for i in range(3):
    cluster_data = df[df["Cluster"] == i]
    plt.scatter(cluster_data["Age"],
                [i] * len(cluster_data),
                color=colors[i],
                s=80,
                label=f"Cluster {i}")

plt.scatter(centroids,
            range(3),
            color="black",
            marker="X",
            s=200,
            label="Centroids")

plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.yticks([0, 1, 2], ["Cluster 0", "Cluster 1", "Cluster 2"])
plt.legend()
plt.grid(True)
plt.show()

```
### Output:

<img width="1127" height="632" alt="Screenshot 2026-11-23 181930" src="https://github.com/user-attachments/assets/f930249e-2b22-4087-998c-06707f2873c5" />

### Result:

Thus, the K-Means clustering algorithm was successfully implemented, and the visitors were grouped into different clusters and visualized using a scatter plot.
