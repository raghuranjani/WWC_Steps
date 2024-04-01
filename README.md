![signin.png](images%2Fsignin.png)

### Navigate to stackblitz.com

![signWithGithub.png](images%2FsignWithGithub.png)
click continue with Github

## Enter the userid and password for github

![enteruserIdAndPwd.png](images%2FenteruserIdAndPwd.png)

### Click new project

![selectNewProject.png](images%2FselectNewProject.png)

### Choose FrontEnd and then React js

![ChooseReact.png](images%2FChooseReact.png)

## It will take a couple of minutes to reboot the app

![renameToMeaningful.png](images%2FrenameToMeaningful.png)

### Voila now you see the react logo with counter try clicking on it

First build is successful. On click of counter button
you will be able to see the counter incrementing.

![firstBuildSuccess.png](images%2FfirstBuildSuccess.png)

#### Lets quickly understand how counter and usestate works here

Open App.jsx file to understand more details
![counterAndUsestate.png](images%2FcounterAndUsestate.png)
We have defined usestate to initialize counter and increment it
The fat arrow function does the job of incrementing value
through the setter function within usestate
![remove.png](images%2Fremove.png)

Remove the highlighted code and replace with below on App.jsx file
![helloWorld.png](images%2FhelloWorld.png)

```
import './App.css';

function App() {
  return (
    <>
      <h1>Hello Welcome to women who code</h1>
    </>
  );
}

export default App;


```

![foodland_components.png](images%2Ffoodland_components.png)

Lets try to understand different terminologies of React and
come back to do the full fledged development.

* Components
* React DOM
* JSX
* Fat arrow function
* Functional programming
* Async - await
* props
* React Hook - usestate
* React Hook - useref

![openPreviewNewTab.png](images%2FopenPreviewNewTab.png)

We will be using open api url to fetch food items
Lets write below simple method to fetch food items

```
const [foodItems, setFoodItems] = useState([]);

const searchFoodItems = async () => {
    try {
      const foodName = 'burger';
      const response = await fetch(
        `https://world.openfoodfacts.org/cgi/search.pl?search_terms=${foodName}&page=1&page_size=10&json=1`
      );
      const data = await response.json();
      setFoodItems(data.products);
      console.log('foodItems', foodItems);
    } catch (error) {
      console.error('Error fetching food items:', error);
    }
  };
```

Inspect console to see you can on the list of food items fetched

#### Unique list item

Lets make the food items code simpler first to fetch all the food items raw

In Angular you might be familiar with pipe JSON directive to pretty print
raw data. In React its a bit different.

```
<div className="container">
          <div>{JSON.stringify(foodItems)}</div>
</div>
```

Now lets simplify it to just print the product name
by adding below code to loop through fooditems using map method
and print H1 heading tag for each food name. When you do so,
you will start to see some warnings in the console as shown below.
With React to uniquely identify elements we need to pass key.
This will hold good if you are trying to print list of items.

```
<div className="container">
          <div>{JSON.stringify(foodItems)}</div>
          <div>
            {foodItems?.map((foodItem) => {
              return <h1>{foodItem.product_name}</h1>;
            })}
          </div>
        </div>
```

![listUniqueWarning.png](images%2FlistUniqueWarning.png)

To fix this error we modify code as shown below

```
<div className="container">
          <div>{JSON.stringify(foodItems)}</div>
          <div>
            {foodItems?.map((foodItem) => {
              return <h1>{foodItem.product_name}</h1>;
            })}
          </div>
        </div>
```

Now you will see the warning has disappeared.

Now lets do one thing. We plug out food items card to a separate
jsx component. This will make the code simple and readable.

```
const FoodCards = ({ foodItem }) => {
  return <h1>{foodItem.product_name}</h1>;
};

export default FoodCards;

```

Change App.jsx code to as below

```

<div className="App">
        <h1>Food Mart</h1>
        <button onClick={searchFoodItems}>fetch food</button>
        <div className="container">
          {/* <div>{JSON.stringify(foodItems)}</div> */}
          <div>
            {foodItems?.map((foodItem, index) => {
              return <FoodCards key={index} foodItem={foodItem} />;
            })}
          </div>
        </div>
</div>

```

#### Food data interesting points
* image_front_url
* product_name
* quantity
* expiration_date

Lets create a food card which can display above details in a nice manner

```
 <div className="food">
      {/* quantity  */}
      <div>
        <p>{foodItem.quantity}</p>
      </div>

      {/* image */}
      <div>
        <img src={foodItem.image_front_url} alt={foodItem.product_name} />
      </div>

      {/* product_name */}
      <div>
        <span>{foodItem.product_name}</span>
        <h3>{foodItem.expiration_date}</h3>
      </div>
      {/* expirydate */}
    </div>
```

Now you will start seeing food list that gets displayed with image
quantity, expiry date, name.

Now we need to add an oomph to this.



