![Trellis Logo](https://cdn.trellisconnect.com/sdk/v1.1/js-sdk/assets/images/header.png)

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
          // Your trellis API Client-Id.
          client_id: '<API_CLIENT_ID>',

          // onSuccess(accountId, metadata)
          // Called when Savvy has completed retrieving policy information from the user.
          // The function is passed in an accountId and a metadata object. The accountId can be
          // used by application server, combined with your Savvy API-SECRET-KEY to pull policy data.
          // The metadata contains summary information about the account connected.
          onSuccess: handleSavvySuccess,

          // onFailure()
          // Called each time the user attempts to authenticate with their insurer and fails.
          onFailure: handleSavvyFailure,

          // onClose()
          // Called when the user closes the modal dialog -- either when they have
          // successfully loaded their policies (potentially after an onSuccess() call) or by
          // clicking the "X" button in the top right of the modal.
          onClose: handleSavvyClose,

          // track(event, params)
          // Similar in meaning to segment.com's analytics.track() call for events occuring
          // inside the Savvy widget.
          // event -- the name of the analytics tracking event
          // params -- a dictionary object of additional event data
          track: handleSavvyAnalyticsTrack,

          // page(page, params)
          // Similar in meaning to segment.com's analytics.page() call for pageviews occuring
          // inside the Savvy widget.  We fire a page() call for every widget screen.
          // page -- the name of the page visited
          // params -- a dictionary object of additional pageview data
          page: handleSavvyAnalyticsPage,
        });
        document.getElementById('openSavvyBtn').onclick = handler.open;
})();
</script>
```

# CHANGELOG

Coming soon.