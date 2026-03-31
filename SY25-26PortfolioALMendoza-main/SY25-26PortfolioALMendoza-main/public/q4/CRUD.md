# CRUD Process

The term CRUD refers to the four basic operations you can perform on data in most applications, specifically it stands for Create, Read, Update and Delete.  Understanding how these four operations work will help you manage your website's data well.

These operations could be applied on data saved inside a JSObject, Data saved in localStorage and also Data saved inside a database.

Below is a complete code to implement it in JS Object only and then followed by implementing it using the localStorage

## A. Example to implement CRUD on JS Object below
### Try the example here: [CRUD with JSObject](https://onecompiler.com/javascript/44eh47nwv)

```js
// Our main object: an anime collection with multiple characters
let animeCollection = {
  naruto: { name: "Naruto Uzumaki", age: 17, anime: "Naruto" },
  luffy: { name: "Monkey D. Luffy", age: 19, anime: "One Piece" },
  goku: { name: "Son Goku", age: 30, anime: "Dragon Ball Z" }
};
```

### C – Create

This means adding new data.

Example: Adding a new anime character to your collection.

In code:

```js
// 1. ADD a new character **sakura**

animeCollection.sakura = { name: "Sakura Haruno", age: 17, anime: "Naruto" };

// Note: you can also use the square bracket notation like so below:
// animeCollection["sakura"] = { name: "Sakura Haruno", age: 17, anime: "Naruto" };

console.log("\n1. The animeCollection object after adding sakura\n")
console.log(animeCollection);
```

### R – Read

This means retrieving or viewing data that already exists.

Example: Checking the name of a character.

In code:

```js
// 2b. READ a character information

console.log("\nReading Specific information from animeCollection \n")
console.log(animeCollection.luffy.name);   // Monkey D. Luffy
console.log(animeCollection.goku.anime);   // Dragon Ball Z

// 2b. READ through the object

console.log("\n2. Reading all data in animeCollection \n")

for (let key in animeCollection) {
  console.log(key, "=", animeCollection[key])
}
```

### U – Update

This means modifying existing data.

Example: Changing Naruto’s age after his birthday.

In code:

```js
// 3a. UPDATE a character information

animeCollection.naruto.age = 18; // Naruto had a birthday!

console.log("\n3a. Anime Collection after an update on naruto \n")
console.log(animeCollection.naruto);

// Result: { name: 'Naruto Uzumaki', age: 18, anime: 'Naruto' }

// 3b. Updating by adding a new entry

console.log("\n3b. Adding new anime Anime  \n")

animeCollection.perseus = { name: "Perseus", age: 25, anime: "Clash of the Titans" };

console.log(animeCollection.perseus);

// Result: { name: "Perseus", age: 25, anime: "Clash of the Titans" }
```

### D – Delete

This means removing data.

Example: Removing a character from the collection.

In code:

```js
// 4. DELETE a character

console.log("\n4. Deleting an entry from the animeCollection \n")

delete animeCollection.goku;

console.log(animeCollection);

// goku is gone, only naruto, luffy, and sakura remain
```



## B. The Example to implement CRUD on JS Object with localStorage

The process of CRUD with localStorage is that it should be applied first on the JSObject. The localStorage will be updated each time CRUD process had been done on the the JSOject, so take note when a line containing localStorage method is used.

### Try the example here: [Putting it all together on a website](https://onecompiler.com/html/44eh6pd3u)

```js
// Our anime collection object
let animeCollection = {
  naruto: { name: "Naruto Uzumaki", age: 17, anime: "Naruto" },
  luffy: { name: "Monkey D. Luffy", age: 19, anime: "One Piece" },
  goku: { name: "Son Goku", age: 30, anime: "Dragon Ball Z" }
};
```

### C-Create

```js
// 1. SAVE to localStorage
localStorage.setItem("animeCollection", JSON.stringify(animeCollection));
// Data is stored as a string, so we use JSON.stringify
```

### R-ead

```js
// 2. READ from localStorage
let savedCollection = JSON.parse(localStorage.getItem("animeCollection"));
console.log(savedCollection.luffy.name); // Monkey D. Luffy
// savedCollection will return null if there is no saved data
```

### U-Update

```js
// 3. UPDATE a character (age of Naruto)
savedCollection.naruto.age = 18;

// Save the updated object back to localStorage
localStorage.setItem("animeCollection", JSON.stringify(savedCollection));
```

### D-Delete

```js
// 4. DELETE a character (remove Goku)
delete savedCollection.goku;

// Save again after deletion
localStorage.setItem("animeCollection", JSON.stringify(savedCollection));

// 5. CLEAR everything (optional)

localStorage.removeItem("animeCollection");
```

### Do note that when you are reading, updating/adding, deleting, you need to check first if the data exists.  The sample line below is helpful when you implement this on your website:

```js
// Load saved collection or start fresh
    let animeCollection = JSON.parse(localStorage.getItem("animeCollection")) || {};
```

This line tries to load the saved collection from localStorage. If there is no saved data (i.e., it returns null), it initializes animeCollection as an empty object {}. This way, you can safely perform CRUD operations without running into errors due to missing data.  This simplifies into one line the the if..else statement that is shown below

```js
// Check if data exists in localStorage
let animeCollection;
if (localStorage.getItem("animeCollection")) {
  animeCollection = JSON.parse(localStorage.getItem("animeCollection"));
} else {
  animeCollection = {};
}
```

