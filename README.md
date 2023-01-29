# apm-terminals
Dashboard for APM Terminals

## Installation

## Troubleshoots
### mongodb-setup container continually restarting and mongodb container isn't the PRIMARY replica set.
1. Check if the shell scripts have the correct end-of-line:
    1. Confirm that shell file is not found by looking mongodb-setup logs.
    ```docker logs mongodb-setup | grep "exec /scripts/mongo-rs-no-auth-setup.sh: no such file or directory"```
    The response must be "exec /scripts/mongo-rs-no-auth-setup.sh: no such file or directory" string repeated  several times.

    2.  Confirm that mongodb
