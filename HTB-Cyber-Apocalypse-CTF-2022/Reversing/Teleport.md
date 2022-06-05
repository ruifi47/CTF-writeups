# __Teleport__

### __Challenge Info__

> You've been sent to a strange planet, inhabited by a species with the natural ability to teleport. If you're able to capture one, you may be able to synthesise lightweight teleportation technology. However, they don't want to be caught, and disappear out of your grasp - can you get the drop on them?

<br>

For this challenge we are given an ELF 64-bit LSB pie executable x86-64 stripped file called __teleport__.

When excuting the program with a password as a parameter, we get the following:

![teleport1](./img/Teleport/teleport1.png)

Let's open [Ghidra](https://ghidra-sre.org/ "Ghidra") to analyze the program.

To start our analysis we go to the Symbol Tree section in Ghidra where we can see all the functions.

![teleport2](./img/Teleport/teleport2.png)

Let's analyze *FUN_00100b2a*.

![teleport3](./img/Teleport/teleport3.png)

In this function we can see an if statement on line 11 to check if the character `t` is in the address `0x00303291`.

<br>

When we go through the other functions, we see that they have a similar logic to *FUN_00100b2a* where the if statement checks if a character is in the correct address.

Take for example *FUN_00100f6a*

![teleport4](./img/Teleport/teleport4.png)

and *FUN_00100dd2*

![teleport5](./img/Teleport/teleport5.png)

Looking at these functions we can see similar character checks to the one shown earlier.

When we double click on `DAT_00303281`, Ghidra takes us to the following part in the listing section:

![teleport6](./img/Teleport/teleport6.png)

We can see a range of addresses from `0x00303280` to `0x003032aa` in which each of those addresses refer to a function. 

As we seen earlier each function should contain a character that is being checked if it's in the correct address with an if statement.

If we click on the function (in green) next to each address on that part of the listing section (of the last picture), we get to see the respective function and the corresponding character present in the if statement.

By putting together all the letters in the functions starting in address `0x00303280` and ending on the `0x003032aa` address, we get the flag:

__`HTB{h0pp1ng_thru_th3_sp4c3_t1m3_c0nt1nuum!}`__