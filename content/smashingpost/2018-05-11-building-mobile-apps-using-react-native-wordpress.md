---
title: 'Building Mobile Apps Using React Native And WordPress'
slug: building-mobile-apps-using-react-native-wordpress
author: muhammad-muhsin
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43edaf0f-c035-4979-b7e4-ba91839717e3/3-woocommerce-sample-800w.png
date: 2018-05-11T15:15:56+02:00
summary: >-
  WordPress can work as an excellent back-end platform for your next native app, especially if it is content-driven or an online shop. In this article, you will learn the foundations for building mobile apps with React Native and WordPress.
description: >-
  WordPress can work as an excellent back-end platform for your next native app, especially if it is content-driven or an online shop. In this article, you will learn the foundations for building mobile apps with React Native and WordPress.
categories:
  - WordPress
  - Apps
  - Mobile
  - React
  - Native
---
<p>As web developers, you might have thought that mobile app development calls for a fresh learning curve with another programming language. Perhaps Java and Swift need to be added to your skill set to hit the ground running with both iOS and Android, and that might bog you down.</p>

<p>But this article has you in for a surprise! We will look at building an e-commerce application for iOS and Android using the WooCommerce platform as our backend. This would be an ideal starting point for anyone willing to get into native cross-platform development.</p>

## A Brief History Of Cross-Platform Development

<p>It’s 2011, and we see the beginning of hybrid mobile app development. Frameworks like Apache Cordova, PhoneGap, and Ionic Framework slowly emerge. Everything looks good, and web developers are eagerly coding away mobile apps with their existing knowledge.</p>

<p>However, mobile apps still looked like mobile versions of websites. No native designs like Android’s material design or iOS’s flat look. Navigation worked similar to the web and transitions were not buttery smooth. Users were not satisfied with apps built using the hybrid approach and dreamt of the native experience.</p>

<p>Fast forward to March 2015, and React Native appears on the scene. Developers are able to build truly native cross-platform applications using React, a favorite JavaScript library for many developers. They are now easily able to learn a small library on top of what they know with JavaScript. With this knowledge, developers are now targeting the web, iOS and Android.</p>

{{% feature-panel %}}

<p>Furthermore, changes done to the code during development are loaded onto the testing devices almost instantly! This used to take several minutes when we had native development through other approaches. Developers are able to enjoy the instant feedback they used to love with web development.</p>

<p>React developers are more than happy to be able to use existing patterns they have followed into a new platform altogether. In fact, they are targeting two more platforms with what they already know very well.</p>

<p>This is all good for front-end development. But <strong>what choices do we have for back-end technology?</strong> Do we still have to learn a new language or framework?</p>

## The WordPress REST API

<p>In late 2016, WordPress released the much awaited REST API to its core, and opened the doors for solutions with decoupled backends.</p>

<p>So, if you already have a WordPress and WooCommerce website and wish to retain exactly the same offerings and user profiles across your website and native app, this article is for you!</p>

## Assumptions Made In This Article

<p>I will walk you through using your WordPress skill to build a mobile app with a WooCommerce store using React Native. The article assumes:</p>

<ul>
<li>You are familiar with the different WordPress <a href="https://codex.wordpress.org/WordPress_API%27s">APIs</a>, at least at a beginner level.</li>
<li>You are familiar with the basics of React.</li>
<li>You have a WordPress development server ready. I use Ubuntu with Apache.</li>
<li>You have an Android or an iOS device to test with Expo.</li>
</ul>

## What We Will Build In This Tutorial

<p>The project we are going to build through this article is a fashion store app. The app will have the following functionalities:</p>

<ul>
<li>Shop page listing all products,</li>
<li>Single product page with details of the selected item,</li>
<li>‘Add to cart’ feature,</li>
<li>‘Show items in cart’ feature,</li>
<li>‘Remove item from cart’ feature.</li>
</ul>

<p>This article aims to inspire you to use this project as a starting point to build complex mobile apps using React Native.</p>

<p><strong>Note</strong>: <em>For the full application, you can <a href="https://github.com/laccadive-io/react-native-woocommerce-store">visit my project on Github</a> and clone it</em>.</p>

## Getting Started With Our Project

<p>We will begin building the app as per the official React Native documentation. Having installed Node on your development environment, open up the command prompt and type in the following command to install the Create React Native App globally.</p>

<pre><code class="language-markup">npm install -g create-react-native-app</code></pre>

<p>Next, we can create our project</p>

<pre><code class="language-markup">create-react-native-app react-native-woocommerce-store</code></pre>

