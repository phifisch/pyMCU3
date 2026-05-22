# pyMCU3
A python package to interface with pyMCU microcontroller
This microcontroller isn't made anymore as far as I know, but some people still having one of these around might like to use them with python3. 
This MCU was my entry point to the world of hardware control, so it has a nostalgic value to me. So I ported the old package to python3 (currently 3.12).
For more information about the hardware,see http://www.circuitsforfun.com/pymcu.html although sooner or later you might have to search in the internet archive for it.
I haven't thoroughly tested all of the code, so use at your own discretion.

## Quick start
Reproduced from the original author's website listed above (for conservation and ease of access).

Import the pyMCU module:
`import pymcu`

You can get general help about the module using pythons built-in help function:
`help(pymcu)`

You will get a listing of all the class object functions and some documentation about what those functions do.

Now create a new mcuModule class object:
`myBoard = pymcu.mcuModule()`

By default this will scan for a device using a baudrate of 115200.
If you want to scan for available devices on another baudrate (perhaps because it failed to find any pyMCU device), you can make use of

```pymcu.mcuScan(baudrate)
    scan for available pyMCUs.
    returns a dictionary (portname, index)
    primarily used during class initialization to find the first available pyMCU hardware module but this could also be called to get a list of all available hardware modules if you needed to find and initialize a specific one manually.
    Usage:
    baudrate - sets the baudrate to use when scanning for available pyMCU hardware modules. If not specified the default value is 115200.```
, and scan using different baud rates (e.g. 57600, 38400, 19200, 9600).

One thing I liked about this device is that it gave me easy access to PWM, with the ability to set parameters like PWM period, from an interactive shell. These are accessible with
```
pwmDuty(pwmPin, duty)
    Sets the PWM duty cycle for one of the PWM pins.
    Usage:
    pwmPin - specifies a valid PWM pin number [1-5]
    duty - specifies a valid duty cycle value [0-1023]
    Example:
    myBoard.pwmDuty(1, 500)
pwmOff(pwmPin)
    Turns off the hardware PWM function for one of the PWM pins.
    Usage:
    pwmPin - specifies a valid PWM pin number [1-5]
    Example:
    myBoard.pwmOff(1)
pwmOn(pwmPin)
    Turns on the hardware PWM function for one of the PWM pins.
    Usage:
    pwmPin - specifies a valid PWM pin number [1-5]
    Example:
    myBoard.pwmOn(1)
pwmPeriod(preScaler, preScalerOffset)
    Set PWM period
    Usage: pwmPeriod(preScaler, preScalerOffset)
    preScaler: 1, 4, 16, or 64
    preScalerOffset: 0 to 255
    Example: pwmPeriod(1, 255) - Sets preScaler to 1:1, preScalerOffset to 255, PWM Period will be 31.875 micro Seconds, at 50% duty cycle Freq. will be 31.25Khz
    ```

