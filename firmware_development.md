# Firmware development

# Most common designs

## Super-loop

- Implement all the logic in one giant loop

```c
int main()
{
    // Initialization code

    while (1)
    {
        if (some condition 1)
        {
            do_something_1();
        }
        else if (some condition 2)
        {
            do_something_2();
        }
    }
    return 0;
}
```

- Good for simple firmware projects
- If one action takes more time, that would prevent other actions from executing
- Time critical code can be implemented in interrupt context

```c
void interrupt_handler_gpio()
{
    process_gpio();
}
```

## Real Time Operating System

- This uses a sophisticated schedular to execute tasks
- Tasks can interrupt (pre-empt) other low priority tasks
- Each task has it's own stack space
- Used for more complex Embedded systems

```c
void task1()
{
    while (condition 1 occured)
    {
        do_something_1();
        clear_condition_1();
    }
}

void task2()
{
    while (condition 2 occured)
    {
        do_something_2();
        clear_condition_2();
    }
}

int main()
{
    // Initialize HAL

    create_task(task1, ...);
    create_task(task2, ...);
    start_kernel();

    while(1);
    return 0;
}
```

- Task can talk with each other using message queues
- Task synchronization needs to be handled
- Tasks run based on its priority
- Schedular can use round robin or any other algorithm to switch between tasks


# Good practices

- Don't overload main function
- Always try to separate concerns to different modules (C files, C++ classes, etc.)
- Use dependency injection to de-couple application logic and hardware
- Strive for testable designs


# Behaviour Driven Development (BDD) and Test Driven Development (TDD)

- Run the test before implementing the code

## Implementing an API using behave

- We can use test frameworks such as [behave](https://behave.readthedocs.io/en/stable/)
- Implement a test to cover the required behaviour

### GetInfo command

Command: GetInfo\n
Response: <version>

### Reset command

Command: Reset\n
Response: None, device resets

### GetTemperature command

Command: GetTemp\n
Response: <temperature>

## Implementing a storage manager using TDD

- Initially write to storage index 0
- Every write increments the index by 1
- Erasing would reset the storage index to 0
- When powered on, shall read and find out where to append data

## Take home messages

- Try your best to implement testable designs, if you can't verify your implementation, we never know when it would break
- Always think abour core Software Engineering concepts such as SRP, DIP, DRY, etc.
- Always refactor code and make it more readable
- Readability trumps efficiency in most of the Embedded Systems