<p>This will create a new React Native project which we can test with Expo.</p>

<p>Next, we will need to install the Expo app on our mobile device which we want to test. It is available for both <a href="https://itunes.apple.com/us/app/expo-client/id982107779?mt=8">iOS</a> and <a href="https://play.google.com/store/apps/details?id=host.exp.exponent">Android</a>.</p>

<p>On having installed the Expo app, we can run npm start on our development machine.</p>

<pre><code class="language-markup">cd react-native-woocommerce-store

npm start</code></pre>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef7a2ced-8a09-4a50-a92f-a98097e4492f/1-react-native-expo-cmd.png" sizes="80vw" caption="Starting a React Native project through the command line via Expo. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef7a2ced-8a09-4a50-a92f-a98097e4492f/1-react-native-expo-cmd.png'>Large preview</a>)" alt="" >}}

<p>After that, you can scan the QR code through the Expo app or enter the given URL in the app’s search bar. This will run the basic ‘Hello World’ app in the mobile. We can now edit App.js to make instant changes to the app running on the phone.</p>

<p>Alternatively, you can run the app on an emulator. But for brevity and accuracy, we will cover running it on an actual device.</p>

<p>Next, let’s install all the required packages for the app using this command:</p>

<div class="break-out">

<pre><code class="language-markup">npm install -s axios react-native-htmlview react-navigation react-redux redux redux-thunk</code></pre></div>

## Setting Up A WordPress Site

<p>Since this article is about creating a React Native app, we will not go into details about creating a WordPress site. Please refer to <a href="https://linode.com/docs/websites/cms/install-wordpress-on-ubuntu-16-04/">this article</a> on how to install WordPress on Ubuntu. As WooCommerce REST API requires HTTPS, please make sure it is set up using Let’s Encrypt. Please refer to <a href="https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-16-04">this article</a> for a how-to guide.</p>

<p>We are not creating a WordPress installation on localhost since we will be running the app on a mobile device, and also since HTTPS is needed.</p>

<p>Once WordPress and HTTPS are successfully set up, we can install the <a href="https://wordpress.org/plugins/woocommerce/">WooCommerce plugin</a> on the site.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ae419f-2c46-4a18-8d83-ade1857aba8a/2-woocommerce-plugin.png" sizes="100vw" caption="Installing the WooCommerce plugin to our WordPress installation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ae419f-2c46-4a18-8d83-ade1857aba8a/2-woocommerce-plugin.png'>Large preview</a>)" alt="" >}}

<p>After installing and activating the plugin, continue with the WooCommerce store setup by following the wizard. After the wizard is complete, click on ‘Return to dashboard.’ </p>

<p>You will be greeted by another prompt.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c1623c5-e377-40ad-b694-59cf66f39f1f/3-woocommerce-sample.png" sizes="100vw" caption="Adding example products to WooCommerce. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c1623c5-e377-40ad-b694-59cf66f39f1f/3-woocommerce-sample.png'>Large preview</a>)" alt="" >}}

<p>Click on ‘Let’s go‘ to 'Add example products'. This will save us the time to create our own products to display in the app.</p>

## Constants File

<p>To load our store’s products from the WooCommerce REST API, we need the relevant keys in place inside our app. For this purpose, we can have a <code>constans.js</code> file.</p>

<p>First create a folder called ‘src’ and create subfolders inside as follows:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd24550-2a61-411a-b411-8a5bc22c053b/4-folder-structure-wide.png" sizes="70vw" caption="Create the file ‘Constants.js’ within the constans folder. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd24550-2a61-411a-b411-8a5bc22c053b/4-folder-structure-wide.png'>Large preview</a>)" alt="" >}}

<p>Now, let’s generate the keys for WooCommerce. In the WordPress dashboard, navigate to WooCommerce&nbsp;&rarr; Settings&nbsp;&rarr; API&nbsp;&rarr; Keys/Apps and click on ‘Add Key.’</p>

<p>Next create a Read Only key with name React Native. Copy over the Consumer Key and Consumer Secret to the <code>constants.js</code> file as follows:</p>

<pre><code class="language-javascript">const Constants = {
   URL: {
wc: 'https://woocommerce-store.on-its-way.com/wp-json/wc/v2/'
   },
   Keys: {
ConsumerKey: 'CONSUMER_KEY_HERE',
ConsumerSecret: 'CONSUMER_SECRET_HERE'
   }
}
export default Constants;
</code></pre>

## Starting With React Navigation

