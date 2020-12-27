# Intro

# Authentication Cheat Sheet

# Mobile risks
##  Improper Platform Usage
- Issues:
  - Misuse of the iOS Touch ID feature, which can result in unauthorized access to the device.
  - Incorrect use of the iOS Keychain for instance by storing session keys in the app local storage.
  - Requesting excessive or wrong platform permissions.
  - Android intents (used to request an action from another app component) that are marked public may reveal sensitive information or permit unauthorized execution.
- Solutions:
  - Restrict apps from communicating with each other, limit access, implement restrictive file permissions, etc.
  - Apply the most restrictive protection class for iOS keychains and adopt best practices to avoid weak implementation of any controls.

## Insecure Data Storage
- Issues:
  - Your mobile device may get lost or stolen and land in the hands of an adversary. Or a piece of malware, acting on the attacker's behalf, may execute on the device, and the attacker might be able to exploit vulnerabilities that leak personal information and gain access to sensitive data.
  - Jailbreaking or rooting a mobile device is sufficient to dodge encryption protection
- Solutions:
  - Assess whether encryption is applied effectively and how the encryption keys are protected.
  - Implement technologies to harden the code against tampering by using obfuscation, protection against buffer overflows and so on.
  - Avoid storing/caching data where feasible.
  - Deploy sound authentication and authorization checks.
## Insecure Communication
- Issues:
  - Insecure communication ranks third in the 2016 OWASP mobile top 10 list. If the data travels unencrypted in cleartext, anyone monitoring the network can capture and read all the information being sent over the wire.

  - Mobile apps commonly exchange data in a client-server model, and it must be transmitted over the device's carrier network and the internet securely. The traffic can be intercepted by proxies, cell towers, or an adversary compromises your WiFi or installs malware on your device. So, what can you do it mitigate vulnerabilities associated with these types of data exchanges?
- Solutions:
  - To avoid data from being stolen as it travels across the network, rely on industry-standard encryption protocols and other general best practices.
  - Deploy SSL/TLS certificates from trusted certificate authorities (CA) to secure all communication channels.
  - Alert users if an invalid SSL/TLS certificate is detected or if the certificate chain verification process fails.

## Insecure Authentication
- Issues:
  - Insecure authentication comes next on the OWASP mobile security vulnerabilities list.
  - Before granting access, mobile apps need to verify the identity of the user. An authentication bypass is often executed by leveraging existing vulnerabilities, such as improper validation of service requests done by the mobile app's backend server.
  - Mobile apps need to verify and maintain user identity, especially during the transmission of confidential data such as financial information.
- Solutions:
  - Weaknesses in the authentication mechanism for mobile apps can be exploited by an attacker. Capitalizing on those weaknesses allows them to bypass password requirements or gain additional permissions leading to data theft and other damages.
  - So, what can you do to stop it?
    - Avoid local authentication methods. Instead, shift this responsibility to the server-side and download application data only after a successful authentication.
    - Refrain from using vulnerable authentication methods (such as device identity), don't store passwords locally, implement multi-factor authentication (MFA), disallow using all four-digit PIN as passwords where feasible, etc.
##  Insufficient Cryptography
- Issues:
  - There are two situations in which a system's cryptography may get compromised to reveal sensitive data:
    - The underlying algorithm used for encryption and decryption might be weak.
    - The cryptographic process itself has implementation flaws.
    - Broken cryptography in mobile apps can be the result of one of several factors. This list of potential causes includes:
      - Bypassing built-in code encryption algorithms.
      - Improperly managing your digital keys.
      - Using custom or deprecated encryption protocols.
- Solutions:
  - Apply strong cryptographic standards as recommended by the [National Institute of Standards and Technology (NIST)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-175Br1.pdf).
  - Avoid storing any sensitive data on the device whenever possible
## Insecure Authorization
- Issues:
  - Not all users are created equal! Some users may be regular users, while others may require additional permissions and privileges, such as admin users.
  - Poor authorization schemes fail to verify not who the user is but whether the user is sanctioned to access the resources they're requesting. Failure to properly enforce identity as well as the permissions given to the users allow hackers to log in as legitimate users and perform privilege escalation attacks.
- Solutions:
  - Ensure that for each request, backend processes verify that incoming identifiers associated with an identity match up and actually belong to the identity.
  - Validate the roles and permissions of an authenticated user using the information on backend systems and not based upon the information supplied by the mobile device.
## Client Code Quality
- Issues:
  - An attacker may pass crafted inputs to function calls made within an app in an attempt to execute them or observe the application's behavior. It may lead to degradation of performance, increased memory usage, etc. Note that the mistakes in code need to be fixed in a localized way since they arise on the mobile client and are different from server-side coding errors. There could be code-level mistakes in mobile apps that may lead to issues such as:
    - Format-string vulnerabilities
    - Buffer overflows
    - Integration with insecure third-party libraries
    - Remote code execution
    - Several apps rely on third-party libraries to build their applications, which often contain bugs and are not well tested. These issues are outside the control of the app developer since they don't own the code. More often than not with code-level bugs, the solution is to rewrite some of the code running on the device. But what else can you do?
- Solutions:
  - Test for buffer overflows, memory leaks, etc. using automated tools, rely on source code reviews, and write code that's easy to understand and well documented.
  - Use consistent coding patterns across the organization.
## Code Tampering
- Issues:
  - App stores sometimes contain tampered versions of mobile apps. An example of a modified app is where a hacker modifies the app's binary to include malicious content, install a backdoor, etc. Attackers can re-sign these counterfeit apps and publish the modified version onto third-party app stores. They can also deliver them to a victim directly via a phishing attack to trick them into downloading the app.
- Solutions:
  - The app must be able to identify any code integrity violation (if additional code has been added or modified) and react suitably to it at runtime. Using something like a code signing certificate could help to let users know about the code alterations.
  - Implement anti-tamper techniques that prevent illicit apps from executing via implementation of checksums, digital signatures, code hardening, and other validation methods.
## Reverse Engineering
- Issues:
  - Attackers may reverse engineer the app and decompile it to perform some code analysis.
  - This is particularly dangerous since the attacker can understand, inspect, and modify the code to include harmful functionality or transmit undesired advertisements. Once they understand how the app operates, they can modify it using tools such as `IDA Pro, Hopper, and other binary inspection tools`. Once they get the app to behave in the desired way, they can recompile and run the app.
- Solutions:
  - In order to prevent reverse engineering, the attacker must be unable to de-obfuscate the code using tools like IDA Pro and Hopper.
## Extraneous Functionality
- Solutions:
  - Sometimes developers may unintentionally leave backdoors or additional functionalities in mobile apps that aren't apparent to end users via the interface. These products may get released into the production environment with a feature not intended to be made available, creating security risks.
  - These weaknesses can typically be exploited by hackers from their systems directly without requiring any participation from regular users. They may examine configuration files, analyze the binary, etc. to discover functionalities in the back-end system that cybercriminals can leverage to perform an attack.
- Issues:
  - Examine the mobile app's configuration settings to detect any hidden switches.
  - Ensure that the logs don't hold exceedingly descriptive statements about backend systems.
## References
  - OSWAP Docs: https://github.com/stephennp/CheatSheetSeries
  - Authentication Cheat Sheet: https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Authentication_Cheat_Sheet.md#authentication-and-error-messages