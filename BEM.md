Правила

1. Основные понятия 
    1. https://tech.yandex.ru/bem/
    2. https://en.bem.info/methodology/quick-start/
2. Из БЭМа используем ТОЛЬКО правила нейминга классов
3. Нэйминг
	
```
<div class="component-name__element-name _modifier-name_modifier-value">
</div>
```
4. Правила
    1. Каждый компонент проекта - это блок
        > Каждый шаблон компонента должен начинаться с класса с именем этого компонента
        > ```
        > <div class="component-name">
        > 
        > </div>
        > ```

    2. Стили вешать только на класс, вешать стили на тэги можно лишь в следующих случаях:
        1. на тэг компонента:
        ```
        // html
        <component-name></component-name>
        ```
        
        ```
        // scss
        component-name {
        // styles
        }
        ```
        2. на компонент материл дизайна (при невозможности добавить ему класс), обязательно использовать (>) дочерние селекторы http://htmlbook.ru/css/selector/child, чтобы эти стили не повлияли на вложенные компоненты
        ```
        // scss
        &__elem > md-tabs-canvas {
        // styles
        }
        ```

    3. модификатор должен начинаться с префикса _ `_modifier-name_modifier-value` или просто `_modifier-name`
    4. в **scss** файле & указывает на блок, запрещена вложенность более 2 
    ```
    // scss
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



