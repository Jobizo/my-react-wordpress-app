# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

Features

CRUD operation with WordPress REST API

Authentication with JWT ( Login Logout )

Accessing public and private routes

Handing WordPress REST API custom end points.

Creating Dashboard with React for CRUD operation.

Pagination

Installation


git checkout branchname

Run npm install

Add REST API ENDPOINTS WordPress Plugin
Clone the REST API ENDPOINTS plugin in your WordPress plugin directory.


Configure


Add your wordPress siteUrl in src/client-config.js

const clientConfig = {
	siteUrl: 'http://localhost:8888/wordpress'
};

export default clientConfig;

Branches


1. login-with-jwt-wordpress-plugin

A React App where you can login using the endpoint provided by JWT Authentication for WP-API WordPress Plugin. So you need to have this plugin installed on WordPress. The plugin's endpoint returns the user object and a jwt-token on success, which we can then store in localstorage and login the user on front React Application

Steps
You need to install and activate JWT Authentication for WP REST API plugin on you WordPress site
Then you need to configure it by adding these:
i. Add the last three lines in your WordPress .htaccess file as shown:

# BEGIN WordPress

   <IfModule mod_rewrite.c>
	
   RewriteEngine On
	
   RewriteBase /wordpress/
	
   RewriteRule ^index\.php$ - [L]
	
   RewriteCond %{REQUEST_FILENAME} !-f
	
   RewriteCond %{REQUEST_FILENAME} !-d
	
   RewriteRule . /wordpress/index.php [L]
   
   
   RewriteCond %{HTTP:Authorization} ^(.*)
	
   RewriteRule ^(.*) - [E=HTTP_AUTHORIZATION:%1]
	
   SetEnvIf Authorization "(.*)" HTTP_AUTHORIZATION=$1
	
   </IfModule>
   
   
   
ii. Add the following in your wp-config.php Wordpress file. You can choose your own secret key.

define('JWT_AUTH_SECRET_KEY', '&BZd]N-ghz|hbH`=%~a5z(`mR=n%7#8-Iz@KoqtDhQ6(8h$og%-IbI#>N*T`s9Dg');

define('JWT_AUTH_CORS_ENABLE', true);

iii. Now you can make a request to /wp-json/jwt-auth/v1/token REST API provided by the plugin. You need to pass username and password and it returns a user object and

token . You can save the token in localstorage and send it in the headers of your protected route requests ( e.g. Create Post /wp-json/wp/v2/posts )

iiv. So whenever you send a request to WordPress REST API for your protected routes, you send the token received in the headers of your request


{
	'Accept': 'application/json',
	'Content-Type': 'application/json',
	'Authorization': `Bearer putTokenReceivedHere`
}

This repo also demonstrates how to create posts in React Application by sending request to protected endpoints ( passing the token in the header )

2. jwt-verify-with-node

A React(front end) + Node(back end) application. It uses jwt.sign() ( from jwtwebtoken npm package ) to generate a token using the username and password sent from front end( React ) and returns it as a response, which we then store in localstorage to login the user. This token received by frond end, will be sent with all further request for protected routes, which will then be verified in node route using jwt.verify() Besides generating the token, the end point in node also accesses the WordPress rest api to confirm the credentials and returns the user object or errors if any.

It also has functionality to create post where we make a request from front end along with token( React ) to a node end point. The node endpoint verifies the token and then makes a request to WordPress REST API endpoint to create the post and then returns the new post id, or error if any.

Commands

Branch master and build-app-for-heroku
start Runs node server for development ( in watch mode ). The server.js sends all front end route request to index.html and then all front end route requests is handled by reach router. Branch jwt-verify-with-node and login-with-jwt-wordpress-plugin dev Runs webpack dev server for development ( in watch mode )
Common prod Runs webpack in production mode

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

