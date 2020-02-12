![Trellis Logo](https://cdn.trellisconnect.com/sdk/v1.1/js-sdk/assets/images/header.png)

Drop-in React-based modal for clients to easily provide quotes for a user based on their current insurance information.

# API Docs

You can find a full list of Savvy endpoints and schemas here: [Savvy API Docs](https://savvy.insure/docs)

# Usage

1. Include our SDK on your page.
2. Configure a handler using `TrellisConnect.configure()` as shown in the example.
3. Call your handler's `open()` method, and Savvy will present a modal dialog enabling the user to connect his or her insurance account.
4. Have your `onSuccess` method pass the `accountId` to your application server, which can call Trellis API endpoints to retrieve information about that account. (Note: Your application server – not your web and mobile clients - should access the Trellis API because such access requires the use of your Trellis `API_SECRET_KEY`, which should never be publicly disseminated.)

```
<script src="https://cdn.savvy.insure/sdk/v1.1/trellis-connect.js"></script>
<a href='#' id='openSavvyBtn'>Open Savvy</a>
<script>
(function() {
        var handler = TrellisConnect.configure({
          // Your trellis API Client-Id
          client_id: '<API_CLIENT_ID>',

          // This enables the Savvy quoting functionality.
          policyOnly: false,

          // onSuccess(accountId, metadata)
          // Called when TrellisConnect has completed retrieving policy information from the user.
          // The function is passed in an accountId and a metadata object. The accountId can be
          // used by application server, combined with your Trellis API-SECRET-KEY to pull policy data.
          // The metadata contains summary information about the account connected.
          onSuccess: handleTrellisSuccess,

          // onFailure()
          // Called each time the user attempts to authenticate with their insurer and fails.
          onFailure: handleTrellisFailure,

          // onClose()
          // Called when the user closes the modal dialog -- either when they have
          // successfully loaded their policies (potentially after an onSuccess() call) or by
          // clicking the "X" button in the top right of the modal.
          onClose: handleTrellisClose,

          // track(event, params)
          // Similar in meaning to segment.com's analytics.track() call for events occuring
          // inside the Trellis widget.
          // event -- the name of the analytics tracking event
          // params -- a dictionary object of additional event data
          track: handleTrellisAnalyticsTrack,

          // page(page, params)
          // Similar in meaning to segment.com's analytics.page() call for pageviews occuring
          // inside the Trellis widget.  We fire a page() call for every widget screen.
          // page -- the name of the page visited
          // params -- a dictionary object of additional pageview data
          page: handleTrellisAnalyticsPage,
        });
        document.getElementById('openSavvyBtn').onclick = handler.open;
})();
</script>
```

# CHANGELOG

Coming soon.