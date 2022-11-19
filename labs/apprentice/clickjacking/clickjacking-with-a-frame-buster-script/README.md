![clickjacking-with-a-frame-buster-script-cover.png](clickjacking-with-a-frame-buster-script-cover.png)

In this apprentice level lab, we will exploit the change email flow from a website vulnerable to clickjacking via URL parameters, even though there is a frame buster script enabled.

Upon logging in with the given credentials, we notice that after going to the account page, all that is needed to change a user's email is click on the `Update Email` button and that the email can be prefilled via URL parameters. Let's use the writing material's clickjacking template to craft our exploit:

This is how the template looks on our exploit server:

![clickjacking-with-a-frame-buster-script-1.png](clickjacking-with-a-frame-buster-script-1.png)

We can read the message `This page cannot be framed`; this happens because the website enabled a frame buster script, so we cannot render an iframe on this site. A workaround we can try is to add the `sandbox` attribute to our exploit's iframe and set it to `allow-forms`; this will skip the frame buster script and render the iframe. This is how the exploit looks now:

![clickjacking-with-a-frame-buster-script-2.png](clickjacking-with-a-frame-buster-script-2.png)

We need to modify the location of the `CLICK ME` div tag so that it is on top of the `Update Email` button on the vulnerable website. Note that we are setting the iframe's opacity to `0.1` to be able to check the exploit appearance and then modifying the div's top and left CSS properties so that when a logged in user clicks on the `CLICK ME` div on our website, they are actually clicking on the vulnerable website's button to update their email to whatever we previously set in the URL parameters. After setting the top property to 450px and the left property to 50px, it looks like the buttons are aligned to perform a successful attack. At this point, our exploit looks like this:

![clickjacking-with-a-frame-buster-script-3.png](clickjacking-with-a-frame-buster-script-3.png)

All we need to do is set the iframe's opacity to 0.00001 or something similar so that it is almost invisible and send the exploit to our victim.
