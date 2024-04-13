![reactlogo.png](images%2Freactlogo.png)
<H1 align="center"> <strong>React Step by step workshop tutorial</strong></H1>


## 1. Get started  🚀

![signin.png](images%2Fsignin.png)


### 2. Navigate to stackblitz.com

![signWithGithub.png](images%2FsignWithGithub.png)
click continue with Github

## 3. Enter the userid and password for github

![enteruserIdAndPwd.png](images%2FenteruserIdAndPwd.png)

### 4. Click new project

![selectNewProject.png](images%2FselectNewProject.png)

### 5. Choose FrontEnd and then React js

![ChooseReact.png](images%2FChooseReact.png)

## It will take a couple of minutes to reboot the app

![renameToMeaningful.png](images%2FrenameToMeaningful.png)

### Voila now you see the react logo with counter try clicking on it

First build is successful. On click of counter button
you will be able to see the counter incrementing.

![firstBuildSuccess.png](images%2FfirstBuildSuccess.png)

#### 6.  Lets quickly understand how counter and usestate works here

Open App.jsx file to understand more details
![counterAndUsestate.png](images%2FcounterAndUsestate.png)
We have defined usestate to initialize counter and increment it
The fat arrow function does the job of incrementing value
through the setter function within usestate
![remove.png](images%2Fremove.png)


Replace App.jsx file with below set of code.
![helloWorld.png](images%2FhelloWorld.png)

```jsx
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

#### 7.  Understand how counter works
I want to show you how the counter works. Lets take a simple example
where we dont use "usestate" to increment counter
Replace App.jsx with below set of code
We have some console log to print counter every time we click the button.
```jsx
import './App.css';

function App() {
  let counter = 0;
  const clickHandler = () => {
    console.log('you are clicking me');
    counter = counter + 1;
    console.log('counter', counter);
  };

  return (
    <>
      <h1>Hello Welcome to women who code</h1>
      <button onClick={clickHandler}>click me {counter}</button>
    </>
  );
}

export default App;


```

Now open the preview mode to inspect console.
![openPreview.png](images%2FopenPreview.png)
![connectToProject.png](images%2FconnectToProject.png)

Right click on browser and choose inspect to inspect the console
![inspect_console.png](images%2Finspect_console.png)

Now you start to see simple console logs below.
Now you see the counter getting printed in console but its not rendered
in the DOM.
![console_log_counter.png](images%2Fconsole_log_counter.png)



Now replace App.jsx with below set of code.
```jsx
import { useState } from 'react';
import './App.css';

function App() {
    const [counter, setCounter] = useState(0);
    console.log('rendering app',counter);

    const clickHandler = () => {
        setCounter(counter + 1);
    };

    return (
        <>
            <h1>Hello Welcome to women who code</h1>
            <button onClick={clickHandler}>click me {counter}</button>
        </>
    );
}

export default App;
```

Now you see the counter value incrementing in the DOM.

Thats all about the basics, lets step in to build a real world simple app.

![foodland_components.png](images%2Ffoodland_components.png)

Lets try to understand different terminologies of React and
come back to do the full fledged development.

* Components
* React DOM
* JSX
* Fat arrow function
* Functional programming
* Array destructuring
* Object destructuring
* Async - await
* props
* React Hook - usestate


![openPreviewNewTab.png](images%2FopenPreviewNewTab.png)

#### 8.  Understand fetch and asynchronous calls

We will be using open api url to fetch food items
from below sample. Let's try to hit this url to see the results.
https://world.openfoodfacts.org/cgi/search.pl?search_terms=burger&page=1&page_size=10&json=1


Replace below lines of code within App.jsx.

```jsx
import { useState } from 'react';
import './App.css';

