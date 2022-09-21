# Lieu
![npm bundle size](https://img.shields.io/bundlephobia/min/lieu)
[![](https://data.jsdelivr.com/v1/package/npm/lieu/badge?style=rounded)](https://www.jsdelivr.com/package/npm/lieu)
![npm](https://img.shields.io/npm/dm/lieu)
![GitHub](https://img.shields.io/github/license/LeadrateMSK/lieu)
![GitHub issues](https://img.shields.io/github/issues/LeadrateMSK/lieu)

JavaScript plugin for adding multilingual website.

## Installation
`npm install lieu` or download lieu.js from /dist.

### ES6
```javascript
import Lieu from 'lieu';

const lieu = new Lieu({/* ... */});
```

### CommonJS
```javascript
const Lieu = require('lieu');

const lieu = new Lieu({/* ... */});
```

### UMD (+ jsDelivr)
```html
<script src="https://cdn.jsdelivr.net/npm/lieu@1.3.1"></script>

<script>
const lieu_ctx = new lieu({/* ... */});
</script>
```

## Usage
### Initialization
```javascript
import Lieu from 'lieu';

const lieu = new Lieu({
    isDebug: true, // default "false"
    initialLanguage: 'en', // default automatically or the first language in the list
    attributeName: 'data-lieu', // default "data-lieu"
    
    languages: {
        en: {
            name: 'English',
            locales: {
                'Hello': 'Hello!',
                'Bye': 'Bye!',
                'HelloName': 'Hello %{name} %{surname}!',
                // [] and {} brackets are acceptable
                'Apples': '{1}There is one apple|[2,5]There are some %{name}|{5,*}There are many %{name}',
            },
        },
        tr: {
            name: 'Türk',
            locales: {
                'Hello': 'Merhaba!',
                'Bye': 'Hoşçakal!',
                'HelloName': 'Merhaba %{name} %{surname}!',
            },
        },
        // ...{pt: {...}, zh: {...}, /* ... */}
    }, 
    
    // or
    // languages: require('languages.json'),

    // Hooks
    onSetLang(newLang, oldLang){ /* your code */ } , // 
    onGetLang(){ /* your code */ } , // 
});
```

### Usage in JavaScript
```javascript
import Lieu from 'lieu';

const lieu = new Lieu({/* ... */});

// translate strings
lieu.trans('Hello'); // "Merhaba!" (if Turkish is selected)

// other methods
lieu.setLang('tr'); // set new language
lieu.getLang('tr'); // get language
lieu.getLangs(); // get all languages
```
#### Replacing Parameters In Translation Strings
```javascript
lieu.trans('HelloName', { name: 'John', surname: 'Doe' }); // "Hello John Doe!" (if English is selected)
```

#### Pluralization
```javascript
lieu.trans('Apples', 1); // "There is one apple" (if English is selected)
lieu.trans('Apples', 3, { name: 'apples' }); // "There are some apples"
lieu.trans('Apples', { name: 'apples' }, 30); // "There are many apples"
```

### Usage in HTML
```html
<span data-lieu="Hello"></span>
<span data-lieu="Bye"></span>
```

#### Replacing Parameters In Translation Strings
```html
<h1 data-lieu="HelloName" data-lieu-name="John" data-lieu-surname="Doe"></h1>
<!-- After Initialization becomes (if English is selected): -->
<h1 data-lieu="HelloName" data-lieu-name="John" data-lieu-surname="Doe">
    Hello John, Doe!
</h1>
```

#### Pluralization
```html
<span data-lieu="Apples" data-lieu-name="apples" data-lieu-plural="4"></span>
<!-- After Initialization becomes: -->
<span data-lieu="Apples" data-lieu-name="apples" data-lieu-plural="4">
    There are some apples
</span>
<!-- NOTE: Data attribute for pluralization always should be "plural"! -->
```

```javascript
<script src="https://cdn.jsdelivr.net/npm/lieu"></script>

<script>
    const lieu = new Lieu({ /* ... */ });
</script>
```

## Options
| option  | type  | required  | description  |
| :------------ | :------------ | :------------ | :------------ |
| languages  | object / json  | true  | List of languages and string translations  |
| initialLanguage  | string  | false  |  Selected default language. If not specified, it will be determined automatically. If you do not have any language, then the first one in the list of `languages` will be selected |
|  isDebug | boolean  | false  | If `true`, warns in the console about errors and not found translations in languages  |
| attributeName  | string  | false  | String localization attribute for HTML usage  |

## Hooks
| hook  | arguments  | description  |
| :------------ | :------------ | :------------ |
| onSetLang  | (newLang, oldLang)  | executed when using the `setLang()` method  |
| onGetLang  | () |  executed when using the `getLang()` method |

## Contributing
The author will be grateful to all developers for any suggestions to improve the plugin. Fork and submit pull requests. Thank you!
