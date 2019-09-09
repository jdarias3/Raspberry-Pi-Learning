# React on Raspberry Pi

## Installation

1. sudo apt-get install nodejs npm

To validate the version
nmp -v
node -v

To set a proxy for NPM, use the following command:

```$ npm config set https-proxy http://proxy.[Company Name].com:8080```

To simplify the App creation, install the the package *create-react-app*

```$ npm install -g create-react-app ```

**Note:** If you use VS Code as your editor, I suggest you, the following extensions extensions for React:

1. Simple React Snippet
2. Prettier - Code formatter

Prettier will reformat after you save your file, to do so, we need to perform an extra step:

1. Go to File > Preferences > Settings
2. On the search bar, type *formatOnSave* and mark this option.

**To Create a Project**

```$create-react-app <name>```

**Note:** The name of the App must be in lowercase

It will install a development server , webpack and babel to compile javascript

After instalation, to lunch the application use the command:

````npm start run```

## File Structure

node_module -> 3rd pary libraries
public -> public assests of our project
src -> js,css and component folder

React Re´pnsive Carousel
http://react-responsive-carousel.js.org/#install


We can use Bootswatch (it create styles base on bootstrap), put URL of the file in the ```/public/index.html```

```<link rel="stylesheet" href="https://bootswatch.com/4/superhero/bootstrap.min.css">```

On */src*, we can create a folder named *component* to save all the components in the same folder and keep our project organized.

