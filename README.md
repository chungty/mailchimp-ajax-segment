Mailchimp-Ajax-Segment
----------------------
**Turn your standard Mailchimp embed form into an Ajaxy Segment call.**

When all you have is an email subscription form, you end up using email address as the primary way of referring to users. This seems natural, but it breaks down quickly when you try to tie data together between your email provider and any other services.

userId, meanwhile, is the standard way to join data at the user level across various tracking/email/etc. services. But that usually requires a proper registration system that creates a new userId for every user.

Why is userId better?

 - userId is stable. Email addresses can and will change, but not the userId.
 - userId is not personally identifiable information (PII). Just as an example, Google Analytics explicitly forbids using PII as a userId when pushing data to them.

So, in addition to manually adding a subscriber to your Mailchimp list, this will explicitly assign a userId to each new subscriber and identify the user via Segment. Using Segment's `identify` call with an excplit userId ensures all downstream services use the same userId. Hooray!

Even without a registration system, it's useful to have a consistent userId. Manybe you want to manually aggregate data later. Maybe you want to use something like Zapier to trigger an HTTP API based on another system's actions. With a consistent userId in hand, these things are actually possible.

**Quick steps:**

 - Get your Mailchimp list embed code here: Lists -> {list} -> Signup forms -> Embedded forms
 - Use it to replace the three values in the "action" line with your own. Also change "us6" if yours is different.
 - In the hidden input field with id "bot-field", replace the name with the one from your own embed code.
 - To add or remove form fields, mofiy the form HTML and related code in the "callSegment" function.

Built on @rydama's "mailchimp-ajax-signup" JS to submit form without redirects: https://github.com/rydama/mailchimp-ajax-signup

----------
Here's generally how the form code will look.

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
Elsewhere on the page, you'll need these libraries.

[jQuery]  
[Your Segment analytics.js]  
[mailchimp-ajax-segment.js]
