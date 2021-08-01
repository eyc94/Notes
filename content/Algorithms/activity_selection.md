# Activity-Selection Problem

- Scheduling several competing activities that require exclusive use of a common resource, with a goal of maximum-size set of mutually compatible activities.
- Suppose we have a set *S = {a<sub>1</sub>, a<sub>2</sub>,..., a<sub>n</sub>}* of *n* proposed **activities** that wish to use a resource, such as a lecture hall, which can only serve one activity at a time.
- Each activity *a<sub>i</sub>* has a **start time** *s<sub>i</sub>* and a **finish time** *f<sub>i</sub>*, where 0 ≤ *s<sub>i</sub>* < *f<sub>i</sub>* < ∞.
- Selected activity, *a<sub>i</sub>*, takes place during half-open time interval \[*s<sub>i</sub>*, *f<sub>i</sub>*).
- Activities *a<sub>i</sub>* and *a<sub>j</sub>* are **compatible** if the intervals \[*s<sub>i</sub>*, *f<sub>i</sub>*) and \[*s<sub>j</sub>*, *f<sub>j</sub>*) do not overlap.
- *a<sub>i</sub>* and *a<sub>j</sub>* are compatible if *s<sub>i</sub>* ≥ *f<sub>j</sub>* or *s<sub>j</sub>* ≥ *f<sub>i</sub>*.
    - Basically, one activity has to come and finish before the other to be non-overlapping.
- In this problem, we want to select a maximum-size subset of mutually compatible activities.
- Assume activities are sorted in monotonically increasing order of finish time.
    - *f<sub>1</sub>* ≤ *f<sub>2</sub>* ≤ *f<sub>3</sub>* ≤ ... ≤ *f<sub>n - 1</sub>* ≤ *f<sub>n</sub>*.

Consider the activities below:

![alt text](https://github.com/eyc94/Notes/blob/master/images/activity_selection_table.png "Image of example of activities")