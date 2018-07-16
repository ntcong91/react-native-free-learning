## Using

# Full docs - [click here](https://facebook.github.io/react-native/docs/dimensions)

* get screen width, height

    ```
    import { Dimensions } from "react-native"

    ...
    const { width, height } = Dimensions.get('window');

    ```

* Using for inline style

```
const { width, height } = Dimensions.get('window');

export default StyleSheet.create({
    fullScreenContainer: {
        width: width,
        height: height
    }
})
```

* Updating in render method -  recommend using/overriding inline styles rather than setting a value in a StyleSheet (If you want to support multiple screen orientations).

    ```
    import React, { Component } from "react";
    import { Dimensions, View } from "react-native";

    export default class MyComponent
    ...
        render() {
            // We recomends 
            const currentDimension = Dimensions.get('window');
            const screenWidth = currentDimension.width;
            const screenHeight = currentDimension.height;

            return (
                <View style={[styles.definedStyle, { width: screenWidth }]}>
                    <Text>Calculate view </Text>
                </View>
            );

        }
    }

    const styles = StyleSheet.create({
        definedStyle: {
            width: width,
            height: height
        }
    })

    ```

