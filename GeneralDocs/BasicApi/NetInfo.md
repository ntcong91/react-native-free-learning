## Full docs - [click here](https://facebook.github.io/react-native/docs/netinfo)

> handle your network status,... on the top component

* Handle network change online/offline
    ```
    class App extends Components {

        componentWillMount() {
            NetInfo.isConnected.addEventListener(
            'connectionChange',
            handleFirstConnectivityChange
            );
        }

        componentWillUnmount() {
            NetInfo.removeEventListener(
                'connectionChange',
                handleFirstConnectivityChange
            );
        }

        handleFirstConnectivityChange = (isConnected) => {
            // Do your task - like show alert

            // You can save the network status on/off in redux
            // and share it to other component like a props
        }
    }
    ```

* Share your network status by redux

    ```
    import React, { Component } from 
    import { connect } from "react-redux";

    class MyComponent extends Component {

        constructor(props) {
            this.state = {
                ///
            }
        }

        componentWillReceiveProps(nextProps) {
            if (this.props.isNetworkAvailble !== nextProps.isNetworkAvailble) {
                /// Do something like set new state or show Popup
            }
        }

        render () {
            const {  }

            return 
        }
    }

    const mapStateToProps = (state) => {
        return {
            isNetworkAvailble: state.network.isNetworkAvailble
        }
    }

    const mapDispatchToProps = (dispatch) => {
        return {
            ///
        }
    }

    export default connect[mapStateToProps, mapDispatchToProps)(MyComponent)
    ```