<p><a href="https://reactnavigation.org">React Navigation</a> is a community solution to navigating between the different screens and is a standalone library. It allows developers to set up the screens of the React Native app with just a few lines of code.</p>

<p>There are different navigation methods within React Navigation:</p>

<ul>
<li>Stack,</li>
<li>Switch,</li>
<li>Tabs,</li>
<li>Drawer,</li>
<li>and more.</li>
</ul>

<p>For our Application we will use a combination of <code>StackNavigation</code> and <code>DrawerNavigation</code> to navigate between the different screens. <code>StackNavigation</code> is similar to how browser history works on the web. We are using this since it provides an interface for the header and the header navigation icons. It has push and pop similar to stacks in data structures. Push means we add a new screen to the top of the Navigation Stack. Pop removes a screen from the stack.</p>

<p>The code shows that the <code>StackNavigation</code>, in fact, houses the <code>DrawerNavigation</code> within itself. It also takes properties for the header style and header buttons. We are placing the navigation drawer button to the left and the shopping cart button to the right. The drawer button switches the drawer on and off whereas the cart button takes the user to the shopping cart screen.</p>

<pre><code class="language-javascript">const StackNavigation = StackNavigator({
 DrawerNavigation: { screen: DrawerNavigation }
}, {
   headerMode: 'float',
   navigationOptions: ({ navigation, screenProps }) => ({
     headerStyle: { backgroundColor: '#4C3E54' },
     headerTintColor: 'white',
     headerLeft: drawerButton(navigation),
     headerRight: cartButton(navigation, screenProps)
   })
 });

const drawerButton = (navigation) => (
 &lt;Text
   style={{ padding: 15, color: 'white' }}
   onPress={() => {
     if (navigation.state.index === 0) {
       navigation.navigate('DrawerOpen')
     } else {
       navigation.navigate('DrawerClose')
     }
   }
   }><Ionicons name="ios-menu" size={30} /&gt;&lt;/Text&gt;
);

const cartButton = (navigation, screenProps) => (
 &lt;Text style={{ padding: 15, color: 'white' }}
   onPress={() => { navigation.navigate('CartPage') }}
 &gt;
   &lt;EvilIcons name="cart" size={30} /&gt;
   {screenProps.cartCount}
 &lt;/Text&gt;
);
</code></pre>

<p><code>DrawerNavigation</code> on the other hands provides for the side drawer which will allow us to navigate between Home, Shop, and Cart. The <code>DrawerNavigator</code> lists the different screens that the user can visit, namely Home page, Products page, Product page, and Cart page. It also has a property which will take the Drawer container: the sliding menu which opens up when clicking the hamburger menu.</p>

<pre><code class="language-javascript">const DrawerNavigation = DrawerNavigator({
 Home: {
   screen: HomePage,
   navigationOptions: {
     title: "RN WC Store"
   }
 },
 Products: {
   screen: Products,
   navigationOptions: {
     title: "Shop"
   }
 },
 Product: {
   screen: Product,
   navigationOptions: ({ navigation }) => ({
     title: navigation.state.params.product.name
   }),
 },
 CartPage: {
   screen: CartPage,
   navigationOptions: {
     title: "Cart"
   }
 }
}, {
   contentComponent: DrawerContainer
 });
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4e13814-f0e4-4401-9c46-f791ab472835/rn-wc-store-home-screen-drawer.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4e13814-f0e4-4401-9c46-f791ab472835/rn-wc-store-home-screen-drawer.png" sizes="100vw" caption="Left: The Home page (<code>homepage.js</code>). Right: The open drawer (DrawerContainer.js)." alt="#" >}}

## Injecting The Redux Store To App.js

<p>Since we are using Redux in this app, we have to inject the store into our app. We do this with the help of the <code>Provider</code> component.</p>

<pre><code class="language-javascript">const store = configureStore();

class App extends React.Component {
 render() {
   return (
     &lt;Provider store={store}&gt;    
       &lt;ConnectedApp /&gt;    
     &lt;/Provider&gt;    
   )
 }
}
</code></pre>

<p>We will then have a <code>ConnectedApp</code> component so that we can have the cart count in the header.</p>

<pre><code class="language-javascript">class CA extends React.Component {
 render() {
   const cart = {
     cartCount: this.props.cart.length
   }
   return (
     &lt;StackNavigation screenProps={cart} /&gt;
   );
 }
}

function mapStateToProps(state) {
 return {
   cart: state.cart
 };
}

const ConnectedApp = connect(mapStateToProps, null)(CA);
</code></pre>

## Redux Store, Actions, And Reducers

