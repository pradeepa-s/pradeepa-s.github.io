# Firmware development

# A button driver

Looking at different ways to implement a simple button driver.

## Polling - All in main loop

```c
int main()
{
    // Initialization code

    while (1)
    {
        if (GPIO_Read(PIN1, PORTA) == SET)
        {
            // Button pressed
            do_something();
        }

        // do other things
    }

    return 0;
}
```

*Pros*

- Simple implementation

*Cons*

- Difficult to unit test
- Cannot re-use code
- Lacks separation of concerns
- Button sampling time is not deterministic


## Polling - Using an abstraction for button

```c
// main.c

int main()
{
    // Initialization code

    while (1)
    {
        if (is_button_pressed())
        {
            do_something();
        }
    }
}

// button.c

int is_button_pressed()
{
    if (GPIO_Read(PIN1, PORTA))
    {
        return 1;
    }
    return 0;
}
```
*Pros*

- Simple implementation
- Better separation of concerns

*Cons*

- Difficult to unit test
- Difficult to re-use code
- Button sampling time depends on the amount of logic inside the super loop
- We can miss button presses.


## Interrupt based 

```c
// interrupt vector
void GPIO_Interrupt()
{
    button_pressed();
}

// main.c

int main()
{
    // Initialization code

    while (1)
    {
        if (is_button_pressed())
        {
            do_something();
        }
    }
}

// button.c

bool button_press_processed = 1;

void button_pressed()
{
    button_press_processed = 0;
}

int is_button_pressed()
{
    if (button_press_processed == 0)
    {
        button_press_processed = 1;
        return 1;
    }
    return 0;
}
```
*Pros*

- Simple implementation
- Better separation of concerns
- Easy to unit test
- Easy to re-use
- We will not miss button presses

*Cons*

- It could take some time to process button press
- More lines of code


# Read temperature sensor

### Marketing requirement

The temperature values can be read using the TemperatureMate software



### System requirement

The TemperatureMate software and TemperatureLogger shall support DataRead command

DataRead command:

Command: DataRead\n
Response: Last 10 temperature values against UTC time.

```
<1632625915>:<2345>
...
...
<1632635915>:<2415>

Time: UNIX epoch time
Temperature: Temperature value * 100
```

### Sub-system specification TemperatureMate

User shall be able to read temperature through ReadTemperature dialog

### Sub-system specification TemperatureLogger

DataRead command shall be responded with last ten temperature values

## Temperature sensor

- [TMP112](https://www.ti.com/product/TMP112)

## Behaviour Driven Development (BDD)

- Implement a test to cover the required behaviour
- We can use test frameworks such as [behave](https://behave.readthedocs.io/en/stable/)
