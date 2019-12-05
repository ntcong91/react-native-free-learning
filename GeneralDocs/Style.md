# Full docs: [React native official docs - Click here](https://facebook.github.io/react-native/docs/style.html)

* inheritance style
    * Now we can define a global style for our app like container, alignCenter,... then import it
    ```
    import { Platform, StyleSheet } from "react-native";
    const appStyles = StyleSheet.create({
        container: {
            flex: 1,
            backgroundColor: "white"
        },
        alignCenter: {
            alignItems: "center",
            justifyContent: "center"
        },
        row: {
            flexDirection: "row",
            alignItems: "center"
        },
        column:{
            flexDirection: "column",
            justifyContent: "center"
        }
    });

    export default appStyles;
    ```

    ```
    import { Platform, StyleSheet } from "react-native";
    import appStyles from "../theme/styles";

    const styles = StyleSheet.create({
        ...appStyles,
        // your style here
    });

    export default styles;
    ```

* Override style with the same name
    ```
    import { Platform, StyleSheet } from "react-native";
    import appStyles from "../theme/styles";

    const styles = StyleSheet.create({
        ...appStyles,
        // your style here
        // Override with the same name container
        container: {
            flex: 1,
            backgroundColor: "blue"
        }
    });

    export default styles;
    ```

* Specify platform
    ```
    import {Platform, StyleSheet} from 'react-native';

    const styles = StyleSheet.create({
    container: {
        flex: 1,
        ...Platform.select({
            ios: {
                marginTop: 0,
            },
            android: {
                marginTop: 20,
            },
        }),
    }
    ```
