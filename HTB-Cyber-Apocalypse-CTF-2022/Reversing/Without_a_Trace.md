# __Without a Trace__

### __Challenge Info__

> Draeger's mothership has suddenly vanished, he could be readying an attack! You need to track him down before disaster strikes...

<br>

The file that we get for this challenge is an ELF 64-bit LSB pie executable x86-64 called __without_a_trace__.

When we run the executable we are prompted with the following output:

![without_a_trace1](./img/Without_a_Trace/without_a_trace1.png)

Let's run the executable again but now using [ltrace](https://www.tutorialspoint.com/unix_commands/ltrace.htm "ltrace") to see if we can get some useful information about the password.

![without_a_trace2](./img/Without_a_Trace/without_a_trace2.png)

With ltrace we can see a string comparison the program makes between our input (`password1` in this case) and the string __`IUCzus5b2^l2^tq^c5^t^f1f1|`__ to check if the password is correct.

Let's go to [CyberChef](https://cyberchef.org/ "CyberChef") and try to decrypt the string __`IUCzus5b2^l2^tq^c5^t^f1f1|`__

![without_a_trace3](./img/Without_a_Trace/without_a_trace3.png)

And we get the flag __`HTB{tr4c3_m3_up_b4_u_g0g0}`__