
* Show error with componentWillReceiveProps (Life cycle function)
    ```
    componentWillReceiveProps(nextProps) {
        if (!this.props.error && nextProps.error) {
            Alert(
                "Error Title", 
                "Error message", 
                [{text: 'Close', onPress: () => {
                    // onclose
                }}]
            );
        }
    }
    ```
    => to avoid duplicating Alert we should check 
* Show error with redux
    ```
    function* sagaFunction() {
        try {
            const response = yield call(myFunc, param);
            if (response && response.error) {
                // yield put(Action.myFuncFailure)
                // Show your error
                Alert(
                    "Error Title", 
                    "Error message", 
                    [{text: 'Close', onPress: () => {
                        // onclose
                    }}]
                );
            }
        } catch(err) {
            Alert(
                "Error Title", 
                "Error message", 
                [{text: 'Close', onPress: () => {
                    // onclose
                }}]
            );
        }
    }
    ```

* Recommend
    > show error alert with redux