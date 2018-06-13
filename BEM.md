## Rules

### Basic knowledges and explanations of BEM 
1. https://tech.yandex.com/bem/
2. https://en.bem.info/methodology/quick-start/
3. https://en.bem.info/methodology/naming-convention/

 We use ONLY naming rules for css classes
#### A little deviation from documentation
for modifier we don't use black name but write modifier directly.
Modifier has to start since prefix _ 
`_modifier-name_modifier-value` or just `_modifier-name`
	
### Rules

1.  Each template must start since class name of component
     ```
     <div class="component-name">
     
     </div>
     ```

2. Add styles ONLY on class. Add style on attributes you could only in following cases :
    1. on component tag:
    ```
    // .html
    <component-name></component-name>
    ```
    
    ```
    // .scss
    component-name {
    // styles
    }
    ```
    2. on material design component (if you don't have ability to add styles on class). Must use (>) child selectors https://developer.mozilla.org/en-US/docs/Web/CSS/Child_selectors
    ```
    // .scss
    &__elem > md-tabs-canvas {
    // styles
    }
    ```
3. In **scss** file & always point to block, depth more then 2 is forbidden. 
    ```
    // .scss
    // good
    .component-name {
        &__element {}
        &__element:hover {}
    }
    // bad
    .component-name {
        &__element {
            &:hover {}
        }
    }
    ```

Examples are available here [link](https://github.com/vorant/test-task-angular-1.5.x/tree/master/client/app/components)

