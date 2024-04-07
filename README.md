

<H1 align="center">![react.svg](images%2Freact.svg) <strong>React Step by step workshop tutorial</strong></H1>


## Get started  🚀

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
from below sample. Lets try to hit this url to see the results.
https://world.openfoodfacts.org/cgi/search.pl?search_terms=burger&page=1&page_size=10&json=1


Replace below lines of code within App.jsx.

```
import { useState } from 'react';
import './App.css';

function App() {
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

  return (
    <>
      <button onClick={searchFoodItems}>fetch food</button>
      <div className="container">
        <div>{JSON.stringify(foodItems)}</div>
      </div>
    </>
  );
}

export default App;

```
You will be able to see a simple page with a single button 
When button is clicked (Note there is a small delay for fetch)
the list will be displayed with food list.

Inspect console to see you can on the list of food items fetched
You can click 
![openPreview.png](images%2FopenPreview.png)

You will see below click on Connect to project
![connectToProject.png](images%2FconnectToProject.png)


Right click and inspect console. Click on button note that 
there will be a delay and the call is asynchronous
so it will take 5-7 seconds to get list back.

![foodItemlist.png](images%2FfoodItemlist.png)

![foodListRawJson.png](images%2FfoodListRawJson.png)
Now lets simplify it to just print the product name 
by adding below code to loop through fooditems using map method
and print H1 heading tag for each food name.

Replace App.jsx code with the below set of code.

```
import { useState } from 'react';
import './App.css';

function App() {
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

  return (
    <>
      <button onClick={searchFoodItems}>fetch food</button>
      <div className="container">
        <div>
          {foodItems?.map((foodItem) => {
            return <h1>{foodItem.product_name}</h1>;
          })}
        </div>
      </div>
    </>
  );
}

export default App;

```

##### Unique list error

When you do so,
you will start to see some warnings in the console as shown below.
With React to uniquely identify elements we need to pass key.
This will hold good if you are trying to print list of items.


![listUniqueWarning.png](images%2FlistUniqueWarning.png)

To fix this error we modify code as shown below
Replace App.jsx with below set of code.

```
import { useState } from 'react';
import './App.css';

function App() {
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

  return (
    <>
      <button onClick={searchFoodItems}>fetch food</button>
      <div className="container">
        <div>
          {foodItems?.map((foodItem, index) => {
            return <h1 key={index}>{foodItem.product_name}</h1>;
          })}
        </div>
      </div>
    </>
  );
}

export default App;
```


![key_index.png](images%2Fkey_index.png)

Now you will see the warning has disappeared.

### Separate FoodCards jsx

Now lets do one thing. We plug out food items card to a separate
jsx component. This will make the code simple and readable and follow React 
principle of making each block as component.

Right click on src folder and click New File.
![NewFile.png](images%2FNewFile.png)

Name the file as `FoodCards.jsx`
⚠️ - Note the casing of file name if it is wrong it might not work as expected

![name_foodcardsjsx.png](images%2Fname_foodcardsjsx.png)

Copy paste below set of code to FoodCards.jsx


```
const FoodCards = (props) => {
  const food = props.foodItem;
  return <h1>{food.product_name}</h1>;
};

export default FoodCards;
```

Replace App.jsx code with below lines of code

```
import { useState } from 'react';
import './App.css';
import FoodCards from './FoodCards';
import SearchIcon from './search.svg';

function App() {
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

  return (
    <>
      <button onClick={searchFoodItems}>fetch food</button>
      <div className="container">
        <div>
          {foodItems?.map((value, index) => {
            return <FoodCards key={index} foodItem={value} />;
          })}
        </div>
      </div>
    </>
  );
}

export default App;
```

Note that we have changed the highlighted lines of code in App.jsx
```
 <div>
      {foodItems?.map((value, index) => {
        return <FoodCards key={index} foodItem={value} />;
      })}
</div>
```

We have also imported the FoodCards
![foodCardimport.png](images%2FfoodCardimport.png)

#### Food data interesting points
* image_front_url
* product_name
* quantity
* expiration_date

Let's create a food card which can display above details in a nice manner

```
const FoodCards = (props) => {
  // instead of writing const foodItem = props.foodItem
  // array destructuring
  const { foodItem } = props;
  return (
    <article className={'food'}>
      <header>
        <p>Quantity - {foodItem.quantity}</p>
      </header>

      <section>
        <img
          src={foodItem.image_front_url ? foodItem.image_front_url : 'N/A'}
          alt={foodItem.product_name}
        />
      </section>

      <footer>
        <span>expires on {foodItem.expiration_date}</span>
        <h3>{foodItem.product_name}</h3>
      </footer>
    </article>
  );
};

export default FoodCards;


```

Note that we are using object destructuring to assign fooditem value
```
const { foodItem } = props;
```

Now you will start seeing food list that gets displayed with image
quantity, expiry date, name. If you inspect console all the html tags
and authoring can be seen.

