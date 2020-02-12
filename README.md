# Savvy JS-SDK

Drop-in React-based modal for clients to easily provide quotes for a user based on their current insurance information.

# API Docs

You can find a full list of Savvy endpoints and schemas here: [Savvy API Docs](https://savvy.insure/docs)

# Usage

1. Include our SDK on your page.
2. Configure a handler using `Savvy.configure()` as shown in the example.
3. Call your handler's `open()` method, and Savvy will present a modal dialog enabling the user to connect his or her insurance account.

```
<script src="https://cdn.savvy.insure/sdk/v1.0/savvy.js"></script>
<a href='#' id='openSavvyBtn'>Open Savvy</a>
<script>
(function() {
        var handler = Savvy.configure({
          // Your Savvy API Client-Id.
          client_id: '<API_CLIENT_ID>',

          // onAccountLink(accountId, metadata)
          // Called when Savvy has completed retrieving policy information from the user.
          // The function is passed in an accountId and a metadata object. The accountId can be
          // used by application server, combined with your Savvy API-SECRET-KEY to pull policy data.
          // The metadata contains summary information about the account connected.
          onAccountLink: handleSavvyAccountLink,

          // onClose()
          // Called when the user closes the modal dialog -- either when they have
          // successfully loaded their policies (potentially after an onSuccess() call) or by
          // clicking the "X" button in the top right of the modal.
          onClose: handleSavvyClose,

          // onEvent(eventName, metadata)
          // Called when certain events happen. Supported event names:
          // - OPEN
          //     - The user has successfully validated their auto insurance login.
          // - EXIT
          //     - The flow has been exited. Also calls `onClose` callback.
          // - ERROR
          //     - If an error happens during the flow.
          // - HANDOFF
          //     - The user has successfully validated their auto insurance login.
          // - ISSUER_CLICKED
          //     - The user has selected an issuer to login as.
          // - QUOTE_CONSENT_PROVIDED
          //     - The user has provided their consent to get quotes.
          // - QUOTES_LOADED
          //     - The quote request has been finished.
          // - QUOTE_CLICKED
          //     - A specific quote has been clicked.
          // - TRANSITION_VIEW
          //     - When the SDK transitions between views.
          onEvent: handleSavvyEvent,
        });
        document.getElementById('openSavvyBtn').onclick = handler.open;
})();
</script>
```

# CHANGELOG

Coming soon.