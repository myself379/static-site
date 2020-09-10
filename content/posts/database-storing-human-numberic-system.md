---
title: "Database Storing Human Numberic System"
date: 2020-08-25T22:36:06+08:00
draft: true
---

MySQL supports various data types for storing numbers. Here are the list of supp
orted types


- Double
- Double Precision
- Float
- Numeric
- Decimal

It is advisable to avoid Double and Float due to the nature interpretation. Unli
ke we, human view numbers in base-10, e.g.: 1, 2, 3, ..., 100, 1000

Computers generally works in binary form, in other words, base-2. i.e.: 0, 1, 01
, 11, 10, 11

In order to store Float and Double system, programs will first mapped the binary
 form into its equivalent in base-10, such example are 01 = 1, 10 = 2, 11 = 3. T
his would be different if it uses different kind of mapping system, it can be bi
nary code, or hexadecimal, or unsigned binary numbers.

With that being said, let say you store 59.95 as Float in database, what actuall
y happens behind-the-scenes, is MySQL will first lookup which is the closest rep
resentation of "59.95" in base-2, then it'll store that value instead. The close
st base-2 of "59.95" is "59.9500000000001694".

Thought, you might said, "well, that's not a big issue, just round it off in Application level". Well its true to a certain extend, that you rely fully on your
Application to work 100% without bugs or forgotten that how MySQL stores Float.
We human are forgetful, it only takes a single mistake to ruin everything down t
he path.

Another thought that, "it wouldn't hurt a fly! ". Well, try said that to a bank
system that uses compound interest. Or any accounting system!

```bash
100^(59.95)

vs

100^(59.9500000000001694)

```

As you can see, even the smallest rounding error, would bring disaster in the calculation

Lucky for us, MySQL also provides human friendly number system! Decimal and Numeric data types. Simply declare it and MySQL will store the value in column exact
ly as it is. e.g.: DECIMAL(10, 3) would mean 1234567.892 can be store but cannot
 store 12345679.892 (note the number of digits before the dot)

 To an extend, the database need to know the nature of the data that it is going
 to handle. Using the wrong dataset would gives you different results
