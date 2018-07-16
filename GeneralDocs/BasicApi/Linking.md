## How to use Linking in react native 
[React Native Docs - click here](https://facebook.github.io/react-native/docs/linking.html)

Read more about Linking Url

* Check URL is valid and open it

    OpenURL function

    ```
    function launchURL(url) {
        Linking.canOpenURL(url)
        .then(supported => {
            if (!supported) {
                console.log(`Can't handle url: ${url}`);
            } else {
                Linking.openURL(url).catch(err => {
                    if (url.includes("telprompt")) {
                        // telprompt was cancelled and Linking openURL method sees this as an error
                        // it is not a true error so ignore it to prevent apps crashing
                        // see https://github.com/anarchicknight/react-native-communications/issues/39
                    } else {
                    console.log("openURL error", err);
                    }
                });
            }
        })
        .catch(err => console.warn("An unexpected error happened", err));
    };
    
    ```

* Map url
    1. Google Map
        > https://developers.google.com/maps/documentation/urls/guide
    2. Apple Map
        > https://developer.apple.com/library/archive/featuredarticles/iPhoneURLScheme_Reference/MapLinks/MapLinks.html#//apple_ref/doc/uid/TP40007899-CH5-SW1

* Send SMS
    1. Open by url (phoneNumber - String, body - String)
        ```
            // Validate phone number function
            function isCorrectType(expected, actual) {
                return Object.prototype.toString.call(actual).slice(8, -1) === expected;
            };

            sendSMS(phoneNumber, body = null) {
                if (arguments.length > 2) {
                    console.log("you supplied too many arguments. You can either supply 0 or 1 or 2");
                    return;
                }

                let url = "sms:";

                if (body && phoneNumber) {
                    url += phoneNumber;

                    if (isCorrectType("String", body)) {
                        url += `?body=${encodeURIComponent(body)}`;
                    } else {
                        console.log(
                        `the body should be provided as a string. It was provided as ${Object.prototype.toString
                            .call(body)
                            .slice(8, -1)},ignoring the value provided`
                        );
                    }
                }

                console.log(url);
                launchURL(url);
            }
        ```

        * Example:
         > sendSMS('+84982707101', "Hello World");



    2. (Android Only) - Can open SMS Application by Intent - We should write a native module  bridge.


* Make a call
    ```
    makeCall = (phoneNumber) => {
        let url = "tel:";

        if (phoneNumber) {
            url += phoneNumber;
            launchURL(url);
        }
        console.log(url);
    };
    ```

    * Example: 
    > makeCall('+84982707101');