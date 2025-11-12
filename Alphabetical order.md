So this problem is from one of the interviews I had, it asked to perform basic insertion sort which I totally forgot.

My tactics were to move the point to the right side, check if the value is smaller than the previous one if it is I wanted to replace the values involved. the code didn't work and unfortunatelly I don't have it here since it was lost in the form. It was something like that:
```python
accepted_students = [] 
# try insertion sort for i in records: 
if (i["gpa"] >=3.5 and i["credits"]>=12): 
  accepted_students.append(i["name"])

for i2 in range(1, len(accepted_students)):
  i3 = i2-1
  if (accepted_students[i2-1] > accepted_students[i2]) # <- added to test after reviewing
    while(accepted_students[i3] > accepted_students[i2]):
      if (i3 != 0):
        i3 -= 1
      else:  # <- added to test after reviewing
        break  # <- added to test after reviewing
    temp = accepted_students[i3]
    accepted_students[i3] = accepted_students[i2]
    accepted_students[i2] = temp

```

but after running it even the start of the for loop didn't work for some reason. 

The problem was in swapping, aparently it should happen inside the while loop becase i3 will never escape the loop hence not swapped, so working version is this:
```python
accepted_students = [] 
# try insertion sort for i in records: 
if (i["gpa"] >=3.5 and i["credits"]>=12): 
  accepted_students.append(i["name"])

for i2 in range(1, len(accepted_students)):
  i3 = i2-1
  if (accepted_students[i2-1] > accepted_students[i2]) # <- added to test after reviewing
    while(accepted_students[i3] > accepted_students[i2]):
      if (i3 != 0):
        i3 -= 1
      else:  # <- added to test after reviewing
        break  # <- added to test after reviewing
      temp = accepted_students[i3] #<-inside the loop now
      accepted_students[i3] = accepted_students[i2] #<-inside the loop now
      accepted_students[i2] = temp #<-inside the loop now
```

There are still problems in that code. The correct approach should be reviewed(according to gemini):

```python
accepted_students = []

# 1. Selection (This part is correct assuming 'records' is a list of dicts)
# for i in records:
#   if (i["gpa"] >= 3.5 and i["credits"] >= 12):
#     accepted_students.append(i["name"])

# --- Example for demonstration (replace with your actual selection logic) ---
accepted_students = ["Zoe", "Alice", "Bob", "Charlie", "David"]
# --------------------------------------------------------------------------

# 2. Insertion Sort
for i in range(1, len(accepted_students)):
    # Store the element to be inserted (the "key")
    key = accepted_students[i]
    
    # Start comparing with the element just before 'key'
    j = i - 1
    
    # Move elements of accepted_students[0..i-1], that are greater than key, 
    # to one position ahead of their current position
    while j >= 0 and key < accepted_students[j]:
        accepted_students[j + 1] = accepted_students[j]
        j -= 1
        
    # Insert the key into its correct sorted position
    accepted_students[j + 1] = key

# accepted_students is now sorted alphabetically
# print(accepted_students)


```
