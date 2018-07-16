## Separate your code

1. import,  export

    * export, import default 1 function
        ```
        // Export Option 1
        export default function add(x, y) {
            return x + y;
        }
        ``` 

        ```
        // Export Option 2
        function add(x, y) {
            return x + y;
        }

        export default add;
        ```


        ```
        // Import
        import addFunction from "./myFunctionFile";
      
        ```
    * export, import 2 or more functions
        ```
        // Export option 1
        export function add(x, y) {
            return x + y;
        }

        export function sub(x, y) {
            return x - y;
        }

        export default {
           // avoid error when you use import as default
           // must have this export
        }
        ```
        ```
        // Export option 2
        function add(x, y) {
            return x + y;
        }

        function sub(x, y) {
            return x - y;
        }

        export default {
            add,
            sub
        }
        ```

        ```
        // Import multi functions OPTION 1
        import { add, sub } from "./myFunctionFile";
        ```
        ```
        // Import multi functions OPTION 2
        import MyFunctions from "./myFunctionFile";

        //use
        const a = MyFunctions.add(2, 5);
        const b = MyFunctions.sub(5, 2);
        ```


2. render

    * Separate your code in a file
    ```
    // ===================================
    // CODE WITHOUT SEPARATING RENDER
    // ====================================
    import React, { Component } from "react";
    import { View, TouchableOpacity, Text, StyleSheet } from "react-native"

    export default class Example extends Component {
        constructor(props) {
            super(props);
            this.state = {
                count: 0
            }
        }

        increaseCount = () => {
            const { count } = this.state;
            this.setState({
                count: count + 1
            })
        }

        decreaseCount = () => {
            const { count } = this.state;
            this.setState({
                count: count - 1
            })
        }

        render() {
            const { count } = this.state;

            // bad => hard to read/change
            return (
                <View>
                    <Text>{count}</Text>
                    <TouchableOpacity 
                        onPress={this.increaseCount}
                        style={styles.btnIncrease}
                    >
                        <Text style={[styles.txtcenter, styles.txtWhite]}>
                            {"Increase"}
                        </Text>
                    </TouchableOpacity>
                    <TouchableOpacity 
                        onPress={this.decreaseCount}
                        style={styles.btnIncrease}
                    >
                        <Text style={[styles.txtcenter, styles.txtWhite]}>
                            {"Decrease"}
                        </Text>
                    </TouchableOpacity>
                </View>
            );
        }
    } 

    const styles = StyleSheet.create({
        btnIncrease: {
            marginVertical: 16,
            paddingHorizontal: 8,
            paddingVertical: 4,
            backgroundColor: "green",
            justifyContent: "center"
        },
        buttonDecrease: {
            marginVertical: 16,
            paddingHorizontal: 8,
            paddingVertical: 4,
            backgroundColor: "red",
            justifyContent: "center"
        },
        txtCenter: {
            textAlign: "center"
        },
        txtWhite: {
            color: "white"
        }
    });
    // ===================================
    // CODE WITHOUT SEPARATING RENDER
    // ====================================
    ```

    Now You can separate your code like this

    ```
    // ===================================
    // CODE WITH SEPARATING RENDER
    // ===================================
    ...

    renderButtonIncrease() {
        return (
            <TouchableOpacity 
                onPress={this.increaseCount}
                style={styles.btnIncrease}
            >
                <Text style={[styles.txtcenter, styles.txtWhite]}>
                    {"Increase"}
                </Text>
            </TouchableOpacity>            
        );
    }

    renderButtonDecrease() {
        return (
            <TouchableOpacity 
                onPress={this.decreaseCount}
                style={styles.btnIncrease}
            >
                <Text style={[styles.txtcenter, styles.txtWhite]}>
                    {"Decrease"}
                </Text>
            </TouchableOpacity>
        )
    }

    renderTextCount() {
        return (
            <Text>{this.state.count}</Text>
        )
    }

    render() {
        // GOOD
        return (
                <View>
                    <Text>{count}</Text>
                    {this.renderButtonIncrease()}
                    {this.renderButtonDecrease()}
                </View>
            );
        }

    ...
    // CODE WITH SEPARATING RENDER
    ```