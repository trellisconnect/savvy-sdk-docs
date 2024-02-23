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
      urlTrackingParams: "REPLACE-THIS-WITH-STRING-FROM-SAVVY",
    });
    document.getElementById("openSavvyBtn").onclick = handler.open;
  })();
</script>
```

## Attribution & Tracking

In order to get credit for your usage, you MUST set `urlTrackingParams` in `Savvy.configure` to the value assigned by your Savvy affiliate success contact (i.e. replace the `'REPLACE-THIS-WITH-STRING-FROM-SAVVY'` placeholder).

Examples:

- Minimum requirement: `'?utm_source=affiliatecode'` (where `affiliatecode` will be provided to you by your Savvy affiliate success contact)
- Minimum requirement for incentivized traffic: `'?utm_source=affiliatecode&utm_medium=incentive'`
- Adding your user_id: `'?utm_source=affiliatecode&external_partner_id=123456'` (where `123456` is your internal user_id)
  - This can be useful so that Savvy can send back per-user performance reporting that you can join Savvy's funnel data to your internal data
  - Savvy expects external_partner_id to represent a unique human end user
- Adding your click_id: `'?utm_source=affiliatecode&txn=98765'` (where `98765` is your internal click_id, transaction_id, etc.)
- Adding campaign information: `'?utm_source=affiliatecode&external_partner_id=123456&utm_campaign=sidebar'` (where "sidebar" is the placement name on your site/app)

Note that you are not limited to just these parameters. See [Savvy URL Tracking Parameters Documentation](https://docs.google.com/document/d/1GF1yxu8BMfpK30EJ4AJZ3lhVuX_6Ae0Cdi2LPXAiAqY) for more information.

## Supported Insurance Carriers

THe following list is the insurance carriers supported by the link technology provided by Trellis Connect:

| Name                   | Slug                 |
| ---------------------- | -------------------- |
| Allstate               | allstate             |
| American Strategic     | americanstrategic    |
| Assurant               | assurant             |
| Auto Owners            | autoowners           |
| Bristol West Insurance | bristolwestinsurance |
| Dairyland              | dairyland            |
| Direct Auto            | directauto           |
| Erie                   | erie                 |
| Esurance               | esurance             |
| Farmers                | farmers              |
| Geico                  | geico                |
| Homesite               | homesite             |
| Kemper                 | kemper               |
| Lemonade               | lemonade             |
| Liberty Mutual         | libertymutual        |
| Mapfre                 | mapfre               |
| Mecrury                | mercury              |
| Metlife                | metlife              |
| Nationwide             | nationwide           |
| Progressive            | progressive          |
| Root                   | root                 |
| Safe Auto              | safeauto             |
| Safeco                 | safeco               |
| State Farm             | statefarm            |
| The Hartford           | thehartford          |
| The General            | thegeneral           |
| Travelers              | travelers            |
| Universal Property     | universalproperty    |
| USAA                   | usaa                 |
| Arrowhead              | arrowhead            |
| Cabrillo               | cabrillo             |
| Homeowners of America  | homeownersofamerica  |
| Narragansett Bay       | narragansettbay      |
| Sagesure Insurance     | sagesureins          |
| Security First         | securityfirst        |
| Stillwater             | stillwater           |

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
      urlTrackingParams: "REPLACE-THIS-WITH-STRING-FROM-SAVVY",
    });
    function handleClick(event) {
      event.preventDefault();
      handler.open();
    }
    document.getElementById("openSavvyBtn").onclick = handleClick;
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
      urlTrackingParams: "?utm_source=YOUR_ID&utm_medium=incentive",

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

      // OPTIONAL: If you would like to hide the uninsured button on the Issuer select screen, set this option to true
      hideUninsuredButton: false,

      // OPTIONAL: If you would like to disable Savvy's default form that collects user information set this option to false
      enableFormExperience: true,

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
      //   - metadata.status: The point the user reached before exiting the Connect flow. One of the following values:
      //     * issuer_selection - User prompted to select or search for their current issuer
      //     * issuer_not_found - User searched for their issuer and Connect found no results
      //     * unsupported_issuer - User selected an insurer that Connect does not support
      //     * trellis_consent - User prompted to accept Trellis' terms and conditions
      //     * unqualified - The user does not have authentication setup with his or her insurer (e.g. has no login)
      //     * requires_credentials - User prompted to provide credentials for the selected issuer
      //     * requires_questions - User prompted to answer security questions
      //     * requires_selections - User prompted to answer multiple choice question(s)
      //     * requires_code - User prompted to provide a one-time passcode
      //     * choose_device - User prompted to select a device on which to receive a one-time passcode
      //     * existing_client - User selected you, the client, as their current issuer
      //     * savvy_consent - User exited while viewing the Savvy Consent Screen
      //     * completed_connect - User exited the modal after fully connecting their account
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
    document.getElementById("openSavvyBtn").onclick = handler.open;
  })();
</script>
```

### destroy() function

The destroy function allows you to destroy the Savvy handler instance, properly removing any DOM artifacts that were created by it. This function will fail if called when Savvy Widget is open.

```html
<script>
  // Create the Savvy handler
  var handler = Savvy.configure({
    urlTrackingParams: "REPLACE-THIS-WITH-STRING-FROM-SAVVY",
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
    handler.headless("GET_ACCOUNT_REFERENCE");
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
