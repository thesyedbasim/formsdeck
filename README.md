# Forms Deck

Easy way to integrate forms with discord.

## How to use Forms Deck

Go to your Discord Server > your Channel settings > Integrations and create a new Webhook.
Copy the Webhook URL.

Now, go to [Forms Deck](https://formsdeck.com) and paste the webhook URL to generate the Forms Deck API link.

**This is the link that is used to make http `POST` requests to Forms Deck API to get responses directly in Discord.**

## How do I add Forms Deck API link to my forms?

There are 2 ways:
1. Using the link in `form` tag in HTML
1. Making http `POST` requests in JavaScript (ex: `fetch` or `axios`)

### Using HTML `form`
You can add the generated API link in the form action. Make sure to add `name` attributes to input and the form method is set to `POST`
```html
<form
        method="POST"
        <!--Your generated API link-->
        action="https://api.formsdeck.com/api/v1/forms/931537507756154922--n4qgtOE1MWV98ZEtR823Ff23K-Z0ZLXlNVcxod2HUqsehMFhJGPDcai4dqEPirngdKe_"
>
        <label for="first-name">Name:</label>
        <input name="first-name" id="first-name" />

        <label for="opinion">Opinion:</label>
        <input name="opinion" id="opinion" />

        <input type="submit" value="Send" />
</form>
```

### Using JavaScript
You can make a `POST` http request to the generated link. Make sure to add `Content-Type: 'application/json'` header.
```js
// Your generated API link
axios.post("https://api.formsdeck.com/api/v1/forms/931537507756154922--n4qgtOE1MWV98ZEtR823Ff23K-Z0ZLXlNVcxod2HUqsehMFhJGPDcai4dqEPirngdKe_",
{
  name: 'Syed Basim',
  opinion: 'I have an opinion on something'
},
{
  headers: {
    'Content-Type': 'application/json'
  }
})
```

## FAQs

#### Why am I getting invalid http method error after submitting the form?
Make sure you have set `form` method to `POST`

#### Why am I getting blank Discord message?
Make sure you have `name` attribute in each input element, as this is the deciding factor for discord messages.
