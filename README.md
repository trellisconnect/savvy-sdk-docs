# Savvy Widget

Savvy allows users to quickly and easily find savings on their existing insurance.

Your website or mobile app can easily embed the "Savvy Widget" so that users can find these savings without ever navigating off your property.

## Basic Usage

Implementing Savvy Widget is easy. Just copy-and-paste a few lines of code:

```html
<script src="https://cdn.savvy.insure/sdk/v1.0/savvy.js"></script>
<button id="openSavvyBtn">Check My Policy for Savings</button>
<script>
  (function () {
    var handler = Savvy.configure({
      urlTrackingParams: 'REPLACE-THIS-WITH-STRING-FROM-SAVVY',
    });
    document.getElementById('openSavvyBtn').onclick = handler.open;
  })();
</script>
```

## Advanced Usage

### Demo Insurance Carrier

To access the demo insurance carrier for testing purposes, append `?t=1` to the URL of the page hosting the Savvy Widget. [Click here to see a list of valid demo account logins](https://docs.google.com/spreadsheets/d/1a0NPlQ87W6mhACQvPPOX97cN4vHLYyy-TNNBnEz6stg/edit#gid=0).

```
https://mywebsite.com/page?t=1

// or if you have other parameters

https://mywebsite.com/page?utm_source=my-source&t=1
```

### Anchor element call-to-action (CTA)

You can use an `<a>` element instead of a `<button>`:

```html
<script src="https://cdn.savvy.insure/sdk/v1.0/savvy.js"></script>
<a href="#" id="openSavvyBtn">Check My Policy for Savings</a>
<script>
  (function () {
    var handler = Savvy.configure({
      urlTrackingParams: 'REPLACE-THIS-WITH-STRING-FROM-SAVVY',
    });
    function handleClick(event) {
      event.preventDefault();
      handler.open();
    }
    document.getElementById('openSavvyBtn').onclick = handleClick;
  })();
</script>
```

### Callbacks

Savvy Widget supports a number of Javascript callbacks that you can use for analytic purposes and to personalize the user experience around the progress made in the Savvy Widget.

```html
<script src="https://cdn.savvy.insure/sdk/v1.0/savvy.js"></script>
<button id="openSavvyBtn">Check My Policy for Savings</button>
<script>
  (function () {
    var handler = Savvy.configure({
      // REQURIED: Use the tracking/attribution params provided by your contact at Savvy.
      // See https://docs.google.com/document/d/1GF1yxu8BMfpK30EJ4AJZ3lhVuX_6Ae0Cdi2LPXAiAqY
      // for more information.
      urlTrackingParams: '?utm_source=YOUR_ID&utm_medium=incentive',

      // OPTIONAL: Your Trellis Client ID. Required if you intend to collect end-user PII.
      trellisClientId: API_CLIENT_ID,
  
      // OPTIONAL: Skip select issuer screen and head straight to the consent screen for an issuer of your choosing.
      // - ISSUERSLUG - Eg: geico, statefarm, etc
      preselectedIssuerSlug: ISSUERSLUG,

      // OPTIONAL: Set the experience to 'connect' if you want to prevent Savvy SDK from displaying
      // results (e.g. if you intend to use Savvy API to render the results natively).
      // Otherwise, leave undefined.
      experience: undefined,

      // OPTIONAL: Set true to skip qualification questions (e.g. "Do you remember your login?") prior to the credentials page.
      skipQualificationQuestions: false,

      // OPTIONAL: If the Savvy Widget is going to be embedded in a native web view, set isWebView: true
      isWebView: false,

      // OPTIONAL: If you would like to enable the Intro screen for an introduction into the Savvy widget set showIntroScreen: true
      showIntroScreen: false,

      // OPTIONAL: onConnect(connectionId, metadata)
      // Called when the user has authenticated access to their insurance account
      // and granted permission to Savvy to access its data.
      // - connectionId - Set to null if trellisClientId not provided.
      //                  Used for accessing user PII from Trellis API.
      onConnect: handleConnect,

      // OPTIONAL: onClose(error, metadata)
      // Called when the user closes the modal dialog.
      // - metadata
      //   - metadata.accountReferenceId - Account reference ID to use for searching Savvy.
      //                                   Currently set equal to Trellis Connection ID when
      //                                   Trellis Client ID is provided.
      //                                   May not be present if our servers could not be reached.
      onClose: handleClose,

      // OPTIONAL: onEvent(eventName, metadata)
      // Called when certain events happen. Supported event names:
      // - OPEN
      //     - The user has opened the widget.
      // - SELECT_ISSUER
      //     - The user has selected their insurance company.
      // - AUTH_COMPLETE
      //     - The user has finished login/authentication for an account.
      // - PROVIDE_CONSENT
      //     - The user has consented to Savvy's searching for offers.
      // - APPLICATION_COMPLETE
      //     - Enough data has been received that Savvy can get personalized offers.
      // - LOAD_OFFERS
      //     - The user has finished waiting for offers.
      // - CLICK_OFFER
      //     - The user clicked on a specific offer.
      // - TRANSITION_VIEW
      //     - When the Widget transitions between views.
      // - CLOSE
      //     - The flow has been exited. Also calls `onClose` callback.
      // - ERROR
      //     - If an error happens during the flow.
      onEvent: handleSavvyEvent,
    });
    document.getElementById('openSavvyBtn').onclick = handler.open;
  })();
</script>
```

### destroy() function

The destroy function allows you to destroy the Savvy handler instance, properly removing any DOM artifacts that were created by it. This function will fail if called when Savvy Widget is open.

```html
<script>
  // Create the Savvy handler
  var handler = Savvy.configure({
    urlTrackingParams: 'REPLACE-THIS-WITH-STRING-FROM-SAVVY',
  });

  // Destroy handler
  handler.destroy();
</script>
```

### Headless Action - Get Account Reference ID

After configuring the Savvy Widget, you can obtain an Account Reference ID without requiring the user to interact with the Savvy Widget by using this headless action.

_IMPORTANT:_ Avoid calling this headless action after opening the Savvy Widget! You may get the wrong Account Reference ID!

```html
<script>
  var handler = Savvy.configure({
    // ... existing configuration including `urlTrackingParams`

    // See the Callbacks section above for more details about onClose.
    onClose: handleOnClose,
  });

  // This can be called when it makes the most sense in the user's journey.
  // It triggers the onClose callback with the Account Reference ID for the user.
  try {
    handler.headless('GET_ACCOUNT_REFERENCE');
  } catch (error) {
    // Headless actions Errors
    // - Unsupported action
    // - Savvy Widget isn't configured/ready
    // - Savvy Widget is currently open
  }
</script>
```

## CHANGELOG

- 2020-12-16
  - Update basic usage demos
- 2020-04-28
  - Update "onClose" handler to pass metadata that includes accountRefId.
- 2020-02-13 – Initial draft
