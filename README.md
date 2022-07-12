<!-- HackMD link: https://hackmd.io/JiIgyQ7QT9i12-y6kiJHog -->
# CSE 11 SS1-2022 PA3 - 2D Arrays and ArrayLists
**Due date: Tuesday, July 19 @ 11:59PM PST**

**No slip day or late submission for approved and legitimate cases.**

## Provided Files
None

## File to Submit
- Minecraft.java

## Background
Minecraft is a popular video game where players explore their 3D block-made world in search of materials. Throughout the player's adventure, they may encounter various mobs, including cows, pigs, zombies, and creepers (here, each mob is an individual entity). Players are encouraged to create their own home base out of whatever blocks they choose.

It is not necessary to have played Minecraft to understand or complete this assignment, but it is a fun game.

![minecraft-geisel](https://i.imgur.com/4dDILn9.png)

## Some General Notes
- Most of these notes are necessary for autograding purposes. If any of these does not make sense, you probably aren't doing anything that it applies to. However, you should make sure that when you do learn about it later on in this quarter that you follow these notes. We cannot be lenient regarding these things because everything is autograded to ensure fairness. 
- Make sure to read the autograder output after you submit to Gradescope (wait until the autograder is finished running). 
- Match the specifications that we provide _exactly_, otherwise we cannot ensure that the autograder will function correctly. This includes file names, class names, method signatures, extending, throwing, etc. 
- "Constants" should be defined as `private static final` variables. 
- Do not use _any_ static variables (other than for constants) or instance variables that are not specified in this writeup. We cannot ensure that these do not get clobbered during grading. Any extra variables used should be local only. 
- Unless otherwise specified, do not add any extra `import`s or use any packages not from `java.lang` other than those implied or explicitly named by this writeup. 
- Do not specify a package for your files. This will cause them to fail to compile with the autograder. 
- Do not add any extra classes to your files and do not write code in files that are not specified. 
- Do not call helper methods except from the class where they are implemented, as we will be using our own version of classes during grading (which will only have the instance variables and methods specified in this writeup). You shouldn't be able to call them anyway if you have declared them as `private`. 
- If a behavior (say, on some specific input) is not specified, you may handle that case however you want. However, if you implement a specific behavior for some special case of a required method, do not rely on that specific behavior when using that method as a helper method (only assume that the method works as specified in the writeup). 

<div style="page-break-after: always"></div>

## Part 1: Rotating Minecraft Floor Plans
Because of quarantine, you and your friends virtually spend time together by playing Minecraft with each other. You and your friends decide to create your main base in a lovely, spacious beach biome and plan to build your home on the ocean cliff. Your friend creates a rectangular floor plan out of various Minecraft blocks. However, the living room faces south, but you were hoping to be able to see the sunset from the living room. If the floor plan were rotated 90 degrees clockwise, the living room would face west where the sun sets. Figure out what the floor plan would look like if it were rotated 90 degrees clockwise so you can propose this change to your friend.

### **TODO: Method to Implement for Rotating**
```java
public class Minecraft {
    ...
    public static int[][] rotateFloorPlan(int[][] originalFloorPlan); 
    ...
}
```
Provided an `n x m` two-dimensional integer array representing the original floor plan, write a method that rotates the original floor plan clockwise by 90 degrees and returns the new, `m x n` rotated floor plan. 

![](https://i.imgur.com/TiSyDUg.png)

#### `public static int[][] rotateFloorPlan(int[][] originalFloorPlan)`
- Return the clockwise-rotated floor plan. 
- If `originalFloorPlan` is `null`, return `null` as the "rotated" floor plan. 
- You can assume that `originalFloorPlan`, if it is not `null`, will be a rectangular and non-ragged `n x m` array (with `n>0` and `m>0`). 
- You can also assume that each index of a non-`null` `originalFloorPlan` will contain an int array (i.e., `originalFloorPlan[i]!=null` will be true for valid index `i` if `originalFloorPlan` not `null`). 


### Examples

![](https://i.imgur.com/TiSyDUg.png)
**Input**
```java
originalFloorPlan = {
    {1,1,1,2,2},
    {1,1,1,2,2},
    {5,5,3,2,2},
    {5,5,3,3,3}
}
```

**Output**
```java
{
    {5,5,1,1},
    {5,5,1,1},
    {3,3,1,1},
    {3,2,2,2},
    {3,2,2,2}
}
```


---
![](https://i.imgur.com/QSJBOu5.png)

**Input**

```java
originalFloorPlan = {
    {1,1,2},
    {1,1,1},
    {2,2,2}
}
```


**Output**
```java
{
    {2,1,1},
    {2,1,1},
    {2,1,2}
}
```


---
![](https://i.imgur.com/jYRXwdh.png)

**Input**
```java
originalFloorPlan = {
    {4,1},
    {4,1},
    {4,1},
    {4,8},
    {7,7}
}
```

**Output**
```java
{
    {7, 4, 4, 4, 4},
    {7, 8, 1, 1, 1}
}
```

<div style="page-break-after: always"></div>

## Part 2: Minecraft Party
While exploring for diamonds in Minecraft, you come across a rather eventful village. There you find a bunch of mobs partying and breaking social distancing rules. Suddenly, a mob announces that they are currently infected with the virus, causing widespread panic. You quickly become the hero of the village, volunteering to determine which mobs should get tested.


### **TODO: Method to Implement for Contact Tracing**
```java
public class Minecraft {
    ...
    public static ArrayList<String> getMobsToTest(String[][] groups, String infected); 
    ...
}
```
Given the name of the infected mob and a 2D array of `String`s, with each inner array representing a different group of mobs that was formed throughout the party, return an `ArrayList` of `String`s of all the mobs that should be tested (the `String`s can be in any order in the list). A mob should be tested if they were in direct contact with the infected mob (they will only have been in direct contact if they were ever in the same group). The returned list should not contain any duplicates and should not contain the original infected mob.

**NOTE: You are NOT allowed to use any data structure other than (2D) arrays and ArrayLists in this method. Using any other data structures may result in a 0, even if it passes the autograder.**


#### `public static ArrayList<String> getMobsToTest(String[][] groups, String infected)`
- Return an `ArrayList` containing all, and only, the names of the mobs that should be tested. 
- If either `groups` or `infected` is `null`, return `null` as you do not have the information needed to solve the problem. So, if both arguments are non-`null`, assume that you have all the information. 
- Mobs with the same `String` name are treated as the same mob (e.g., treat multiple occurrences of "Villager" as the same entity). This means that your returned list should not have any duplicates, but duplicates may appear within some `groups[i]` array. Also, each name is case-sensitive ("Villager" will be a different entity from "villager"). 
- Elements in `groups` might be `null`. Skip any `null`s. Note that we do not have the assumption that `groups[i]` or `groups[i][j]` are non-`null`. 


### Examples
```java
groups = {
  {"Cow", "Squid", "Horse"}, 
  {"Sheep", "Cow", "Horse", ""},
  {"Sheep", "Bat"}
}

infected = "Cow"

expected output: any permutation of ["Squid", "Horse", "Sheep", ""]
// Note that the output should be an ArrayList
```
In this example, we see that Cow is our infected mob. We also see that in the first two arrays, Cow interacted with Squid, Horse, and Sheep. We do not include Bat because Bat did not directly interact with Cow. We also only include Horse once since we do not want to include duplicates in our outputted ArrayList.

```java
groups = {
  {"Zombie", "Cow", "Creeper", "Guardian", null, "Slime"},
  {"Sheep", "Iron Golem", "Cow"},
  {"Sheep"},
  {"Cow", "Pufferfish", "Squid", "Sheep"}
}

infected = "Sheep"

expected output: any permutation of ["Cow", "Pufferfish", "Squid", "Iron Golem"]
// Note that the output should be an ArrayList
```
The same logic applies in this case. Sheep interacted with Iron Golem and Cow on one occasion and Cow, Pufferfish, and Squid on another. Thus, our outputted ArrayList should have Cow, Pufferfish, Squid, and Iron Golem.


<div style="page-break-after: always"></div>

## Style
Coding style is an important part of ensuring readability and maintainability of your code. Namely, there are a few things you must have in each file/class/method:
1. File headers
2. Class headers
3. Method headers
4. Inline comments
5. Proper indentation (do not intermingle spaces and tabs for indentation)
6. Descriptive variable names
7. No magic numbers (define any literal values other than the integral/numeric -1, 0, 1 as `private static final` values)
8. Reasonably short methods (if you have implemented each method according to specification in this write-up, you’re fine)
9. Lines shorter than 80 characters (note, tabs will be counted as 4 characters toward this limit. It is a good idea to set your tab width/size to be 4. A good way to check is using the command `grep -n '.\{81\}' *.java` in the directory with your files, but note that this won't necessarily take tabulation into account appropriately. Also note that trailing whitespaces contribute to this total.)
10. Javadoc conventions (@param, @return tags, /** header comments */, etc.)

A full style guide can be found [here](https://docs.google.com/document/d/1xqhafV9rKQXRO1G2hq9S_O5JqK-1xQw2Fpf9fPJO-sI). If you need any clarifications, feel free to ask on Edstem. 

## Submission
### Turning in your code
Submit the following file to Gradescope by **Tuesday, July 19 @ 11:59PM PST**
- Minecraft.java

When submitting, please wait until the autograder finishes running and read the output. **Your code must compile in the autograder in order to receive proper partial credit.**
