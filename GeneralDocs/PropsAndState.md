## PROPS AND STATE

# There are two data types of a component. You can use them to control your logic flow.

1. state
    * what you can change/modify in your component file. 
    * You can change your state values by
        ```
        this.setState({
            myValue1: value1,
            myValue2: value2
        });
        ```
    * Access your state value by
        ```
        const x = this.state.myValue1;
        ....

        ```
    * Here is an example about state
    ```
    import React,  { Component } from "react";
    import { Text, View, TouchableOpacity, StyleSheet } from "react-native";

    export default class StateExample extends Component {

        // init your state values in constructor
        constructor(props) {
            super(props);
            // here this.state like an object
            this.state = {
                count: 0
            };
        }

        renderButtonIncrease() {
            const { count } = this.state;
            this.setState({
                count: count + 1
            });
        }

        renderButtonIncrease() {
            return (
                <TouchableOpacity
                    style={styles.button}
                    onPress={this.renderButtonIncrease.bind(this)}
                >
                    <Text style={styles.textButton}>{"INCREASE"}</Text>
                </TouchableOpacity>
            );
        }

        render() {
            return (
                <View style={styles.container}>
                    <Text>{this.state.count}</Text>
                    {this.renderButtonIncrease()}
                </View>
            );
        }
    }

    const styles = StyleSheet.create({
        container: {
            flex: 1,  //full
            backgroundColor: "white",
            alignItems: "center, 
            justifyContent: "center"
        },
        button: {
            margin: 16,
            padding: 16,
            backgroundColor: "green",
            justifyContent: "center",
            alignItems: "center"
        },
        textCount: {
            textAlign: "center",
            color: "black"
        },
        textButton: {
            textAlign: "center",
            color: "white"
        }
    });
    ```

2. props
    * For example: You have a parent view and one child view| two children views | more ... Your children views may have the same style, interface but different input or display parameter...
        ```
        <ParentView>
            <ChildImage source={pic1} style={{ width: 193, height: 110 }}/>
            <ChildImage source={pic2} style={{ width: 193, height: 110 }}/>
        </ParentView>
        ```
        * "source" is a prop, "style" too. You can control, customise your child image props (url, style).

        > You can't modify your props in child view. Your child view only receives value of the prop. 
        
        > But you can change it in your parent view by pass value as a state source={this.state.pic}. Your child view can receive a new value when "this.state.pic" changes

    * Props can be:
        * constant: "number", "string", "boolean"
        * function:

            ```
            // Parent View
            import React,  { Component } from "react";
            import { View, Alert } from "react-native";
            import MyCustomButton from "./MyCustomButton";

            export default class StateExample extends Component {

                constructor(props) {
                    super(props);
                }

                onMyCustomButtonPress = (returnValue) => {
                    Alert.alert("Alert", returnValue ? "return true" : "return false");
                }

                render() {
                    return (
                        <View style={{ flex: 1, alignItems: "center", justifyContent: "center" }}>
                            <MyCustomButton
                                onPressProps={(returnValue) => {
                                    this.onMyCustomButtonPress(returnValue);
                                }}
                                boolValueProps={true}
                            />
                        </View>
                    )
                }
            }
            ```
            Here is MyCustomButton.js file
            ```
            import React, { Component } from "react";
            import { TouchableOpacity, Text } from "react-native";

            export default class MyCustomButton extends Component {
                constructor(props) {
                    super(props);
                }

                onPressButton() {
                    const { boolValueProps, onPressProps } = this.props;
                    if (onPressProps) {
                        // return your bool props
                        onPressProps(boolValueProps);
                    }
                }

                render() {
                    return (
                        <TouchableOpacity
                            onPress={this.onPressButton.bind(this)}
                        >
                        </TouchableOpacity>
                    )
                }
            }

            ```

3. Determine using "props" or "state"? WHEN, HOW?

    * When props or state changes => Your component will rerender => it is not good for mobile app performance, battery energy.

    * So you should separate your code into more ChildComponent to restrict ParentComponent rerender. When you set state for your child component. Only your child component renders again =>  ParentComponent doesn't render again.

    * For example
    
    ```
    import ChildComponentOne from "./ChildComponentOne";
    import ChildComponentTwo from "./ChildComponentTwo;

    ...
    render() {
        return (
            <View>
                <ChildComponentOne initCount={2} />
                <ChildComponentTwo initCount={1} />
            </View>
        )
    }
    ...
    ```

    Your ChildComponentOne file like this
    ```
    constructor(props) {
        super(props);
        this.state = {
            count: props.initCount || 0
        };
    }

    increaseCount() {
        this.setState({
            count: this.state.count + 1
        });
    }

    render() {
        return (
            <TouchableOpacity onPress={this.increaseCount.bind(this)}>
                <Text>{this.state.count}</Text>
            </TouchableOpacity>            
        );
    }
    ```
