# Kundan-Kumar_Front-End

Answer 1: The List component in React is made up of two sub-components: SingleListItem and List. SingleListItem renders a single list item, and List renders a list of items. List uses the useState hook to keep track of the currently selected item's index and the useEffect hook to reset the selected index when the list items change.

When an item in the list is clicked, the handleClick function updates the selected index state variable. The List component maps over the list items and renders a SingleListItem for each item, passing the necessary props to each one. The isSelected prop is used to indicate which item is currently selected and changes the background color of the item to green or red accordingly. The key prop is used to ensure each item is uniquely identified by React.

Answer 2: There were some errors in the code the first error was we need to install the dependencies named props-types or @types/props-types second error was PropsTypes.arrayOf instead of PropsTypes.array and the third error was using PropsTypes.shape instead of PropsTypes.shape.

Answer 3: 
```
import React, { useState, useEffect, memo } from "react";
import PropTypes from "prop-types";

// Single List Item
const WrappedSingleListItem = ({ index, isSelected, onClickHandler, text }) => {
return (
<li
style={{
backgroundColor: isSelected ? "green" : "red"
}}
onClick={() => onClickHandler(index)}
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
const [selectedIndex, setSelectedIndex] = useState();

useEffect(() => {
setSelectedIndex(null);
}, [items]);

const handleClick = (index) => {
setSelectedIndex(index);
// console.log(index);
};

return (
<>
{items.map((item, index) => (
<ul style={{ textAlign: "left" }} key={index}>
<SingleListItem
onClickHandler={() => handleClick(index)}
text={item}
index={index}
isSelected={selectedIndex}
/>

))}
</>
);
};

WrappedListComponent.propTypes = {
items: PropTypes.arrayOf(
PropTypes.shape({
text: PropTypes.string
}).isRequired
)
};

WrappedListComponent.defaultProps = {
items: ["Books", "Laptop"]
};

const List = memo(WrappedListComponent);

export default List;
```

# Output

![image](https://user-images.githubusercontent.com/98895276/233848042-8bd61bf9-9ddf-419d-87ef-b41e925f65ca.png)
