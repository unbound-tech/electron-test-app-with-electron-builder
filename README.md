# Electron builder code signing with UKC

This is a minimal Electron application based on the [Quick Start Guide](https://electronjs.org/docs/tutorial/quick-start) within the Electron documentation.

## To Use

To test code signing using a UKC key in Electron builder, use the following instructions:

1. Find the details of the code signing certificate, including email address, location, state and country. You can locate it in UKC using the `ucl list` and `ucl show -u <UID>` commands.
2. Download the sample project: https://github.com/unbound-tech/electron-test-app-with-electron-builder
3. In the project, edit the *package.json* build file. 
    a. Find the win section. 
    b. Add the field *certificateSubjectName* with values that match the installed certificate. For example:
    ```
    "win": { 
        "target": "squirrel", 
        "icon": "build/icon.ico", 
        "certificateSubjectName": "E=<Email address>, CN=<Common name>, OU=<Organizational unit>, O=<Organization Name>, L=<Location>, S=<State>, C=<Country>"
     }
     ```
     
     Refer to the [Electron-builder documentation](electronjs.org/docs) for more information about this field.
4. Run the following command to install all dependencies.

    `npm i`
5. Run the sample signing app.

    `npm run dist`

## Verification

Verify signing by checking the log file dy-ekm-crypto.log on the UKC Entry Point. You should see an entry like:
```
06-08-2020 08:38:03.137 partition=codesigning                          job=88ef478b61b75407 ktype=RSA       key=abc9bb4073ab846d operation=SIGN        rv=0             alg=PKCS1
```
Operations of type *SIGN* designate that signing occurred in the partition specified by *partition*.
