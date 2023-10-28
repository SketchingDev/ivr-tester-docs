---
title: Quick Start
layout: page
nav_order: 3
---

# Quick Start

1. [Create a Twilio account](https://www.twilio.com/), load it with money and rent a phone number
2. Store an [authentication token](https://support.twilio.com/hc/en-us/articles/223136027-Auth-Tokens-and-How-to-Change-Them) in environment variables:
   ```shell
   export TWILIO_ACCOUNT_SID=ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
   export TWILIO_AUTH_TOKEN=your_auth_token
   ```
3. Configure your environment for either [Google](https://github.com/SketchingDev/ivr-tester/tree/main/packages/transcriber-google-speech-to-text) or [Amazon's](https://github.com/SketchingDev/ivr-tester/tree/main/packages/transcriber-amazon-transcribe) transcription service
4. Install and start ngrok
   ```shell
   npm install ngrok -g
   ngrok http 8080
   ```
5. Run the tests
   ```shell
   # Local port that IVR Tester will listen on
   export LOCAL_SERVER_PORT=8080
   # URL that ngrok exposes to the outside world
   export PUBLIC_SERVER_URL=$(curl -s localhost:4040/api/tunnels | jq -r .tunnels[0].public_url)

   node test.js
   ```


```typescript
const config = { transcriber: googleSpeechToText({ languageCode: "en-GB" }) };

new IvrTester(config).run(
  { from: "0123 456 789", to: "0123 123 123" },
  {
    name: "Customer is provided a menu after their account number confirmed",
    steps: [
      {
        whenPrompt: similarTo("Please enter your account number"),
        then: press("184748"),
        silenceAfterPrompt: 3000,
        timeout: 6000,
      },
      {
        whenPrompt: similarTo(
          "press 1 for booking a repair or 2 for changing your address"
        ),
        then: hangUp(),
        silenceAfterPrompt: 3000,
        timeout: 6000,
        },
     ],
  }
);
```

## Commands

| When         | Overview                             |
|--------------|--------------------------------------|
| [contains]   | Prompt contains a piece of text      |
| [matches]    | Prompt matches regular expression    |
| [similarTo]  | Prompt is similar to a piece of text |
| [isAnything] | Prompt can be anything               |

[contains]: https://github.com/SketchingDev/ivr-tester/tree/main/packages/ivr-tester/doc#contains
[matches]: https://github.com/SketchingDev/ivr-tester/tree/main/packages/ivr-tester/doc#matches
[similarTo]:  https://github.com/SketchingDev/ivr-tester/tree/main/packages/ivr-tester/doc#similarto
[isAnything]: https://github.com/SketchingDev/ivr-tester/tree/main/packages/ivr-tester/doc#isanything

| Then        | Overview            |
|-------------|---------------------|
| [press]     | Produces DTMF tones |
| [hangUp]    | Terminates the call |
| [doNothing] | Doesn't do anything |

[press]: https://github.com/SketchingDev/ivr-tester/tree/main/packages/ivr-tester/doc#press
[hangUp]: https://github.com/SketchingDev/ivr-tester/tree/main/packages/ivr-tester/doc#hangup
[doNothing]: https://github.com/SketchingDev/ivr-tester/tree/main/packages/ivr-tester/doc#donothing
