#### Frontend Developer Assignment(Steel Eye)


**Q1. Explain what the simple List component does.**

**Ans:**
Lists are commonly used on websites to display menus and to display data in an ordered format. Lists in React can be created in the same way that they are in JavaScript.
For traversing the lists, the map() function is used. The map() function in the following example takes an array of numbers and multiplies their values by 5. We log the new array returned by map() and assign it to the variable multiplyNums.
e.g.
>
var numbers = [1, 2, 3, 4, 5];   
const multiplyNums = numbers.map((num)=>{   
    return (num * 5);   
});   
console.log(multiplyNums);   
>
----

**Q2. What problems/warnings are there with the code?**
**Ans:**
>
While using useState() the 'set' variable should be after the local variable.
Fixed code:
const [selectedIndex, setSelectedIndex] = useState();
Syntax error of PropTypes in WrappedListComponent. It should be arrayOf instead of shapeOf.
Fixed code:
WrappedListComponent.propTypes = {
items: PropTypes.arrayOf(
PropTypes.shape({
text: PropTypes.string.isRequired
})
)
};
>
WrappedListComponent.defaultProps has items: null. Therefore there is no item to be mapped.

**Fixed code:**
>>
WrappedListComponent.defaultProps = {
items: [{ text: "First Item" }, { text: "Second Item" }]
};
Each child in a list should have a unique "key" prop.
Fixed code:
<ul style={{ textAlign: "left" }}>
{items.map((item, index) => (
<SingleListItem
onClickHandler={() => handleClick(index)}
text={item.text}
index={index}
isSelected={selectedIndex}
key={index}
/>
))}

Invalid prop is selected of type array supplied to WrappedSingleListItem, expected boolean. Therefore converting it to boolean.

**Fixed code:**
<li
style={{ backgroundColor: isSelected ? "green" : "red" }}
onClick={() => onClickHandler(Boolean(index))} >
{text}

const handleClick = (index) => {
setSelectedIndex(Boolean(index));
console.log("This is index: " + index);
};
>>
----
**Q3. Please fix, optimize, and/or modify the component as much as you think is necessary.**
**Ans**
>>
import React, { useState, useEffect, memo } from "react";
import PropTypes from "prop-types";

// Single List Item
const WrappedSingleListItem = ({ index, isSelected, onClickHandler, text }) => {
return (
<li
style={{ backgroundColor: isSelected ? "green" : "red" }}
onClick={()=>onClickHandler(index)}
>
{text}

);
};

WrappedSingleListItem.propTypes = {
index: PropTypes.number,
isSelected: PropTypes.bool,
onClickHandler: PropTypes.func.isRequired,
text: PropTypes.string.isRequired
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({ items }) => {
const [selectedIndex, setSelectedIndex] = useState(false);

useEffect(() => {
setSelectedIndex();
}, [items]);

const handleClick = (index) => {
setSelectedIndex(true);
};

return (
<ul style={{ textAlign: "left" }}>
{items.map((item, index) => (
<SingleListItem
onClickHandler={() => handleClick(index)}
text={item.text}
index={index}
key={index}
isSelected={selectedIndex}
/>
))}

);
};

WrappedListComponent.propTypes = {
items: PropTypes.arrayOf(
PropTypes.shape({
text: PropTypes.string.isRequired
})
)
};

WrappedListComponent.defaultProps = {
items: [
{ text: "Kaushal", index: 1 },
{ text: "Kaushal Kumar", index: 1 },
{ text: "mail4kaushal.kr@gmail.com", index: 1 }
]
};

const List = memo(WrappedListComponent);

export default List;
>>
--------------------------------------------------------------------------------------------------------------------------------------
**Thank you!**
Submitted By: Kaushal Kumar
College: Lovely Professional University
Email: Mail4kaushal.kr@gmail.com
C. No: +91 7970513448
--