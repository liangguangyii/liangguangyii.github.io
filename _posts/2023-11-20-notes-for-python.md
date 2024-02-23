---
layout: post
title: Notes for Python
tags: [Python, "Computer Science"]
categories: code
giscus_comments: true
related_posts: true
date: 2023-11-20
toc:
  sidebar: left
---

## Recurrence

This is an example about how recursion works in search all possible combinations of a given set of list, beside with additional insert function to insertion another list into the input list during recursion.

### Basic Recursion

```python
def iterate(current_loop, max_loop, iterate_range, current_path = [], result = None):

if result == None:
    result = []

#* the interation count for the current interation
#* the interval between max_loop and current_loop narrows after each interation
index = len(iterate_range) - (max_loop - current_loop + 1)

#* otherwise in the first loop the index will be minus
assert index >= 0, \
    "the length of iterate_loop mismatches the number of loop."

if current_loop > max_loop:
    result.append(current_path)
    return

for i in range(iterate_range[index]):
    iterate(current_loop + 1, max_loop, iterate_range, current_path + [i], result)

return result
```

Here are something to notice:

- Only the parameters of a function could be passed in the nexr recursion, so the value should be stored in the function's parameters.

- When it reaches the base level of the recurrence, the result should be returned. 

For this example, in the first step of the loop, the function keeps nesting unitl it reaches the reutrn condition -- current_loop > max_loop. Then it returns to the level which current_loop = max_loop, continues the next step of loop, and so on.

After the loop in the level of current_loop = max_loop, the function returns to the level of current_loop = max_loop - 1, and so on.

For a simple example:

```python
current_loop = 1
max_loop = 3
iterate_range = [4, 3, 2] 

result = iterate(current_loop, max_loop, iterate_range)
```

The output result is:
```python
[0, 0, 0]
[0, 0, 1]
[0, 1, 0]
[0, 1, 1]
[0, 2, 0]
[0, 2, 1]
[1, 0, 0]
[1, 0, 1]
[1, 1, 0]
[1, 1, 1]
[1, 2, 0]
[1, 2, 1]
[2, 0, 0]
[2, 0, 1]
[2, 1, 0]
[2, 1, 1]
[2, 2, 0]
[2, 2, 1]
[3, 0, 0]
[3, 0, 1]
[3, 1, 0]
[3, 1, 1]
[3, 2, 0]
[3, 2, 1]
```


## Pointer, swallow copy and deep copy in python

### Swallow copy and deep copy

Swallow copy only copies the object itself and its pointer, for list elemets, that means it only copy the pointer of the list elements, not the elements of list.

And the deep copy will create a new object independently and copy the elements of the object.

For example:

```python
a = [1, 2, 3, 4, ['a', 'b']] 
 
b = a                       
c = copy.copy(a)           
d = copy.deepcopy(a)        
 
a.append(5)                 
a[4].append('c')            
 
print( 'a = ', a )
print( 'b = ', b )
print( 'c = ', c )
print( 'd = ', d )
```

The output is:

```python
('a = ', [1, 2, 3, 4, ['a', 'b', 'c'], 5])
('b = ', [1, 2, 3, 4, ['a', 'b', 'c'], 5])
('c = ', [1, 2, 3, 4, ['a', 'b', 'c']])
('d = ', [1, 2, 3, 4, ['a', 'b']])
```

### In the view of pointer

The in place operation will change the object itself, and the object's pointer will not be changed.

Besides, if the object that are operated are list, then actually it is the pointer of the list elements that are viewd as the object.

For a Fucking sick example:

```python
def insert_into_input_list(input_list, insert_index, insert_list):

    output_list = []
    output_list_for_list = []
    temp_list = []
    current_list = []
    
    #* for the permutation and combination of the input_list, each first level list could could contribute one element to the final list
    #* the the number of the recurrsion layers equal to the length of the fianl list
    #* and each element in the final list corresponds to one recurrsion layer
    for inlist in input_list:
        counter = 0
        temp_list = inlist.copy()
        for i in range(len(insert_index)):
            if isinstance(insert_list[i], list):

                current_list = temp_list.copy()
                for j in range(len(insert_list[i])):
                    temp_list.insert(insert_index[i] + 1 + counter, insert_list[i][j])
                    output_list.append(temp_list)
                    temp_list = current_list.copy()
                counter += 1
            elif insert_list[i] == None:
                pass
            else:
                temp_list.insert(insert_index[i] + 1 + counter, insert_list[i])
                output_list.append(temp_list)
                counter += 1
        
    
    return output_list
```

```python
fch_filename = 'Au8Pt5tddft.fch'
LOG_filename = 'AU8PT5TDDFT.LOG'
excited_states_list = [13, 14, 15]
input_list = [[fch_filename], [18], [1], [LOG_filename], [excited_states_list], [1], [3], \
    [10], [11], [12], [13], [14], [15], [16]]
insert_list = [1, 1, 2, [1, 2, 3, 4]]
insert_index = [7, 8, 9, 11]
Multiwfn_input_list = iterate_list(1, len(input_list), input_list)

Multiwfn_output_list = insert_into_input_list(Multiwfn_input_list, insert_index, insert_list)

for i in range(len(Multiwfn_output_list)):
    print (Multiwfn_output_list[i])
```

The output is:

```python
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 13, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 13, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 13, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 13, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 13, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 2, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 13, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 3, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 13, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 4, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 14, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 14, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 14, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 14, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 14, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 2, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 14, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 3, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 14, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 4, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 15, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 15, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 15, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 15, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 1, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 15, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 2, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 15, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 3, 15, 16]
['Au8Pt5tddft.fch', 18, 1, 'AU8PT5TDDFT.LOG', 15, 1, 3, 10, 1, 11, 1, 12, 2, 13, 14, 4, 15, 16]
```

And the function `iterate_list` is defined as follows:

```python
def iterate_list(current_loop, max_loop, input_list, current_list = [], result = None):

    if result == None:
        result = []

    if current_loop > max_loop:
        result.append(current_list)
        return

    index = len(input_list) - (max_loop - current_loop + 1)
    assert index >= 0, \
        'length of input_list and the number of loops are not compatible!'

    loop_range = len(input_list[index])

    for i in range(loop_range):
        if isinstance(input_list[index][i], list):
            for j in range(len(input_list[index][i])):
                iterate_list(current_loop + 1, max_loop, input_list, current_list + [input_list[index][i][j]], result)
        elif input_list[index][i] == None:
            iterate_list(current_loop + 1, max_loop, input_list, current_list, result)
        else:
            iterate_list(current_loop + 1, max_loop, input_list, current_list + [input_list[index][i]], result)

    return result
```


It's insane, right? And it doesn't work.

We have already known the `.append` is in place operator, thus the `temp_list` appended into `outpu_list` in the else statement have the same pointer, thus there will be three same list generated from else statement, for this example.

However, how dows another `1` append into these three list? I have already reset `temp_list` in the j-loop, I mean `temp_list = current_list.copy()`. In the first loop of j-loop, the pointer of `temp_list` doesn't change, that's why there is `1` after `14` in the first three list and the fitst list in generated in j-loop, the four lists share the same pointer, any in place modification on any one of it will chage them all.

After `temp_list = current_list.copy()`, the pointer of `temp_list` changes, and the last three lists are indenpendent.