# Full docs: [Platform Specific Code](https://facebook.github.io/react-native/docs/platform-specific-code.html)

* Separate into two files: "SpecifiedPlatformText.android.js", "SpecifiedPlatformText.ios.js"

  ```
  import SpecifiedPlatformText from "./SpecifiedPlatformText";
  ```

* Separate by if command

  ```
  render() {
      if (Platform.OS === "ios") {
          return (
              <Text>{"This is iOS Platform"}</Text>
          );
      }

      /// android
      return (
          <Text>{"This is Android Platform"}</Text>
      );
  }
  ```

* Separate by "select"
  ```
  export default {
      ...Platform.select({
          android: {
              text: "android"
          },
          ios: {
              text: "ios"
          }
      })
  }
  ```
