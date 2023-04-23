# VaishaliTyagi_FrontEnd
STEELEYE ASSIGNMENT

1) Explain what the simple List component does.

Solution -> The Simple List component in React.js is a useful tool for displaying lists of information in a clean and organized manner. It's a building block that can be used to create a variety of different list-based user interfaces, such as menus, product listings, and more.

To use the Simple List component in React.js, you simply pass an array of items as a prop, and the component will automatically generate a list of those items. This list can then be styled and customized to match the design of your application.

One of the benefits of using the Simple List component is that it allows you to abstract away some of the complexity of creating a list-based UI. Instead of having to manually create and style each list item, you can simply pass in an array of items and let the component do the work for you.

Overall, the Simple List component is a powerful and versatile tool for creating list-based user interfaces in React.js, and can help streamline the development process while improving the overall user experience.


---------------------------

2) What problems / warnings are there with code?

Solution -> The following Problems are there with the given code :- 

There is a mistake in the use of the useState hook in the WrappedListComponent. The selectedIndex variable is being set to the function that should be used to update the state value, instead of the initial state value. To correct this, the state value should be assigned to the first element of the array returned by useState.

The isSelected prop in the SingleListItem component is expecting a boolean, but it is being passed a number instead. This could cause unexpected behavior in the component, so the prop should be passed as a boolean value.


The onClickHandler prop in the SingleListItem component is not being called correctly. It needs to be wrapped in an arrow function to prevent it from being called immediately when the component is rendered.

The key prop is missing when rendering the SingleListItem components in the WrappedListComponent. This can cause performance issues and should be fixed by adding a unique key prop to each SingleListItem, such as key={index}.

There are two typos in the PropTypes declarations for the items prop. PropTypes.array should be PropTypes.arrayOf, and PropTypes.shapeOf should be PropTypes.shape.

The default value for the items prop in the WrappedListComponent defaultProps is null. This could cause issues when the component attempts to map over the items array, since null is not iterable. To fix this, the default value for the items prop should be an empty array.


---------------------------

3) Please fix, optimize, and/or modify the component as much as you think is necessary.

Solution :- 

import React, { useState, useEffect, memo, useCallback } from 'react';
import PropTypes from 'prop-types';

const SingleListItem = memo(({ index, isSelected, onClickHandler, text }) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? 'green' : 'red'}}
      onClick={() => onClickHandler(index)}
    >
      {text}
    </li>
  );
});

SingleListItem.propTypes = {
  index: PropTypes.number,
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const List = memo(({ items }) => {
  const [selectedIndex, setSelectedIndex] = useState(null);

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = useCallback((index) => {
    setSelectedIndex(index);
  }, []);

  return (
    <ul style={{ textAlign: 'left' }}>
      {items.map((item, index) => (
        <SingleListItem
          key={index}
          onClickHandler={handleClick}
          text={item.text}
          index={index}
          isSelected={selectedIndex === index}
        />
      ))}
    </ul>
  );
});

List.propTypes = {
  items: PropTypes.arrayOf(
    PropTypes.shape({
      text: PropTypes.string.isRequired,
    })
  ),
};

List.defaultProps = {
  items: null,
};

export default List;


------------------------------------------
