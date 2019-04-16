# Associating the ShiftLeft CLI with your ShiftLeft Account

To submit applications to ShiftLeft for analysis and profiling, you must first authenticate with ShiftLeft. This is done using the CLI command `sl auth` or using environment variables.

## Option 1: sl auth

The command `sl auth` is used to to authenticate with ShiftLeft and associate your applications with the organization your are in.

When you run `sl auth` without any arguments you will be prompted to enter the following information:
* ShiftLeft **Organization ID**
* ShiftLeft **Upload Token**

Alternatively using `sl auth --org "$ORG" --token "$TOKEN"` with the same values is possible too and for ease of use this is also what is provided in the ShiftLeft dashboard on the account page.

Once authenticated the CLI creates the local file `$HOME/.shiftleft/config.json` that contains the Organization ID and Upload Token. The CLI requires this file to run the `sl analyze` command. If the `$HOME` environment variable is not set locally, we use the following path: `/etc/shiftleft/config.json`.

## Option 2: Environment Variables

If you are using a CI/CD tool to submit applications to ShiftLeft for analysis, create the following environment variables to automate the authentication process: 

Environment variable for **Organization ID**:
- Name: `SHIFTLEFT_ORG_ID`
- Value: `{org-id-string}`

Environment variable for **Upload Token**:
- Name: `SHIFTLEFT_UPLOAD_TOKEN`
- Value: `{upload-token-string}`

## Obtaining Your Credentials

Once you have logged in to the system, you can obtain these credentials at the **Profiles** page of the ShiftLeft Dashboard.