function App() {
    const [foodItems, setFoodItems] = useState([]);
    console.log('rendering component fooditems', foodItems);

    const searchFoodItems = async () => {
        try {
            const foodName = 'burger';
            const response = await fetch(
                `https://world.openfoodfacts.org/cgi/search.pl?search_terms=${foodName}&page=1&page_size=10&json=1`
            );
            const data = await response.json();
            console.log('data json',data);
            setFoodItems(data.products);

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
and print h1 heading tag for each food name.

#### 9.  Print simple product name in a list

Replace App.jsx code with the below set of code.

```jsx
import { useState } from 'react';
import './App.css';

function App() {
    const [foodItems, setFoodItems] = useState([]);
    console.log('rendering food items', foodItems);

    const searchFoodItems = async () => {
        try {
            const foodName = 'burger';
            const response = await fetch(
                `https://world.openfoodfacts.org/cgi/search.pl?search_terms=${foodName}&page=1&page_size=10&json=1`
            );
            const data = await response.json();
            console.log('data', data);
            setFoodItems(data.products);

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

##### 10. Unique list error

When you do so,
you will start to see some warnings in the console as shown below.
With React to uniquely identify elements we need to pass key.
This will hold good if you are trying to print list of items.


![listUniqueWarning.png](images%2FlistUniqueWarning.png)

To fix this error we modify code as shown below
Replace App.jsx with below set of code.

```jsx
import { useState } from 'react';
import './App.css';

function App() {
  const [foodItems, setFoodItems] = useState([]);
  console.log('rendering food items', foodItems);
  
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

### 11. Separate FoodCards jsx

Now lets do one thing. We plug out food items card to a separate
jsx component. This will make the code simple and readable and follow React 
principle of making each block as component.

Right click on src folder and click New File.
![NewFile.png](images%2FNewFile.png)

Name the file as `FoodCards.jsx`
⚠️ - Note the casing of file name if it is wrong it might not work as expected

![name_foodcardsjsx.png](images%2Fname_foodcardsjsx.png)

Copy paste below set of code to FoodCards.jsx


```jsx
const FoodCards = (props) => {
  const food = props.foodItem;
  return <h1>{food.product_name}</h1>;
};

export default FoodCards;
```

Replace App.jsx code with below lines of code

```jsx
import { useState } from 'react';
import './App.css';
import FoodCards from './FoodCards';

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
```jsx
 <div>
      {foodItems?.map((value, index) => {
        return <FoodCards key={index} foodItem={value} />;
      })}
</div>
```

We have also imported the FoodCards
![foodCardimport.png](images%2FfoodCardimport.png)

#### 12. Food data interesting points
* image_front_url
* product_name
* quantity
* expiration_date

Let's create a food card which can display above details in a nice manner
Replace FoodCards.jsx with below lines of code.

```jsx
const FoodCards = (props) => {
  // instead of writing const foodItem = props.foodItem
  // object destructuring
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
```jsx
const { foodItem } = props;
```

Now you will start seeing food list that gets displayed with image
quantity, expiry date, name. If you inspect console all the html tags
and authoring can be seen.

![foodcards_moreattrs.png](images%2Ffoodcards_moreattrs.png)

## 13. Better user experience with asynchronous call
Now we have refined the code to make it a bit more readable
and also introduced the concept of loading with asynchronous call.

We have written some logic here to initialize the list
first it is initialized with empty card.
We have introduced a loading state
so whenever user clicks on button loading state will be true
and once the load is complete it will be false.
If loading state is true we show "Page is loading..."


Replace App.jsx with below lines of code.


```jsx
import { useState } from 'react';
import './App.css';
import FoodCards from './FoodCards';

function App() {
    const [foodItems, setFoodItems] = useState([]);
    const [loading, setLoading] = useState(false);

    console.log('rendering component foodItems',foodItems);
    console.log('rendering component loading',loading)

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

    //initialize food list with empty cards first
    let foodList = (
        <div className={'empty'}>
            <h2>No food found</h2>
        </div>
    );

    if (loading) {
        foodList = <PageisLoading />;
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

### 14. Make Food search more dynamic
All this time we only see results for burger. 
Lets add a search box with search icon

create search.svg inside src folder
⚠️ (usually we create images inside asset folder, since this is a simple tutorial lets created inside src folder) 
file and copy below code
![createFile.png](images%2FcreateFile.png)

![nameFile.png](images%2FnameFile.png)
```svg
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

```jsx
import { useState } from 'react';
import './App.css';
import SearchIcon from './search.svg';
import FoodCards from './FoodCards';

const App = () => {
    const [foodItems, setFoodItems] = useState([]);
    const [searchTerm, setSearchTerm] = useState('burger');
    const [loading, setLoading] = useState(false);

    console.log('rendering component foodItems', foodItems);
    console.log('rendering component loading', loading);
    console.log('searchTerm', searchTerm);

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
            console.log('data', data);
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

#### 15. Lets try to search for our favorite food items here
![searchRandom.png](images%2FsearchRandom.png)

You are almost there. Now for a final touch to add some colors and beauty
lets do the below last step.

Update App.css with below code.
[App.css](App.css)


![finalSearchWithDosa.png](images%2FfinalSearchWithDosa.png)

🎉 ## Congratulations you have successfully completed the workshop