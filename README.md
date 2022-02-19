# LEVEN SEARCH

Leven Search is a Search algorithmen used for string based objects, or strings itself.

## Installation

To install the package simply write the following in the terminal.

```

npm i @themathkoch/leven-search

```
To use the package check that you are using "commonjs" as your package type. Then you can get the module via the following.

```

const levenSearch = require("@themathkoch/leven-search");

```

## GitHub

https://github.com/KilianKoch/Leven-Search

## Functions 

The package gives the following three functions to work with.

```
function dist(str1, str2) ~ levenSearch.dist

function pass(input, compare, threshold = 0.5, Leven = false, ...attr) ~ levenSearch.pass

function search(input, data, threshold = 0.5, Leven = false, ...attr) ~ levenSearch.search

```

The first function calculates the so called levenshtein distance for two strings. This distance describes the number of transformation needed to get to one string to the other. This distance will be calculated in O(nm), where n,m are the respective string lengths.

The second function checks if the input and compare value fits the threshold. There we use the following properties:

| property   |      datatype      |  usecase | standardValue |
|----------|:-------------:|------:|------:|
| input |  Obj/String | first Obj/String to Compare |none |
| compare |    Obj/String   |   second Obj/String to Compare |none |
| threshold | number |   threshold which must be exceeded |0.5 |
| Leven | bool |true,  threshold in [0,∞). false, threshold in [0,1)  |false |
| ...attr | Obj/String |which attr to compare |empty |

This function is in O(nm), with n,m the respectiv lengths of input and compare.

The third function is the search algorithmen to use for in Arrays. There we use the following properties:

| property   |      datatype      |  usecase | standardValue |
|----------|:-------------:|------:|------:|
| input |  Obj/String | Obj/STring to search |none |
| data |    Obj[]/String[]   |   Dataset to search in |none |
| threshold | number |   threshold which must be exceeded |0.5 |
| Leven | bool |true,  threshold in [0,∞). false, threshold in [0,1)  |false |
| ...attr | Obj/String |which attributes to compare to |empty |

In the case, that threshold < 0, the function will return []. In the case of threshold ≥ 1 (to be ignored when Leven = true), the result will be data.

## Examples

Here we have 3 short examples of usecases for the package.

### 1. Example
```

const levenSearch = require("@themathkoch/leven-search");

let str1 = "OneWord"
let str2 = "ÖneWord"
let str3 = "ThirdWord"

console.log(levenSearch.dist(str1,str2),levenSearch.dist(str2,str3),levenSearch.dist(str1,str3));
//Output 1 5 5

console.log(levenSearch.pass(str1,str2)); //ref. to Functions for the standard values
//Output true
console.log(levenSearch.pass(str2,str3))
//Output false

```
### 2. Example

```

const levenSearch = require("@themathkoch/leven-search");

let input = "Apple";

let data = ["Apple", "Grapple", "Banana", "Appletree", "pple"];

let threshold = 3;

let leven = true;

console.log(levenSearch.search(input, data, threshold, leven));
//Output [ 'Apple', 'Grapple', 'pple' ]

threshold = 0.6;

leven = false

console.log(levenSearch.search(input, data, threshold, leven));
//Output [ 'Apple', 'Grapple', 'Appletree', 'pple' ]

```

### 3. Example

```

const levenSearch = require("@themathkoch/leven-search");

let input = {1: "Apple", 2: "Euro", 3: "Tree"};

let data = [{1: "Grapple", 2: "Dollar", 3: "Forest"},{1: "Grapple", 2: "Eüro", 3: "Tre", 4: "Ignored"}, input];

let threshold = 3;

let leven = true;

console.log(levenSearch.search(input, data, threshold, leven, "1", "2", "3")); //Attribute 4 is ignored
/* Output
    [
        { '1': 'Grapple', '2': 'Eüro', '3': 'Tre' , '4': 'Ignored'},
        { '1': 'Apple', '2': 'Euro', '3': 'Tree' }
    ]
*/

console.log(levenSearch.search(input, data, threshold, leven, "1")); //Use only one attribute
/* Output
    [
        { '1': 'Grapple', '2': 'Dollar', '3': 'Forest' },
        { '1': 'Grapple', '2': 'Eüro', '3': 'Tre', '4': 'Ignored' },
        { '1': 'Apple', '2': 'Euro', '3': 'Tree' }
    ]
*/


```