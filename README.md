Mailchimp-Ajax-Segment
----------------------
**Turn your standard Mailchimp embed form into an Ajaxy Segment call.**

userId is a better way to join data at the user level across various tracking/email/etc. services.

Why?

 - userId is stable (e.g., update a user's email address from anywhere
   by calling Segment identify with the same userId.)
 - userId is not PII (e.g., Google Analytics explicitly forbids using PII as a userId)

So, in addition to manually adding a subscriber to your Mailchimp list, this will explicitly assign a userId to each new subscriber and identify the user via Segment.

**Quick steps:**

 - Get your Mailchimp list embed code here: Lists -> {list} -> Signup forms -> Embedded forms
 - Use it to replace the three values in the "action" line with your own. Also change "us6" if yours is different.
 - In the hidden input field with id "bot-field", replace the name with the one from your own embed code.
 - To add or remove form fields, mofiy the form HTML and related code in the "callSegment" function.

Built on @rydama's "mailchimp-ajax-signup" JS to submit form without redirects: https://github.com/rydama/mailchimp-ajax-signup

----------

    <form id="subscribe-form" action="http://<your_account>.us6.list-manage.com/subscribe/post-json?u=<your value>&id=<your value>" method="get">
        <h3>Want more great content delivered to your inbox?</h3>
        <p>(no spam ever, unsubscribe at any time)</p>
        <div>
            <input type="text" placeholder="first name" value="" id="mce-FNAME" name="FNAME">
            <input type="text" placeholder="last name" value="" id="mce-LNAME" name="LNAME">
            <input type="email" placeholder="email *" value="" id="mce-EMAIL" name="EMAIL">
        </div>

        <!-- Do not remove this or risk form bot signups -->
        <div style="position: absolute; left: -5000px;" aria-hidden="true">
            <input type="text" id="bot-field" name="<your name here>" tabindex="-1" value="">
        </div>

        <div class="clear">
            <input type="submit" value="Keep Me Updated" id="mc-embedded-subscribe" class="btn btn-large" name="subscribe">
        </div>
        <!-- The subsription response message will be inserted below -->
        <div id="subscribe-result"></div>
    </form>

----------

[jQuery]
[Your Segment analytics.js]
[mailchimp-ajax-segment.js]