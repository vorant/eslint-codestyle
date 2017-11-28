# Codestyle guide
### Why we need it
- [Coding_conventions WIKI](https://en.wikipedia.org/wiki/Coding_conventions)
- [Why Enforcing Code Style is Important](https://coryrylan.com/blog/why-enforcing-code-style-is-important)

## E6 codestyle guide
Javascript styles list [rules](https://github.com/vorant/eslint-codestyle/blob/master/codestyle.md)
HTML styles [instruction](https://github.com/vorant/eslint-codestyle/blob/master/BEM.md)


## How to use
### There are 2 ways of using esliner. 
 - use in console
 - use in IDE (Webstorm, Sublime, etc.)
 
### For both cases you should do follows
- Download [.eslintrc](https://github.com/vorant/eslint-codestyle/blob/master/.eslintrc) and put in root folder of your project
- Set up npm dependencies
  ```javascript
    npm install eslint --save-dev
    // if you use AngularJs (v1.x.x)
    npm install eslint-plugin-angular --save-dev
    ```
    
### Use in console

- Add scripts to `package.json`
    ```
      "scripts": {
        ...
        "eslint": "./node_modules/.bin/eslint path/to/your/appFolder",
        "eslint-fix": "./node_modules/.bin/eslint --fix path/to/your/appFolder"
      },
    ```
    `path/to/your/appFolder` - path to folder which you want to check
- run npm command to check you project 
    ```
    npm run eslint
    ```
    
### Use in Webstorm
![Webstorm settings](https://github.com/vorant/eslint-codestyle/blob/master/webstorm-settings.png?raw=true)

### Use in Sublime
Read [instruction](http://jonathancreamer.com/setup-eslint-with-es6-in-sublime-text/)

## Ignore ESLint rules
Sometimes we need to skip some rules. (This)[https://eslint.org/docs/user-guide/configuring#disabling-rules-with-inline-comments] article describe you how to do it
