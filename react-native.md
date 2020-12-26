# Intro

## Set up
- Download java jdk
- Add environment variables:
  - System variables:
    - JAVA_HOME: `C:\Program Files\Java\jdk-13`
    - PATH:
      - `%JAVA_HOME%\bin`
      - `C:\Users\Dat Ngo\AppData\Local\Android\Sdk\tools`
      - `C:\Users\Dat Ngo\AppData\Local\Android\Sdk\platform-tools`

  - User variables:
    - ANDROID_HOME: `C:\Users\Dat Ngo\AppData\Local\Android\Sdk`
 - Update environment variables 
 - Update Android API version if needed
 - Add local.properties file at Android `app/src` with sdk directory:
    - `sdk.dir=C\:\\Users\\Dat Ngo\\AppData\\Local\\Android\\Sdk`

## Development
- Debugger: `http://localhost:8081/debugger-ui/`

## Troubleshooting
- Execution failed for task `':app:processDebugGoogleServices'. Failed to delete: \google-services\debug`
  - Just delete `build` folder inside `android/app/` and run as an administrator your cmd.