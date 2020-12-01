# Intro



# Issue
## received emaul from Gmail be deplay
- Your email templates should not have style/css tag
    ```csharp
    @section Head {
        <style type="text/css">
        </style>
    }
    ```
- Must validate google auth from https://postmaster.google.com/
- Your link must have ssl certification
- Your sendgrid must verify sender and domain authentication
- Yust validate SPF, DKIM through Gmail anylyze header