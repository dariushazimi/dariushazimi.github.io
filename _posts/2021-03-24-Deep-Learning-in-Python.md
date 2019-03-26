---
layout: post
title: Deep learning in Python
# subtitle: How to get the elements from a list using Map
tags: [Forwared propogation, deep learning, DL]
---

# Neural network and deep learning

Neural networks account for interaction between input layers really well.
Deep learning uses especially powerful neural networks with can handel large number of interactions between the input layers.


## Forward Propagation

Neural networks use models to make predictions, which is called the *forward propogation* algorithm.

Here is an example of calculating output using forward propogation.

![image](https://s3.amazonaws.com/assets.datacamp.com/production/course_3524/datasets/1_4.png)

```
# Calculate node 0 value: node_0_value
node_0_value = (input_data * weights['node_0']).sum()

# Calculate node 1 value: node_1_value
node_1_value = (input_data * weights['node_1']).sum()
    
# Put node values into array: hidden_layer_outputs
hidden_layer_outputs = np.array([node_0_value, node_1_value])

# Calculate output: output
output = (hidden_layer_outputs * weights['output']).sum()

# Print output
print(output)
```