![foodcards_moreattrs.png](images%2Ffoodcards_moreattrs.png)

## Better user experience with asynchronous call
Now we have refined the code to make it a bit more readable
and also introduced the concept of loading with asynchronous call
Replace App.jsx with below lines of code.


```
import { useState } from 'react';
import './App.css';
import FoodCards from './FoodCards';

function App() {
  const [foodItems, setFoodItems] = useState([]);
  const [loading, setLoading] = useState(false);

  const searchFoodItems = async () => {
    try {
      setFoodItems([]);
      setLoading(true);
      const foodName = 'burger';

      const response = await fetch(
        `https://world.openfoodfacts.org/cgi/search.pl?search_terms=${foodName}&page=1&page_size=10&json=1`
      );
      const data = await response.json();

      setFoodItems(data.products);

      setLoading(false);
    } catch (error) {
      console.error('Error fetching food items:', error);
    }
  };

  let foodList = (
    <div className={'empty'}>
      <h2>No food found</h2>
    </div>
  );

  let loadingCards = <PageisLoading />;

  if (loading) {
    foodList = loadingCards;
  }

  if (foodItems.length > 0 && !loading) {
    foodList = (
      <div className={'container'}>
        {foodItems?.map((value, index) => (
          <FoodCards key={index} foodItem={value} />
        ))}
      </div>
    );
  }

  return (
    <>
      <button onClick={searchFoodItems}>fetch food</button>
      <div className="container">{foodList}</div>
    </>
  );
}

function PageisLoading() {
  return <h1> Page is loading.....</h1>;
}

export default App;

```

### Make Food search more dynamic
All this time we only see results for burger. 
Lets add a search box with search icon

create search.svg file and copy below code
![createFile.png](images%2FcreateFile.png)

![nameFile.png](images%2FnameFile.png)
```
<svg width="42" height="42" viewBox="0 0 42 42" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path d="M29.8594 29.8594L39.4219 39.4219" stroke="#D88769" stroke-width="4.5" stroke-linecap="round" stroke-linejoin="round"/>
    <path d="M17.9062 33.0469C26.2682 33.0469 33.0469 26.2682 33.0469 17.9062C33.0469 9.54431 26.2682 2.76562 17.9062 2.76562C9.54431 2.76562 2.76562 9.54431 2.76562 17.9062C2.76562 26.2682 9.54431 33.0469 17.9062 33.0469Z" stroke="#D88769" stroke-width="4.5" stroke-linecap="round" stroke-linejoin="round"/>
</svg>
```


Replace App.jsx with below lines of code. If you read through the code
you can see we have introduced the search term.
based on what we select in search box you can dynamically see
the food item results.
You also have progress loader which shows up during asynchronous call.

```
import { useState } from 'react';
import './App.css';
import SearchIcon from './search.svg';
import FoodCards from './FoodCards';

const App = () => {
  const [foodItems, setFoodItems] = useState([]);
  const [searchTerm, setSearchTerm] = useState([]);
  const [loading, setLoading] = useState(false);

  const searchFoodItems = async (foodName) => {
    try {
      setFoodItems([]);
      setLoading(true);
      foodName = foodName ? foodName : 'burger';
      const response = await fetch(
        `https://world.openfoodfacts.org/cgi/search.pl?search_terms=${foodName}&page=1&page_size=10&json=1`
      );
      const data = await response.json();
      setFoodItems(data.products);
      console.log('foodItems', foodItems);
      setLoading(false);
    } catch (error) {
      console.error('Error fetching food items:', error);
    }
  };

  let foodList = (
    <div className={'empty'}>
      <h2>No food found</h2>
    </div>
  );

  let loadingCards = <PageisLoading />;

  if (loading) {
    foodList = loadingCards;
  }

  if (foodItems.length > 0 && !loading) {
    foodList = (
      <div className={'container'}>
        {foodItems?.map((value, index) => (
          <FoodCards key={index} foodItem={value} />
        ))}
      </div>
    );
  }

  return (
    <main className="app">
      {/* header */}
      <h1>Food Land</h1>

      {/* search */}
      <search className="search">
        <input
          placeholder={'Search for foods'}
          value={searchTerm}
          onChange={(event) => {
            setSearchTerm(event.target.value);
          }}
        />
        <img
          src={SearchIcon}
          alt="Search"
          onClick={() => {
            searchFoodItems(searchTerm);
          }}
        />
      </search>

      {/* foodList */}
      {foodList}
    </main>
  );
};

function PageisLoading() {
  return <h1> Page is loading.....</h1>;
}

export default App;

```

You are almost there. Now for a final touch to add some colors and beauty
lets do the below last step.



Now for a final touch we need to add an oomph and color to this.
Update App.css with below code.
[App.css](App.css)


![finalSearchWithDosa.png](images%2FfinalSearchWithDosa.png)

🎉 ## Congratulations on completing this workshop