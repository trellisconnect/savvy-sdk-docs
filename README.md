# Savvy Widget

Savvy allows your users to quickly and easily find savings on their existing insurance.

Savvy makes the entire user experience available via the easily-embedded "Savvy Widget" so that users can find these savings without even leaving your website or app.

## Basic Usage

```
<script src="https://cdn.savvy.insure/sdk/v1.0/savvy.js"></script>
<a href='#' id='openSavvyBtn'>Check My Policy for Savings</a>
<script>
(function() {
        var handler = Savvy.configure({affiliate_id: 'YOUR_API_CLIENT_ID'});
        document.getElementById('openSavvyBtn').onclick = handler.open;
})();
</script>
```

## Advanced Usage

Savvy Widget supports a number of Javascript callbacks that you can use for analytic purposes and to personalize the user experience around the progress made in the Savvy Widget.

```
<script src="https://cdn.savvy.insure/sdk/v1.0/savvy.js"></script>
<a href='#' id='openSavvyBtn'>Check My Policy for Savings</a>
<script>
(function() {
        var handler = Savvy.configure({
          // Your Savvy affiliate ID
          affiliate_id: '<API_CLIENT_ID>',

          // onAccountLink(accountId, metadata)
          // Called when Savvy has completed retrieving policy information from the user.
          // The function is passed in an accountId and a metadata object.
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
          // - ISSUER_SELECTED
          //     - The user has selected an issuer to login as.
          // - ACCOUNT_LINK
          //     - The user has successfully proceeded past account authentication.
          // - CONSENT_PROVIDED
          //     - The user has provided consent to Savvy's terms and conditions.
          // - OFFERS_LOADED
          //     - The quote request has been finished.
          // - OFFER_CLICKED
          //     - A specific quote has been clicked.
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

## CHANGELOG

* 2020-02-13 – Initial draft
