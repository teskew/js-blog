# js-blog
## My js Project

  My javaScript project in the Flatiron school was to program a website using the client-side and server-side application. The app has two respoitories, the front end, and the backend. Javascript is the framework for the front-end code, which means it directly interacts with the client. This happens in the browser. The back-end code is a framework based on Ruby. My app is about beer orders from the brewery companies. It can create a new beer order, update, and delete an order. It can also create a new company to have clients order beer from it.

# Creating 

After setting the backend and frontend repositories, we create the models and controls by using command line: 

```js
rails new project-name-here --api --database=postgresql
```
In order to apply this in the application model, we can get the data from the API or build it with the seed data. The database can determine how our active record models can be constructed and what the association is between them.
 ‘Orders belongs _to  companies’ and  ‘Companies has_many Orders’
At the frontend, we create javascript files such as  'index.js,' 'index.html,' and 'style.css.' Of course, our source file of our models is 'order.js' and 'company.js.'
Make sure you add the Middleware gem ‘Rack-cors’
Also add ‘active_model_serializers' to your gem file, and gem 'fast_jsonapi’

# Backend  setup

The beer’s API data and models code are built using the rails in the backend. The data will need to be migrated using rails db:migrate 
In the models code instead of delver specific views or data in our controllers, we would render our variables with file and data interchange format,  json:

```js
def create  
    company = Company.new(company_params)
    if company.save 
        render json: CompanySerializer.new(company)
    else
        render json: {error: "Couldn’t be saved"}
    end
 ```

The models inputs variables that communicate with Rails controllers or render the variables to the frontend by storing the information in the params hash. The params hash is natively built into Ruby on Rails,  and it acts as the medium to pass it, 

```js
def company_params 
     params.require(:company).permit(:name)
end
```

In order to select which attributes we need in the API, we have to be specific in the model’s serializer:

```js
class CompanySerializer 
  include FastJsonapi::ObjectSerializer
  attributes :name
  has_many :orders
 end
```

## Frontend setup


The frontend is responsible to ensure that the client can easily interact with the webpage.
  This can be done through the combination of javascript, Html and css. The html is used to lay out the document  structure and content. CSS for styling, and javaScript is required for advanced interactivity.
In index.html, the script tag connect with our javascript file. 

``js
<script defer src="src/order.js"></script>
```

By making the fetch requests to a Rails backend, we have access to the database containing information 
Data connects via fetch with a method of “POST”.
It uses the promise to deliver more flexible features that will make requests to backend servers from the web browsers.

```js
    getOrders(){
      fetch(this.port + `/orders`)
     .then(response => response.json())
     .then(json => {
         for(const order of json.data) {
         let o = new Order({id: order.id, ...order.attributes}
         o.attachToDom()
 ```

Finally, put together those final pieces of the web development puzzle.
The fetch API, the html, and the CSS all allow the backend and frontend programming languages to run to insure the client can easily interact with the web page.

