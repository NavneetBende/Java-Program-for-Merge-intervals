Java Program for Merge intervals
This page will go over the program to merge intervals in Java. Given a set of time intervals in any order, we must merge all overlapping intervals into one and output the result, which should only contain mutually exclusive intervals.
For the sake of simplicity, let the intervals be represented as pairs of integers.

Kadane’s Algorithm
Example :

Consider the input array below. Intervals (1, 5), (3, 7), (4, 6), (6, 8) are overlapping so they should be merged to one big interval (1, 8). Similarly, intervals (10, 12) and (12, 15) are also overlapping and should be merged to (10, 15).

Algorithm
Initialize by setting max so far to INT MIN and max ending here to 0.

 

For each array element, repeat the loop.
                   (a) max ending here equals max ending here + a[i]

                   (b) if(max so far max end here)

maximum so far = maximum ending here
                  (c) if (max ending here=0)

maximum end here = 0
return max_so_far
merge intervals
Note
The runtime complexity of this solution is linear, O(n)
Code in JAVA
Run
import java.util.Arrays;
import java.util.Comparator;
import java.util.Stack;
public class Main {

public static void mergeIntervals(Interval arr[])
{
// Test if the given set has at least one interval
if (arr.length <= 0)
return;

// Create an empty stack of intervals
Stack<Interval> stack=new Stack<>();

// sort the intervals in increasing order of start time
Arrays.sort(arr,new Comparator<Interval>(){
public int compare(Interval i1,Interval i2)
{
return i1.start-i2.start;
}
});

// push the first interval to stack
stack.push(arr[0]);

// Start from the next interval and merge if necessary
for (int i = 1 ; i < arr.length; i++)
{
// get interval from stack top
Interval top = stack.peek();

// if current interval is not overlapping with stack top,
// push it to the stack
if (top.end < arr[i].start)
stack.push(arr[i]);

// Otherwise update the ending time of top if ending of current
// interval is more
else if (top.end < arr[i].end)
{
top.end = arr[i].end;
stack.pop();
stack.push(top);
}
}

// Print contents of stack
System.out.print("The Merged Intervals are: ");
while (!stack.isEmpty())
{
Interval t = stack.pop();
System.out.print("["+t.start+","+t.end+"] ");
}
}

public static void main(String args[]) {
Interval arr[]=new Interval[4];
arr[0]=new Interval(6,8);
arr[1]=new Interval(1,9);
arr[2]=new Interval(2,4);
arr[3]=new Interval(4,7);
mergeIntervals(arr);
}
}

class Interval
{
int start,end;
Interval(int start, int end)
{
this.start=start;
this.end=end;
}
}
Output
The Merged Intervals are: [11,16] [8,9] [1,6] 