<p>In Redux, we have <a href="https://redux.js.org/basics">three different parts</a>:</p>

<ol>
<li><strong>Store</strong><br />Holds the whole state of your entire application. The only way to change state is to dispatch an action to it.</li>
<li><strong>Actions</strong><br />A plain object that represents an intention to change the state.</li>
<li><strong>Reducers</strong><br />A function that accepts a state and an action type and returns a new state.</li>
</ol>

<p>These three components of Redux help us achieve a predictable state for the entire app. For simplicity, we will look at how the products are fetched and saved in the Redux store.</p>

<p>First of all, let’s look at the code for creating the store:</p>

<pre><code class="language-javascript">let middleware = [thunk];

export default function configureStore() {
    return createStore(
        RootReducer,
        applyMiddleware(...middleware)
    );
}
</code></pre>

<p>Next, the products action is responsible for fetching the products from the remote website.</p>

<pre><code class="language-javascript">export function getProducts() {
   return (dispatch) => {
       const url = `${Constants.URL.wc}products?per_page=100&consumer_key=${Constants.Keys.ConsumerKey}&consumer_secret=${Constants.Keys.ConsumerSecret}`

       return axios.get(url).then(response => {
           dispatch({
               type: types.GET_PRODUCTS_SUCCESS,
               products: response.data
           }
       )}).catch(err => {
           console.log(err.error);
       })
   };
}
</code></pre>

<p>The products reducer is responsible for returning the payload of data and whether it needs to be modified.</p>

<pre><code class="language-javascript">export default function (state = InitialState.products, action) {
    switch (action.type) {
        case types.GET_PRODUCTS_SUCCESS:
            return action.products;
        default:
            return state;
    }
}
</code></pre>

## Displaying The WooCommerce Shop

<p>The <code>products.js</code> file is our Shop page. It basically displays the list of products from WooCommerce.</p>

<div class="break-out">

<pre><code class="language-javascript">class ProductsList extends Component {

 componentDidMount() {
   this.props.ProductAction.getProducts(); 
 }

 _keyExtractor = (item, index) => item.id;

 render() {
   const { navigate } = this.props.navigation;
   const Items = (
     &lt;FlatList contentContainerStyle={styles.list} numColumns={2}
       data={this.props.products || []} 
       keyExtractor={this._keyExtractor}
       renderItem={
         ({ item }) => (
           &lt;TouchableHighlight style={{ width: '50%' }} onPress={() => navigate("Product", { product: item })} underlayColor="white"&gt;
             &lt;View style={styles.view} &gt;
               &lt;Image style={styles.image} source={{ uri: item.images[0].src }} /&gt;
               &lt;Text style={styles.text}>{item.name}&lt;/Text&gt;
             &lt;/View&gt;
           &lt;/TouchableHighlight&gt;
         )
       }
     /&gt;
   );
   return (
     &lt;ScrollView&gt;
       {this.props.products.length ? Items :
         &lt;View style={{ alignItems: 'center', justifyContent: 'center' }}&gt;
           &lt;Image style={styles.loader} source={LoadingAnimation} /&gt;
         &lt;/View&gt;
       }
     &lt;/ScrollView&gt;
   );
 }
}
</code></pre></div>

<p><code>this.props.ProductAction.getProducts()</code> and <code>this.props.products</code> are possible because of <code>mapStateToProps</code> and <code>mapDispatchToProps</code>.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df6fa3f1-883d-4624-ad85-f96fbd6369a6/7-products-list-wide.png" sizes="70vw" caption="Products listing screen. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/198701a8-a845-41a2-bbc4-9639be7d8f04/7-products-list.png'>Large preview</a>)" alt="" >}}

## <code>mapStateToProps</code> and <code>mapDispatchToProps</code>

<p>State is the Redux store and Dispatch is the actions we fire. Both of these will be exposed as props in the component.</p>

<div class="break-out">

<pre><code class="language-javascript">function mapStateToProps(state) {
 return {
   products: state.products
 };
}
function mapDispatchToProps(dispatch) {
 return {
   ProductAction: bindActionCreators(ProductAction, dispatch)
 };
}
export default connect(mapStateToProps, mapDispatchToProps)(ProductsList);
</code></pre></div>

## Styles

<p>In React, Native styles are generally defined on the same page. It’s similar to CSS, but we use <code>camelCase</code> properties instead of hyphenated properties.</p>

