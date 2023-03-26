# Matching

## What happens if you remove the go-command from the Seek call in the main function?

### Hypothesis
Removing the go keyword from the Seek function call would result in the function being executed synchronously, meaning that the program would wait for the Seek function to complete before continuing with the rest of the code.

### Result
It works fine since the chanel is buffered. This means that the thread doesn't have to wait for someone to recieve before it can move on. The for loop can then continue and the next call to `Seek()` will read the value.


## What happens if you switch the declaration wg := new(sync.WaitGroup) to var wg sync.WaitGroup and the parameter wg *sync.WaitGroup to wg sync.WaitGroup?

### Hypothesis
Since the WaitGroup struct contains a mutex field, which is not copyable, passing it by value would result in a compilation error.

### Result
As predicted the program reached a deadlock at the `wg.Wait()`.
    
## What happens if you remove the buffer on the channel match?

### Hypothesis
It will create an unbuffered channel. This means that any send operation on this channel will block until there is a corresponding receive operation that can receive the sent value.

### Result
The hypothesis was proven to be correct!

## What happens if you remove the default-case from the case-statement in the main function?

### Hypothesis
In the absence of a default-case, the select statement will block until one of the cases is ready for communication. If none of the specified cases are ready, the select statement will block indefinitely.

### Result
I must be some sort of genius cause I was correct again!