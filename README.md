stamplay-ebayclassifieds
========================

A mobile Post &amp; Search free local classifieds app like Ebay's one. Built with Ionic Framework

![EbayClassifieds](http://blog.stamplay.com/wp-content/uploads/2014/10/foto_iphone5s_silver_portrait-1024x6821.jpg "EbayClassifieds")

This time we go mobile! Today’s tutorial will show you how to use Stamplay with the amazing Ionic Framework to create a fully fledged native mobile app. We wanted to deliver something that can be reused in many context so we decided to build an Ebay Classifieds clone to let users post, search and sell their items.

We love javascript and front end framework and this time we show you how you can create this app using Ionic and [AngularJS](http://angularjs.org) to implement the client side logic. Here are the user stories for this example:

* as a guest user I can read and search posted items filtering them by Category or City
* as a guest user I can post an item I’d like to sell
* as a guest user I need to confirm to have provided valid email address before posting a new item
* as a guest/logged user I can reach out to the owner of an item I want
* as a logged user I can to track my listings
* as a guest/logged user I can get in touch with the app adminsitrator
* as a guest user I can signup with email and password to be able to fully interact with the content of the website.

To start building your own version of this great tutorial go and create a new project on [Stamplay](https://stamplay.com) , follow this guide to see how to configure the back-end and then use the code on the Github repository to build your native client.

-----------------------
# Anatomy

This Ebay Classifieds clone is built around the following building blocks

* [Users](https://www.stamplay.com/docs#user)
* [Custom Objects](https://www.stamplay.com/docs#customobject)
* Mailchimp
* [Email](https://www.stamplay.com/docs#email)


After creating a new app on Stamplay let’s start by picking the component we need in this app that are. Lets see one-by-one how they are configured:

### User

We chose to not do fancy things on the user signup this time and to go for the classic email+password. So we really only need to add the user component to our app recipe :)

### Custom Object

Let’s define the entities for this app, we will define “Item”, “Category” and “Area” that are defined as follows:

##### Item

* Name: `photo`, Type: `file`, required, the item’s picture
* Name: `price`, Type: `number`, required, the item’s price
* Name: `description`, Type: `string`, required, the author of the question (it will contain one user’s _id)
* Name: `email`, Type: string, `optional`, the item’s owner email address
* Name: `address`, Type: `string`, answers posted for the current question listed as an array of answer’s _id s
* Name: `tags`, Type: `collection` of category, the categories associated to the item listed as an array of categories’ _id
* Name: `name`, Type: `string`, required, the name of the item
* Name: `area`, Type: `relation` to an area, required, the item’s owner area
* Name: `telephone`, Type: `string`, required, the item’s owner phone number
* Name: `user`, Type: `user_relation`, optional, the user who published this item
* Name: `published`, Type: `boolean`, required, the status of the item (public or not)

##### Category

the categories available to classify posted items. These can be created only by the admin:

* Name: `name`, Type: `string`, required, the name of the category

##### Area

the categories available to classify posted items. These can be created only by the admin:

Name: `name`, Type: `string`, unique, required, area’s name

After setting up this Stamplay will instantly expose Restful APIs for our newly resources the following URIs:

`https://APPID.stamplay.com/api/cobject/v0/item`
`https://APPID.stamplay.com/api/cobject/v0/category`
`https://APPID.stamplay.com/api/cobject/v0/area`

##### Email

This component doesn’t need any setup, couldn’t be easier than that ;)


-----------------------


## Creating the server side logic with Tasks

Now let's add the tasks that will define the server side of our app. For our app we want that:

### When a user signs up, send him a welcome email

Trigger : User - Signup

Action: Email - Send

**User signup configuration**

	none

**Email Send configuration**

	to: {{user.email}} 
  from: classifieds@stamplay.com 
  name: "Stamplay Classifieds"
  Subject: "Thanks for ordering with Stamplay FoodMe"
  Body: "Hi {{user.name.firstName}}, <br/> 
        welcome to our Post and Search mobile service
        <br/>
        the easiest way to share what you want to sell search what you want to buy!"
