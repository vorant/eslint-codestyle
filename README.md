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
    npm install --save-dev eslint babel-eslint 
    // if you use AngularJs (v1.x.x)
    npm install --save-dev eslint-plugin-angular 
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

## Disabling Rules with Inline Comments
Sometimes we need to skip some rules. 

To temporarily disable rule warnings in your file, use block comments in the following format:

```
/* eslint-disable */

alert('foo');

/* eslint-enable */
```

You can also disable or enable warnings for specific rules:
```
/* eslint-disable no-alert, no-console */

alert('foo');
console.log('bar');

/* eslint-enable no-alert, no-console */
```
To disable rule warnings in an entire file, put a /* eslint-disable */ block comment at the top of the file:
```
/* eslint-disable */

alert('foo');
```
You can also disable or enable specific rules for an entire file:
```
/* eslint-disable no-alert */

alert('foo');
```
To disable all rules on a specific line, use a line comment in one of the following formats:
```
alert('foo'); // eslint-disable-line

// eslint-disable-next-line
alert('foo');
```
To disable a specific rule on a specific line:
```
alert('foo'); // eslint-disable-line no-alert

// eslint-disable-next-line no-alert
alert('foo');
```
To disable multiple rules on a specific line:
```
alert('foo'); // eslint-disable-line no-alert, quotes, semi

// eslint-disable-next-line no-alert, quotes, semi
alert('foo');
```
All of the above methods also work for plugin rules. For example, to disable `eslint-plugin-example`’s `rule-name` rule, combine the plugin’s name (`example`) and the rule’s name (`rule-name`) into `example/rule-name`:
```
foo(); // eslint-disable-line example/rule-name
```
**Note**: Comments that disable warnings for a portion of a file tell ESLint not to report rule violations for the disabled code. ESLint still parses the entire file, however, so disabled code still needs to be syntactically valid JavaScript.


