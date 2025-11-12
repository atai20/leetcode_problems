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
