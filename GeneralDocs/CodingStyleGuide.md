# Basic 

## * ES6 AirBnb coding style

[Click Here](https://github.com/airbnb/javascript)

## Other guidelines

1. Capitalize class name.
    class MyClass {

    }

2. Function/Method name, variable / local const
    ```
    \\ Normal function
    function myFunction () {
        let myVar = 5;
        const myName = "Cong Nguyen";
    }
    ```

    ```
    \\ Arrow function
    const myFunction = () => {
        let myVar = 5;
        const myName = "Cong Nguyen";
    }
    ```

    ```
    \\ 
    const MyClass = () => {
        renderHeader = () => {
            return (
                <View>
                    <Text>My Header</Text>
                </View>
            )
        }
    }
    ```
3. Global Constant definition:
    ```
    \\ alway upper case
    const TIMEOUT_IN_SECONDS = 10;
4. Always use ";"("dot comma") at the end of command.
5. Declare Global constant of the FILES (Class,Hook Function) at the first lines of file.
    ```
    CONST MY_TEST_DATA = [
        {
            id: 1,
            text: "This in the intro description.",
            imageId: "INTRO_1"
        },
        {
            id: 2,
            text: "Press START to explore more.",
            imageId: "INTRO_2"
        }
    ];

    ...

    function MyComponent ({  props1, props2 }) => {
        //
        ...
    }
    ...
    ```

    
