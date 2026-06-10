## agar humein data kahin se fetch krna hai toh kya krte hain useEffect se fetch krte hain aur useState mein store krte hain

```
const Products=()=>{
  const [products,setProducts]=useState([])

 useEffect(() => {
  const fetchProducts = async () => {
    const response = await fetch(
      "https://dummyjson.com/products"
    );

    const data = await response.json();

    setProducts(data.products);
  };

  fetchProducts();  
}, []);


  return(
    <div>
    Products
    </div>
  )
}


```

### Important thing to note here How something can cause infinite loop

```
My question was
useEffect(() => {
  const fetchProducts = async () => {
    const response = await fetch(
      "https://dummyjson.com/products"
    );

    const data = await response.json();

    setProducts(data.products);
  };

  fetchProducts();  
}, []); Here i have not passed any dependency array so
will it go like this
first component is mounted so when it is mounted useeffect calls the api and it loads the products data in product state by causing setProducts(data.products) but will it cause again rerender because it is changing the state of Products but this time there will be no api calling since there is no dependency array 
but lets say i want whenever products change it should call the api so how to do it


```

```
Solution-
Your understanding is almost correct. Let's trace it carefully.

useEffect(() => {
  fetchProducts();
}, []);
Step 1: Initial Render
products = []

React renders the component.

Step 2: useEffect runs

Because the dependency array is [], React runs the effect once after the component is mounted.
API Call
↓
response.json()
↓
setProducts(data.products)
Step 3: State changes
setProducts(data.products);

changes state.

Whenever state changes, React re-renders the component.

Render #2
products = [all products]
Step 4: Does useEffect run again?

No.

React compares dependencies:

[]

Nothing to compare, so React treats it as "run only on mount".

Render #1
↓
Effect runs
↓
setProducts()
↓
Render #2
↓
Effect DOES NOT run



But infinite loop
"Whenever products change, call the API"

You can do:

useEffect(() => {
  fetchProducts();
}, [products]);

But this is usually wrong.

Why?

Effect
↓
API Call
↓
setProducts()
↓
products changed
↓
Effect again
↓
API Call
↓
setProducts()
↓
products changed
↓
Effect again
...

Infinite loop again.


```

```
Real solution

Scenario A: You want a "Refresh" button
If you want the API to be called again when a user clicks a button, you can create a dummy state variable just to trigger the effect.

JavaScript
const [products, setProducts] = useState([]);
const [refreshTrigger, setRefreshTrigger] = useState(0);

useEffect(() => {
  const fetchProducts = async () => {
    const response = await fetch("https://dummyjson.com/products");
    const data = await response.json();
    setProducts(data.products);
  };

  fetchProducts();  
}, [refreshTrigger]); // <-- Runs whenever refreshTrigger changes

// In your JSX:
<button onClick={() => setRefreshTrigger(prev => prev + 1)}>
  Refresh Products
</button>

int overflow
Is there a better way?
Even though the number counter is 100% safe from crashing, if the idea of an infinitely growing number still bothers your engineering instincts, you can completely avoid it by using an object reference instead.

Since React triggers a re-render whenever an object reference changes in memory, you can do this:

JavaScript
const [refreshTrigger, setRefreshTrigger] = useState({}); // Empty object

// Inside your useEffect dependency array: [refreshTrigger]

// Creates a brand new object in memory, triggering the effect
<button onClick={() => setRefreshTrigger({})}>
  Refresh Products
</button>
Both the number counter (prev + 1) and the new object ({}) methods are widely used, standard patterns in React. You can confidently use either one without fearing a runtime error!

Scenario B: You want to fetch based on a Category or Page Number
If your data changes based on a user selecting a category or moving to page 2, you track that variable in the dependency array, not the products themselves.

JavaScript
const [products, setProducts] = useState([]);
const [category, setCategory] = useState("smartphones");

useEffect(() => {
  const fetchProducts = async () => {
    // The API url now depends on the category state
    const response = await fetch(`https://dummyjson.com/products/category/${category}`);
    const data = await response.json();
    setProducts(data.products);
  };

  fetchProducts();  
}, [category]); // <-- Safely runs only when the 'category' changes

// In your JSX:
<button onClick={() => setCategory("laptops")}>
  Load Laptops
</button>


```

### Now loading state dikhana hai
```

const Products=()=>{
  const [products,setProducts]=useState([])
  const [isLoading,setIsloading]=useState(false)
    const[isError,setIsError]= useState(null);

 useEffect(() => {
  const fetchProducts = async () => {
 try{
    setIsloading(true)
    setIserror(null);-> ye pehle error ko remove krega
    const response = await fetch(
      "https://dummyjson.com/products"
    );-> isme ye error ni dega agar url galat hai
    
    const data = await response.json();- ye error dega isliey axios use kro

    setProducts(data.products);
    setIsloading(false)
  };
 }
 catch{
    seterror(err.message);
    setloading(false);
 }
    

  fetchProducts();  
}, []);

    if(isloading)return(<h3>spinner</h3>)
  return(
    <div>
    Products
    </div>
  )
}

agar error aa gya toh hmesha isloading true rhegi 
so error handle ke liye 




```
### Tanstack Query

```

useQuery(Tanstack Query)-> koi chiz fetch krna hai
```