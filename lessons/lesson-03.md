# FEW 2.5 - Lesson 3

<!-- Put a link to the slides so that students can find them -->

<!-- ➡️ [**Slides**](https://make-school-courses.github.io/FEW-2.5-Data-Visualization-and-Web-Graphics/Slides/Lesson-4.html ':ignore') -->

<!-- > -->

## Overview

In the last lesson you organized and extracted values from a dataset. The next step is to make this data visible. The goal now is take all of the values and tunr them into something that can be displayed. 

<!-- > -->

## Why is this important?

Turning data into something that people can easily understand is why we make websites! 

<!-- > -->

## Learning Objectives










## Infographic vs Data Visualization

Let's clarify what you are expected to make.

An infographic provides information in the form of an image. These are often more comic strip and less abstract. The goal is to inform.

A data visualization is more abstract showing data in visual form.


Some examples

- [Info Graphic](https://venngage.com/blog/what-is-an-infographic/)

- Data visualizations Examples
  - [What is data visualization](https://www.tableau.com/learn/articles/data-visualization)
  - [Tableau Best Data viz examples](https://www.tableau.com/learn/articles/best-beautiful-data-visualization-examples)
  - [Best Data Visualizations 2018](https://visme.co/blog/best-data-visualizations/)
  - [James Round](https://www.jamesrounddesign.com)
  - [Data visualization](https://datavizcatalogue.com)
  - [Examples](https://www.maptive.com/17-impressive-data-visualization-examples-need-see/)

Generative art and Data: 
- https://www.ted.com/playlists/201/art_from_data
- https://joshuadavis.com
- https://www.theatlantic.com/entertainment/archive/2015/05/the-rise-of-the-data-artist/392399/
- https://techcrunch.com/2016/05/08/the-digital-age-of-data-art/














<!-- > -->

## Distributions

A distribution shows how many times a value appears. While seeing a list of people who survived and did not survive is interesting, showing how many survived by class, fare, or gender might add insight to the data.

A distribution shows how many times a value appears. For example we might have 891 passengers who each boarded the Titanic in a class. The distribution would show how many passengers were in each class.

Often you won't know how many 'buckets' you will have for a group. For example in the case of the Titanic we might not know the number of classes.

<!-- > -->

An easy way to create a distribution is to use an object. Use the key to track 'buckets' and the value of the key to count the occurrence of a value.

```JS
// Create a distribution
function createDistribution(data) {
  return data.reduce((acc, value) => {
    if (acc[value] !== undefined) {
      acc[value] += 1
    } else {
      acc[value] = 1
    }
    return acc
  }, {})
}

const d = [0, 1, 1, 3, 6, 6, 6, 7, 7, 8, 8, 8, 9, 9, 9, 10, 11, 12, 12, 12]
createDistribution(d) // returns:
// {0: 1, 1: 2, 3: 1, 6: 3, 7: 2, 8: 3, 9: 3, 10: 1, 11: 1, 12: 3}
// This says the number 7 appears 2 times in d.
// The numbers 8 and 9 appear 3 times etc.
console.log(createDistribution('javascript'.split('')))
// {j: 1, a: 2, v: 1, s: 1, c: 1, r:1, p: 1, t:1}
```

<!-- > -->

### Distributions Activity

Make a distribution for our previous example! Your distribution should show how many Titanic passengers were in each class

<!-- > -->

## Sorting

[`Array.sort()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) sorts an array alphabetically (UTF-16 code units values), in place. This applies to numbers, by sorting on the first digit. For example 10, 200, 3000 etc.

Use a compare function – `Array.sort([sorting-func])` – to sort on your own criteria. This function receives two parameters, which are two elements ``(a, b)`` from the array. It should returns -1 (`a` should be sorted before `b`), +1 (`b` should sorted before `a`), or 0 (the elements should remain in place).

```JS
const arr = 'javascript'.split('')
arr.sort()
console.log(arr) // Returns:
// ["a", "a", "c", "i", "j", "p", "r", "s", "t", "v"]
```

<!-- > -->

For numbers this sorts on the **first digit** which may not be what you want!

For all other cases supply `Array.sort()` with a sorting function that receives two params. These are values to compare. Your function should return -1, +1, or 0. This determines which value comes before the other.

For example:

```JS
const numbers = [10, 9, 8, 4, 12, 5, 7, 9, 6, 8, 10, 8, 5, 6, 10, 11, 6, 5, 11, 5]
numbers.sort((a, b) => a - b) // Rearranges numbers to:
// [4, 5, 5, 5, 5, 6, 6, 6, 7, 8, 8, 8, 9, 9, 10, 10, 10, 11, 11, 12]
```

<!-- > -->

### Sorting Activity

Write a sorting function that sorts in reverse order (so for numbers, sorts largest to smallest, or for letters, reverse alphabetically).

<!-- > -->

## Filtering

[`Array.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) returns a new array which is a subset of the original array.

You can supply a filter function that receives an element from the array, and returns `true` if that element should be included or `false` if it should not be included.

The filter function should return true when an item is to be included and false when it is not included.

```JS
const class3Passengers = titanicData.filter((passenger) => passenger.fields.pclass === 3)
// class3Passengers has only passengers where fields.pclass === 3
```

<!-- > -->

### Filtering Activity

Filter all Titanic passengers who were younger than 30

<!-- > -->

## Holding Elements

Once you have created elements you might want to hold onto them. This is good if you have a fixed number of elements and you want to display different data points owned by each.

Since you're making the elements based on your data, might as well save reference to those elements at the moment they are created!

<!-- v -->

Imagine you're starting with the Titanic dataset from the JSON. Add an element to each object:

```JS
// Set up your elements and save them to objects in data
data.forEach((passenger, i) => {
	const el = document.createElement('div')
	...
	passenger.el = el
	...
})
```

After you can access the elements from your data.

```JS
// From here you could
data.forEach((passenger, i) => {
	...
	passenger.el.style.height = `${passenger.fields.age / maxAge * 400}px`
	...
})
```

<!-- v -->

### Holding Elements Activity

Create a `div` for each passenger, and use their `fare` as a factor in calculating the width of their `div`. Look at the previous example to help guide you.

<!-- > -->

## Animating changes

Use CSS transitions to set the time it takes for changes in all CSS properties to take place. You can set the time in milliseconds `ms` or seconds `secs`. For example:

`transition: 400ms;`

You can optionally include a property to animate, ignoring other properties.

`transition: height 400ms;`

Include a list of properties and times to assign a different time to each property that may change:

`transition: height 400ms, color 1200ms;`

<!-- v -->

You can also include an _easing function_. This sets the curve of the change.

A linear curve maintains a constant rate of change. This is a good for color and opacity changes.

`Ease In` accelerates the change over time.

`Ease out` decelerates change over time.

`transition: height 400ms ease-out, color 1200ms linear;`

The [timing function](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function) has a lot of options.

<!-- v -->

### Animation Activity

Create a transition for the `div`s you made in the previous activity.

<!-- > -->

## CSS transform

The CSS transform property provides methods to move, scale, rotate, and skew elements. There are also a set of 3d transforms. The 3d transforms use the hardware acceleration and should be used when possible, even if you are not thinking of transforming an element in 3 dimensions.

For example:

`transform: translate(100px, 200px)` translates an object `100px` on the x and `200px` on the y.

`transform: translate3d(100px, 200px, 0)` same as above, but also translates `0` on the z while also taking advantage of hard acceleration. You should always use this when animating elements!

<!-- v -->

Only define `transform` once! it takes as many properties as needed. For example:

`transform: translate3d(300px, 0, 0) rotate3d(0, 0, 45deg)`

The order transforms are applied matters! The example above translates 300px to the right, then rotates 45 degrees on the z axis. Swapping the rotate and translate here would rotate first, then move the object down and to the right at a 45 degree angle!

<!-- v -->

### Helpful Documentation

- [translate(x, y)](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/translate)
- [translate3d(x, y, z)](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/translate3d)
- [scale(x, y)](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/scale)
- [scale3d(x, y, z)](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/scale3d)
- [rotate(angle)](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/rotate)
- [rotate3d(angleX, angleY, angleZ)](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/rotate3d)
- [skew(angleX, angleY)](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/skew)

<!-- v -->

### Transform Activity

Take at least 3 of the transform functions above and manipulate some Titanic data with it!

<!-- > -->

## Using closures for fun and profit!

Remember that you can utilize the properties of items within closures to help you dynamically create elements. Check out this example below where we take an array of data, and use it to create `div` objects:

```JS
// Data is an array of objects
const data = [{a:45, b:88, c:'group-a'}, {}, ...]

data.forEach((item) => {
	const el = document.createElement('div')
	el.setHeight = () => {
		el.style.height = `${item.a}%`
	}
})
```

<!-- > -->

<!-- .slide: data-background="#087CB8" -->
## [**10m**] BREAK

<!-- > -->

## Lab

Check out this [YouTube dataset](https://www.kaggle.com/datasnaek/youtube-new), and use it to perform the following operations:

1. Get the top 100 most liked videos, and sort them by number of dislikes
1. Filter the videos to only display videos that have over 600,000 views
1. Display the top 100 most liked videos in rectangle `div` to make a bar graph, and vary their color by number of dislikes
1. Animate the colors of the bar graph in the previous question
1. Make the bars in the graph grow when rendered using transforms/transitions

<!-- > -->

## After Class

- Start [Visualization 2](Assignments/Data-Visualization-2.md), due 2/12 11:59pm


<!-- > -->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Overview and Learning Outcomes                |
| 0:05        | 0:15      | Distributions                  |
| 0:20        | 0:10      | Sorting       |
| 0:30        | 0:10      | Filtering                     |
| 0:40        | 0:15      | Holding Elements      |
| 0:55        | 0:15      | Animations      |
| 1:10        | 0:15      | CSS Transforms      |
| 1:25        | 0:10      | Closures      |
| 1:35        | 0:10      | BREAK      |
