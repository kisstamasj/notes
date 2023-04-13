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
