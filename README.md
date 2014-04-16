# sendgridjs

Proxy so you can send email via JavaScript through SendGrid.

## Developing on Nitrous.IO

Start working with sendgridjs on
[Nitrous.IO](https://www.nitrous.io/?utm_source=github.com&utm_campaign=sendgridjs&utm_medium=hackonnitrous) in
a matter of seconds:

[![Hack scottmotte/sendgridjs on
Nitrous.IO](https://d3o0mnbgv6k92a.cloudfront.net/assets/hack-l-v1-3cc067e71372f6045e1949af9d96095b.png)](https://www.nitrous.io/hack_button?source=embed&runtime=nodejs&repo=scottmotte%2Fsendgridjs&file_to_open=README.nitrous.md)

## Usage 

```bash
$ git clone https://github.com/scottmotte/sendgridjs.git
$ cd sendgridjs
$ heroku create
$ heroku addons:add sendgrid:starter
$ heroku config:set FROM=fromemail
$ git push heroku master
```

After you are done with that - you can call requests to that url to send an email.

```bash
curl -X POST http://yoursubdomain.herokuapp.com/send \
-d "to=you@youremail.com" \
-d "subject=Test" \
-d "html=<h1>Hello, there</h1>"
```

#### Optional: Using with JavaScript and HTML.

You might have a website with a form and you want to send emails from that form. After setting up this app, you can send emails by adding the following javascript to your html page.

First, make sure you add jQuery to your page. Then do the following on form submit.

```javascript
$("form#id").submit(function() {
  var sendgridjs_url      = "http://yoursubdomain.herokuapp.com/send";
  var sendgridjs_to       = $("input#to").val();
  var sendgridjs_subject  = $("input#subject").val();
  var sendgridjs_html     = "<p>html of email here as a string</p>";

  var email = {
    to      : sendgridjs_to, 
    subject : sendgridjs_subject,
    html    : sendgridjs_html
  }
  $.post(sendgridjs_url, email, function(response) {
    if (response.success) {
      // redirect somewhere or something. up to you. the email was sent successfully.
    } else {
      alert(response.error.message);
    }
  });

  return false;
});
```

## Development

```bash
touch .env
```

Set your settings in .env and then run:

```bash
node app.js
```
