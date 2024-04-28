# Shell Basics

#### Assignment and Substitution

```
`a1_=1`
`a2_=2`
`value_a_1=$a1_`
`value_a_=$((a1_+a2_))`
```

#### Variables

**1.Built-in Variables**

```
For example `$HOME` `PWD` ... , for more info , type `env`
```

**2.Positional Parameters**

```
`echo $para 1 $para 2 ... $para n $n $* $@ $#`
```

**3.Predefined Parameters**

```
$?    #exit status of a command, function, or the script itself
$$    #the ID of current process
$!    #the ID of latest process
```

#### Branches

```
if [ condition1 ];then
    command_series1
elif [ condition2 ];then
    command_series2
else
    default_command_series3
fi
```

#### Loops

**range for**

```
for arg in `seq 10`; do
    echo $arg
done
```

**for in C-like syntax**

```
LIMIT=10
for ((a=1; a<=LIMIT; a++)); do
    echo "$a"
done
```

**while**

```
LIMIT=10
a=1
while ((a<=LIMIT)); do
    ((a += 1))
done
```

#### IO redicret

```
command < input-file > output-file    #rewrite
command >> output-file                #appending
```

#### Function

```
# define a function
function fun_name(){
command...
}
## or
fun_name(){ # arg1 arg2 arg3
command...
}
# apply a function
fun_name $arg1 $arg2 $arg3
# dereference
fun_name(){ # arg1
eval "$1=hello"
}
fun_name arg1
## the above code block is equivalent to
arg1=hello
```

#### Debbugging

```
1. take good use of sh(1)
for example:
sh -n script: checks for syntax
sh -v script: echo each command before executing it
sh -x script: echo the result of each command in an abbreviated manner
2. use echo
3. use trap
```

#### Parallel

```
use GNU parallel
```

#### Script with Style

```
1. Comment your code
2. Avoid using magic number
3. Use exit codes in a systematic and meaningful way
4. Use standardized parameter flags for script invocation
```