<pre><code class="language-javascript">const styles = StyleSheet.create({
 list: {
   flexDirection: 'column'
 },
 view: {
   padding: 10
 },
 loader: {
   width: 200,
   height: 200,
   alignItems: 'center',
   justifyContent: 'center',
 },
 image: {
   width: 150,
   height: 150
 },
 text: {
   textAlign: 'center',
   fontSize: 20,
   padding: 5
 }
});
</code></pre>

## Single Product Page

<p>This page contains details of a selected product. It shows the user the name, price, and description of the product. It also has the ‘Add to cart’ function.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/103ad787-9ef4-480f-9ac7-a73f42acaa8b/8-single-product-wide.png" sizes="70vw" caption="Single product page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ade3fbcf-7b8e-4307-91fc-c2a14f150b1c/8-single-product.png'>Large preview</a>)" alt="" >}}

## Cart Page

<p>This screen shows the list of items in the cart. The action has the functions <code>getCart</code>, <code>addToCart</code>, and <code>removeFromCart</code>. The reducer handles the actions likewise. Identification of actions is done through actionTypes &mdash; constants which describe the action that are stored in a separate file.</p>

<div class="break-out">

<pre><code class="language-markup">export const GET_PRODUCTS_SUCCESS = 'GET_PRODUCTS_SUCCESS'
export const GET_PRODUCTS_FAILED = 'GET_PRODUCTS_FAILED';

export const GET_CART_SUCCESS = 'GET_CART_SUCCESS';
export const ADD_TO_CART_SUCCESS = 'ADD_TO_CART_SUCCESS';
export const REMOVE_FROM_CART_SUCCESS = 'REMOVE_FROM_CART_SUCCESS';
</code></pre></div>

<p>This is the code for the <code>CartPage</code> component:</p>

<div class="break-out">

<pre><code class="language-javascript">class CartPage extends React.Component {

 componentDidMount() {
   this.props.CartAction.getCart();
 }

 _keyExtractor = (item, index) => item.id;

 removeItem(item) {
   this.props.CartAction.removeFromCart(item);
 }

 render() {
   const { cart } = this.props;
   console.log('render cart', cart)

   if (cart && cart.length > 0) {
     const Items = &lt;FlatList contentContainerStyle={styles.list}
       data={cart}
       keyExtractor={this._keyExtractor}
       renderItem={({ item }) =>
         &lt;View style={styles.lineItem} &gt;
           &lt;Image style={styles.image} source={{ uri: item.image }} /&gt;
           &lt;Text style={styles.text}&gt;{item.name}&lt;/Text&gt;
           &lt;Text style={styles.text}&gt;{item.quantity}&lt;/Text&gt;
           &lt;TouchableOpacity style={{ marginLeft: 'auto' }} onPress={() => this.removeItem(item)}&gt;&lt;Entypo name="cross" size={30} /&gt;&lt;/TouchableOpacity&gt;
         &lt;/View&gt;
       }
     /&gt;;
     return (
       &lt;View style={styles.container}&gt;
         {Items}
       &lt;/View&gt;
     )
   } else {
     return (
       &lt;View style={styles.container}&gt;
         &lt;Text>Cart is empty!&lt;/Text&gt;
       &lt;/View&gt;
     )
   }
 }
}
</code></pre></div>

<p>As you can see, we are using a <code>FlatList</code> to iterate through the cart items. It takes in an array and creates a list of items to be displayed on the screen.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09907ef4-3173-4504-8c2c-f58310e9d06c/example-full-empty-cart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09907ef4-3173-4504-8c2c-f58310e9d06c/example-full-empty-cart.png" sizes="100vw" caption="Left: The cart page when it has items in it. Right: The cart page when it is empty." alt="#" >}}

## Conclusion

<p>You can configure information about the app such as name and icon in the <code>app.json</code> file. The app can be published after npm installing exp.</p>

<p>To sum up:</p>

<ul>
<li>We now have a decent e-commerce application with React Native;</li>
<li>Expo can be used to run the project on a smartphone;</li>
<li>Existing backend technologies such as WordPress can be used;</li>
<li>Redux can be used for managing the state of the entire app;</li>
<li>Web developers, especially React developers can leverage this knowledge to build bigger apps.</li>
</ul>

<p>For the full application, you can <a href="https://github.com/laccadive-io/react-native-woocommerce-store">visit my project on Github</a> and clone it. Feel free to fork it and improve it further. As an exercise, you can continue building more features into the project such as:</p>

<ul>
<li>Checkout page,</li>
<li>Authentication,</li>
<li>Storing the cart data in AsyncStorage so that closing the app does not clear the cart.</li>
</ul>

{{< signature "da, lf, ra, yk, il" >}}

