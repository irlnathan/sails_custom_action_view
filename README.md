
### This is a project in response to the following stackoverflow question: [HCustom view/action/controller not working in Sails JS](http://stackoverflow.com/questions/19882748/custom-view-action-controller-not-working-in-sails-js?noredirect=1#comment29838727_19882748). 

##Here's the question:

I must be doing something wrong, but I can't see... Basically if I create a controller/model through sails generate controller products and in the file /controllers/ProductsController I add some variables to the index action such as:

```` javascript
index: function(req, res) {

    return res.view({
        myOne: 'World?',
        myvar: 'hello???',
        title: 'Yeap'
    })

},
````

and when I check localhost:1337/products surely enough the variables are printed within the template. Note that I haven't added a custom view and my template file is located at views/products/index.jade (I'm using Jade rather than EJS). However if I create a custom view in /config/routes such as:

```` javascript
'/custom': {

    view: 'custom',
    controller: 'ProductsController',
    action: 'customAction'

}
````

and in my ProductsController I have a very similar action as previously described:

```` javascript
customAction: function(req, res) {

    return res.view({
        myOne: 'Hello?',
        myvar: 'World???',
        title: 'Yeap'
    })

},
````

The variables are not printed in my template. The template is being called alright so is the Controller and Action (so it seems). Can anyone explain what I'm doing wrong?

##Here's my answer:

You have a choice between naming the view the same name as your action `customAction.jade` if you want to access it via:
```` javascript
    index: function(req, res) {

      return res.view({
        myOne: 'World?',
        myvar: 'hello???',
        title: 'Yeap'
      })

	},
````

or you can access the same view/template (e.g. index.jade) by using this syntax:

```` javascript
    customAction: function(req, res) {

      return res.view('products/index', {
        myOne: 'World?',
        myvar: 'hello???',
        title: 'Yeap'
      })

    },
````