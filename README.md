# check_robot_tags
Synopsis: Checks to make sure that Tags are equivalent to test case names or task names (see example, below).

For robot framework test suite files,
checks to see if the name of the test case or task corresponds with the tag.
When the two are not equivalent, the script prints the filename,
the test name, and the tag.

Consider the following file named hello_world.robot:
```
*** Settings ***
Documentation     A hello world

Hello World Test Case
    [Tags]  Hello_World_Tests_Case
    Log To Console            Hello Robot World!
```

Run the awk script on the robot file as follows:
```
$ awk -f check_robot_tags.awk hello_world.robot
```
The output of the above run will highlight the differences as shown here:
```
 --- hello_world.robot:
Hello World Test Case
Hello_World_Tests_Case
 
```
This 4-line output pattern will be generated for each name/tag pair that is not equivalent.



Run it over all \*.robot test suite files in the current directory tree as follows:
```
$ find | grep '\.robot$' | xargs awk -f check_robot_tags.awk
