## title: downunderflow | PWN | 521  Solves

**Resolver:** Yxzi

## description:

It's important to see things from different perspectives.

## Solution:

To task is attached binary file and source code of this binary writen in C. The solution is exploited this program using intiger overflow. Program asks the user for number and save this inputed number to 'unsigned shord idx' vatible type. From inputed value subtracted is 1 and this value (num_from_user - 1) can't be greater than or equal to 7.

when I inputed -1 program returns 'Segmentation fault' because minuses numbers are unsupported data types for unsigned varibles (unsigned means that it's value without char, and can stored only natural numbers from 0 to 'some value').

<code>[12:38:31]:[michal@HACKERMAN]$ ./downunderflow
Select user to log in as: -1
Segmentation fault (core dumped)</code>


65535 - maximum value for 'unsigned short int'

https://learn.microsoft.com/en-us/cpp/cpp/data-type-ranges?view=msvc-170

unsigned varibles can operate only on natural numbers from 0 to (2^'bum_of_bits)')-1


I tryed input -65535 and program return me that i loged as user1, because occurred intiger overflow. When I inputted -65535 variable which stores inputted value was zeroed and program returns me element with index 0 from table logins.

<code>[12:38:31]:[michal@HACKERMAN]$ ./downunderflow
Select user to log in as: -65535
Logging in as user1
Mon Sep  4 13:27:44 CEST 2023</code>

so I changing every next value to lower for 1, with each subsequent lower value input to program logged me as next user. with inputed value: -65529 program logged me as admin and return shell :)

<code>[11:51:44]:[michal@HACKERMAN]$ nc 2023.ductf.dev 30025
Select user to log in as: -65529
Logging in as admin
Welcome admin.
cat flag.txt
DUCTF{-65529_==_7_(mod_65536)}</code>
