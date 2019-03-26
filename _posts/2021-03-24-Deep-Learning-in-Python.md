---
layout: post
title: Deep learning in Python
# subtitle: How to get the elements from a list using Map
tags: [Forward propagation, deep learning, DL]
---

# Neural network and deep learning

Neural networks account for interaction between input layers really well.
Deep learning uses especially powerful neural networks with can handle large number of interactions between the input layers.


## Forward Propagation

Neural networks use models to make predictions, which is called the *forward propagation* algorithm.

Here is an example of calculating output using forward propagation.

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

## Activation function
Activation function allows us to capture how changes in input will impact the output.

i.e. How going from 2 children to 3 children will change the number of transactions?

Or how going from 2 account to 4 account will again change the output?

In other words activation functions help us in capturing non linearities.

## Rectified Linear Activation Function

Here is an example of a `ReLU`  function.

```
def relu(input):
    '''Define your relu activation function here'''
    # Calculate the value for the output of the relu function: output
    output = max(input, 0)
    
    # Return the value just calculated
    return(output)

# Calculate node 0 value: node_0_output
node_0_input = (input_data * weights['node_0']).sum()
node_0_output = relu(node_0_input)

# Calculate node 1 value: node_1_output
node_1_input = (input_data * weights['node_1']).sum()
node_1_output = relu(node_1_input)

# Put node values into array: hidden_layer_outputs
hidden_layer_outputs = np.array([node_0_output, node_1_output])

# Calculate model output (do not apply relu)
model_output = (hidden_layer_outputs * weights['output']).sum()

# Print model output
print(model_output)
```
