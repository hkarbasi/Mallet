# Mallet
======

The patch for recent `Mallet-v2.0.8`

## Patch

All you should do is to replace the files with the existing ones; 
For:

* java files: `/src/cc/mallet/topics/` 
* class files: `/class/cc/mallet/topics`

It resolves the issues for me as I haven’t seen Mallet break and throw Exception again under different circumstances. If it doesn’t resolve your issues, you should probably download the latest version from github (https://github.com/mimno/Mallet), debug and build it yourself.

## My experience

Recently, I ran Mallet with two different datasets (one with 100M and the other one around 1G). Usually this kind of exception happened with the larger dataset and when I wanted to run in in parallel for larger iteration numer like 100 for the larger dataset. It threw `Exception :ArrayIndexOutOfBoundsException` in two different files:  `WorkerRunnable` and `ParallelTopicModel` in different spots. So the thing is when the array reaches the end of the array, it prints `overflow in merging on type` to the logger and after that point, the program doesn’t do anything to get out of the situation. I was able to patch these edge cases with index checking before accessing to the array. It helps me run it without breaking it but I am not sure how it might change the output anyways and it also keeps printing the same message `overflow in merging on type` as usuall but it goes on and doesn’t throw any exception.
