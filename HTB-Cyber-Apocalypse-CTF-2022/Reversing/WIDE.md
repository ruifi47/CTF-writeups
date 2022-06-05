# __WIDE__

### __Challenge Info__

> We've received reports that Draeger has stashed a huge arsenal in the pocket dimension Flaggle Alpha. You've managed to smuggle a discarded access terminal to the Widely Inflated Dimension Editor from his headquarters, but the entry for the dimension has been encrypted. Can you make it inside and take control?

<br>

For this challenge we are given an ELF 64-bit LSB pie executable x86-64 file called __wide__ and a file called __db.ex__.

When we execute the __wide__ file with __db.ex__ as a parameter we are prompted with the following:

![wide1](./img/WIDE/wide1.png)

Since the challenge info refer to the Flaggle Alpha dimension, let's select its correspondent number (__`6`__).

![wide2](./img/WIDE/wide2.png)

By selecting the dimension number __`6`__ (Flaggle Alpha), the program asks us for the `WIDE decryption key`.

Let's now open the executable file __wide__ in [Ghidra](https://ghidra-sre.org/ "Ghidra") to start reverse engineering the executable and find the `WIDE decryption key`.
After opening up __wide__ in Ghidra we select the *main* function and go to the decompiler section to see if we can spot something interesting.

![wide3](./img/WIDE/wide3.png)

In the *main* function we see some code responsible for displaying some error messages if we don't run the program with the right parameters and also some code responsible for printing the text that we see when the program is being executed. In line 45, we can see that a function called *menu* is called so let's take a look at what that function does.

![wide4](./img/WIDE/wide4.png)

Looking at the function *menu*, we can see that in line 152, a string comparison is being made using [`wcscmp`](https://www.cplusplus.com/reference/cwchar/wcscmp/ "wcscmp") to see if our input matches the string __`sup3rs3cr3tw1d3`__.
So now let's input the string __`sup3rs3cr3tw1d3`__ when the program asks us for the `WIDE decryption key`.

![wide5](./img/WIDE/wide5.png)

And we get the flag __`HTB{str1ngs_4r3nt_4lw4ys_4sc11}`__