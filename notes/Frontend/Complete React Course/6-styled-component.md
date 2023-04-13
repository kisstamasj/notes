# Styled Component

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
