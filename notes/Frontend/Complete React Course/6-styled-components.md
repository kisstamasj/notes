# Styled Components

Generate unique class names and protect from any style clashes.

## Convert SASS css to styled-components

1. Install: ```yarn add styled-components```
2. Rename ```scss``` file extension to ```jsx```
3. Convert styles:
   ```js
    import styled from "styled-components";

    export const NavigationContainer = styled.div`
      height: 70px;
      width: 100%;
      display: flex;
      justify-content: space-between;
      margin-bottom: 25px;
    `
   ```
4. Use like a component:
   ```jsx
   import { NavigationContainer } from './navigation.styles';
   
   ...
   
   <NavigationContainer>
   
      ...
      
   </NavigationContainer>
   ```
   
5. Using components inside styled component:
   ```js
   import { Link } from "react-router-dom";

   ...

   export const LogoContainer = styled(Link)`
     height: 100%;
     width: 70px;
     padding: 25px;
   `
   ```
   The ```LogoContainer``` will be a ```Link``` component from ```react-router-dom```, so when you used it will be have all props it has.

6. Rendering the component as a different HTML element:
   ```jsx
     <NavLink as='span' onClick={signOutUser}>
        Sign Out
      </NavLink>
   ```
   Using the ```as``` keyword we can render the component as a different HTML element.
   
7. Using a base class to inherit from:
   ```jsx
   import styled from 'styled-components';

   export const BaseButton = styled.button`
     min-width: 165px;
     width: auto;
     height: 50px;
     letter-spacing: 0.5px;
     line-height: 50px;
     padding: 0 35px 0 35px;
     font-size: 15px;
     background-color: black;
     color: white;
     text-transform: uppercase;
     font-weight: bolder;
     border: none;
     cursor: pointer;
     /* display: flex; */
     justify-content: center;
     font-weight: 100;
     transition: 300ms ease all;

     &:hover {
       background-color: white;
       color: black;
       border: 1px solid black;
     }
   `;

   export const GoogleSignInButton = styled(BaseButton)`
     background-color: #4285f4;
     color: white;

     &:hover {
       background-color: #357ae8;
       border: none;
     }
   `;

   export const Inverted = styled(BaseButton)`
     background-color: white;
     color: black;
     border: 1px solid black;

     &:hover {
       background-color: black;
       color: white;
       border: none;
     }
   `;

   ```
   
## Rendering component by a given string parameter
```jsx
import { BaseButton, GoogleSignInButton, Inverted } from './button.styles.jsx';

// possible types
export const BUTTON_TYPE_CLASSES = {
  base: 'base',
  google: 'google-sign-in',
  inverted: 'inverted',
};

// get the correct styled component by the given type parameter
const getButton = (buttonType = BUTTON_TYPE_CLASSES.base) => {
  return {
    [BUTTON_TYPE_CLASSES.base]: BaseButton,
    [BUTTON_TYPE_CLASSES.google]: GoogleSignInButton,
    [BUTTON_TYPE_CLASSES.inverted]: Inverted,
  }[buttonType];
};

const Button = ({ children, buttonType, ...otherProps }) => {
  const CustomButton = getButton(buttonType);
  return <CustomButton {...otherProps}>{children}</CustomButton>;
};

export default Button;
```

## Props in styled component
You can make custom properties for a styled component, and you can access it in a styled component.
```jsx
import { BackgroundImage, Body, DirectoryItemContainer, H2, P } from './directory-item.styles.jsx';

const DirectoryItem = ({ category }) => {
  const { imageUrl, title } = category;
  return (
    <DirectoryItemContainer>
      <BackgroundImage imageUrl={imageUrl} />
      <Body>
        <H2>{title}</H2>
        <P>Shop Now</P>
      </Body>
    </DirectoryItemContainer>
  );
};

export default DirectoryItem;

```

```jsx
import styled from 'styled-components';

export const BackgroundImage = styled.div`
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  background-image: ${({ imageUrl }) => `url(${imageUrl})`};
`;
```

## Insert CSS from variable
```jsx
import styled, { css } from 'styled-components';

const shrinkLabelStyles = css`
  top: -14px;
  font-size: 12px;
  color: ${mainColor};
`;

export const FormInputLabel = styled.label`
  color: ${subColor};
  font-size: 16px;
  font-weight: normal;
  position: absolute;
  pointer-events: none;
  left: 5px;
  top: 10px;
  transition: 300ms ease all;
   
  /* shrink comes from param, and insert here the shrinkLabelStyles variable content*/ 
  ${({ shrink }) => shrink && shrinkLabelStyles};
`;
```
