---
layout: post
title: C Basic about environment and main function
---

{{ page.title }}
================

<p class="meta">22 March 2016 - Beijing</p>

# C语言main函数参数定义可以是多种
int main(void)
int main(int argc ,char *argv[])
int main(int argc, char *argv[], char *envp[])
前面两个比较常见，第三个定义中第三个参数是指环境变量
The 3rd argument is valid in Microsoft C and GNU GCC:
The main parameter envp is not specified by POSIX but is widely supported.

An alternative method of accessing the environment list is to declare a third argument to the main() function:

int main(int argc, char *argv[], char *envp[])
This argument can then be treated in the same way as environ, 
with the difference that its scope is local to main(). 
Although this feature is widely implemented on UNIX systems, 
its use should be avoided since, in addition to the scope limitation, 
it is not specified in SUSv3.

#直接使用environ这个指针
#include <stdio.h>
extern char ** environ;
int main(int argc, char **argv)
{
    int i = 1;
    char *s = *environ;

    for (; s; i++) {
        printf("%s\n", s);
        s = *(environ+i);
    }

    return 0;
}

#参数传入
#include <stdio.h>
int main(int argc, char **argv, char** env) {
    while (*env)
        printf("%s\n", *env++);
    return 0;
}

[Discuss this post on StackOverflow](http://stackoverflow.com)
