---
title: How To Improve Your Billing Form’s UX In One Day
slug: improve-billing-form-ux
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f01634d4-ae29-4dc3-adec-f9892b789676/4-halter-1.png'
date: 2017-03-22T17:58:53.000Z
author: margaritaklubochkina
summary: >-
  Improving your billing form can make the user experience much more intuitive and, as a result, ensure user convenience and increase confidence in your product. It’s an important part of web applications.
description: >-
  Improving your billing form can make the user experience much more intuitive and, as a result, ensure user convenience and increase confidence in your product. It’s an important part of web applications.
categories:
  - UX
  - Forms
  - E-Commerce
  - UX
  - Product Strategy
---
The checkout page is the last page a user visits before finally decide to complete a purchase on your website. It’s where window shoppers turn into paying customers. If you want to leave a good impression, you should provide **optimal usability of the billing form** and improve it wherever it is possible to.

In less than one day, you can add some simple and useful features to your project to make your billing form user-friendly and easy to fill in. A demo with all the functions covered below is available. You can find its code in the GitHub repository.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Reducing Abandoned Shopping Carts In E-Commerce](https://www.smashingmagazine.com/2014/10/reducing-abandoned-shopping-carts/)
*   [Form-Field Validation: The Errors-Only Approach](https://www.smashingmagazine.com/2012/06/form-field-validation-errors-only-approach/)
*   [Fundamental Guidelines Of E-Commerce Checkout Design](https://www.smashingmagazine.com/2011/04/fundamental-guidelines-of-e-commerce-checkout-design/)
*   [An Extensive Guide To Web Form Usability](https://www.smashingmagazine.com/2011/11/extensive-guide-web-form-usability/)

<p>Credit-card details are among the most commonly corrected fields in forms. Fortunately, nowadays almost every popular browser has an autofill feature, allowing the users to store their card data in the browser and to fill out form fields more quickly. Also, since iOS 8, mobile Safari users can scan their card’s information with the iPhone’s camera and fill in their card’s number, expiration date and name fields automatically. Autocomplete is simple, clear and built into HTML5, so we’ll add it to our form first.</p>

<p>Both autofill and card-scanning work only with forms that have special attributes: <code>autocomplete</code> for modern browsers (listed in the <a href="https://html.spec.whatwg.org/multipage/forms.html#inappropriate-for-the-control">HTML5 standard</a>) and <code>name</code> for browsers without HTML5 support.</p>

<p><strong>Note</strong>: <em>A demo with all the functions covered below <a href="https://billing-form.herokuapp.com/">is available</a>. You can find its code in the <a href="https://github.com/gretchenfitze/billing-form">GitHub repository</a></em>.</p>

<p>Credit cards have specific autofill attributes. For <code>autocomplete</code>:</p>

*   `cc-name`
*   `cc-number`
*   `cc-csc`
*   `cc-exp-month`
*   `cc-exp-year`
*   `cc-exp`
*   `cc-type`
*   `cc-csc`

For <code>name</code>:

*   `ccname`
*   `cardnumber`
*   `cvc`
*   `ccmonth`
*   `ccyear`
*   `expdate`
*   `card-type`
*   `cvc`

{{% feature-panel %}}

To use autofill, you should add the relevant <code>autocomplete</code> and <code>name</code> attributes for the input elements in your <code>index.html</code> file:

<div class="break-out">

<pre><code class="language-html">&lt;input type="text" id="card__input_number" class="card__input card__input_number" placeholder="XXXX XXXX XXXX XXXX" pattern="[0-9]{14,23}" required autofocus autocomplete="cc-number" name="cardnumber"&gt;
&lt;input type="text" id="card__input_month" class="card__input card__input_date card__input_month" placeholder="MM" pattern="[0-9]{1,2}" required autocomplete="cc-exp-month" name="ccmonth"&gt;
&lt;input type="text" id="card__input_year" class="card__input card__input_date card__input_year" placeholder="YYYY" pattern="[0-9]{2,4}" required autocomplete="cc-exp-year" name="ccyear"&gt;
&lt;input type="text" class="card__input card__input_cardholder" placeholder="CARDHOLDER NAME" required autocomplete="cc-name" name="ccname"&gt;
</code></pre></div>

Don’t forget to use <code>placeholder</code> in input fields to help users understand the required data formats. We can provide input validation with HTML5 attributes: <code>pattern</code> (based on JavaScript regular expressions) and <code>required</code>. For example, with <code>pattern="[0-9\s]{14,23}" required</code> attributes in a field, the user won’t be able to submit the form if the field is empty, has a non-numeric or non-space symbol, or is shorter than 14 symbols or longer than 23 symbols.

Once the user has saved their card data in the browser, we can see how it works:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b441704a-8695-4b6f-9275-d09a9b5abe42/1-autocomplete.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b441704a-8695-4b6f-9275-d09a9b5abe42/1-autocomplete.gif" alt="Chrome autocomplete sample." width="613" height="413" /></a><figcaption>Autocomplete sample in Google Chrome browser</figcaption></figure>

Notice that using one field for the expiration date (<code>MM/YYYY</code>) is not recommended because Safari requires separate month and year fields to autocomplete.

Of course, autocomplete and autofill attributes are widely used not only for billing forms but also for names, email and postal addresses and passwords. You can save the user time and make them even happier by correctly using these attributes in your forms.

Even though we now have autocomplete, Google Payments and Apple Wallet, many users still prefer to enter their credit-card details manually, and no one is safe from making a typo with a 16-digit number. Long numbers are hard to read, even more painful to write and almost impossible to verify.

{{% ad-panel-leaderboard %}}

To help users feel comfortable with their long card number, we can divide it into four-digit groups by adding the simple <a href="https://github.com/BankFacil/vanilla-masker">VanillaMasker</a> library by BankFacil to our project. Inputted data will be transformed to a masked string. So, we can add a custom pattern with spaces after every fourth digit of a card number, a two-digit pattern for the expiration month and a four-digit pattern for the expiration year. VanillaMasker can also verify data formats: If we have passed only “9” (the default number for the masker) to the ID, then all non-numeric characters will be deleted after input.

<pre><code class="language-bash">npm install vanilla-masker --save
</code></pre>

In our <code>index.js</code> file, let’s import the library and use it with one string for every field:

<pre><code class="language-javascript">import masker from 'vanilla-masker';

const cardNumber = document.getElementById('card__input_number');
const cardMonth = document.getElementById('card__input_month');
const cardYear = document.getElementById('card__input_year');

masker(cardNumber).maskPattern('9999 9999 9999 9999 99');
masker(cardMonth).maskPattern('99');
masker(cardYear).maskPattern('9999');
</code></pre>

Thus, the digits of the card number in our form will be separated, like on a real card:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ac07097-23b6-4024-8cbd-fedfb22d422e/2-masker.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ac07097-23b6-4024-8cbd-fedfb22d422e/2-masker.gif" alt="VanillaMasker example" width="613" height="413" /></a><figcaption>VanillaMasker in action</figcaption></figure>

The masker will erase characters with an incorrect value type or length, although our HTML validation will notify the user about invalid data only after the form has been submitted. But we can also check a card number’s correctness as it is being filled in. Did you know that all plastic credit-card numbers are generated according to the simple and effective Luhn algorithm? It was created in 1954 by Hans Peter Luhn and subsequently set as an international standard. We can include the Luhn algorithm to pre-validate the card number’s input field and warn the user about a typo.

To do this, we can use the tiny <a href="https://www.npmjs.com/package/fast-luhn">fast-luhn</a> npm package, adapted from <a href="https://gist.github.com/ShirtlessKirk/2134376">Shirtless Kirk’s gist</a>. We need to add it to our project’s dependencies:

<pre><code class="language-bash">npm install fast-luhn --save
</code></pre>

To use fast-luhn, we’ll import it in a module and just call <code>luhn(number)</code> on the input event to check whether the number is correct. For example, let’s add the <code>card__input_invalid</code> class to change the <code>outline</code> and field’s text <code>color</code> when the user has made an accidental error and a check has not been passed. Note that VanillaMasker adds a space after every four-digit group, so we need to convert the inputted value to a plain number without spaces using the <code>split</code> and <code>join</code> methods, before calling <code>lunh</code>.

The result is code that looks like this:

<div class="break-out">

<pre><code class="language-javascript">import luhn from 'fast-luhn';

const cardNumber = document.getElementById('card-number');

cardNumber.addEventListener('input', (event) =&gt; {
  const number = event.target.value;

  if (number.length &gt;= 14) {
    const isLuhnCheckPassed = luhn(number.split(' ').join(''));
    cardNumber.classList.toggle('card__input_invalid', !isLuhnCheckPassed);
    cardNumber.classList.toggle('card__input_valid', isLuhnCheckPassed);
  } else {
    cardNumber.classList.remove('card__input_invalid', 'card__input_valid');
  }
});
</code></pre></div>

To prevent <code>luhn</code> from being called while the user is typing, let’s call it only if the inputted number is as long as the minimum length with spaces (14 characters, including 12 digits) or longer, or else remove the <code>card__input_invalid</code> class.

Here are the validation examples in action:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ebbf599-28ea-448d-9bd5-5086a0cc374e/3-luhn.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ebbf599-28ea-448d-9bd5-5086a0cc374e/3-luhn.gif" alt="Fast-luhn example" width="613" height="413" /></a><figcaption>Validation example with fast-luhn</figcaption></figure>

The Luhn algorithm is also used for some discount card numbers, IMEI numbers, National Provider Identifier numbers in the US, and Social Insurance Numbers in Canada. So, this package isn’t limited to credit cards.

Many users want to check their card details with their own eyes, even if they know the form is being validated. But human beings perceive things in a way that makes comparison of differently styled numbers a little confusing. As we want the interface to be simple and intuitive, we can help users by showing a font that looks similar to the one they would find on a real card. Also, the font will make our card-like input form look more realistic and appropriate.

{{% ad-panel-leaderboard %}}

Several free credit-card fonts are available:

*   [Halter](https://www.dafont.com/halter.font?text=ssfrshgrsdeh), Apostrophic Labs
*   [Kredit](https://www.fontspring.com/fonts/typodermic/kredit), Typodermic Fonts
*   [Credit Card](https://www.k-type.com/fonts/credit-card/), K-Type (free for personal use)

We’ll use Halter. First, download the font, place it in the project’s folder, and create a CSS3 <code>@font-face</code> rule in <code>style.css</code>:

<pre><code class="language-css">@font-face {
  font-family: Halter;
  src: url(font/HALTER__.ttf);
}
</code></pre>

Then, simply add it to the <code>font-family</code> rule for the <code>.card-input</code> class:

<pre><code class="language-css">.card-input {
  color: #777;
  font-family: Halter, monospace;
}
</code></pre>

Don’t forget that if you input the CSS in a JavaScript file with the webpack bundle, you’ll need to add <code>file-loader</code>:

<pre><code class="language-bash">npm install file-loader --save
</code></pre>

And add <code>file-loader</code> for the font file types in <code>webpack.config.js</code>:

<pre><code class="language-javascript">module: {
   loaders: [
   {
     test: /\.(ttf|eot|svg|woff(2)?)(\?[a-z0-9=&amp;.]+)?$/,
     loader: 'file',
   }],
 },
</code></pre>

The result looks pretty good:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f01634d4-ae29-4dc3-adec-f9892b789676/4-halter-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f01634d4-ae29-4dc3-adec-f9892b789676/4-halter-1.png" alt="Halter example" width="612" height="412" /></a><figcaption>Halter font on the card form</figcaption></figure>

You can make it even fancier, if you like, with an embossed effect using a double <code>text-shadow</code> and a semi-transparency on the text’s <code>color</code>:

<pre><code class="language-css">.card-input {
  color: rgba(84,110,122,0.5);
  text-shadow: -0.75px -0.75px white, 0.75px 0.75px 0 black;
  font-family: Halter, monospace;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33c86bda-aac1-4635-9d58-e92822c0bb29/4-halter-2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33c86bda-aac1-4635-9d58-e92822c0bb29/4-halter-2.png" alt="Halter with double shadow example" width="612" height="412" /></a><figcaption>Halter font with <code>text-shadow</code></figcaption></figure>

Last but not least, you can pleasantly surprise customers by adding a coloring feature to the form. Every bank has its own brand color, which usually dominates that bank’s card. To make a billing form even more user-friendly, we can use this color and print the bank’s name above the form fields (corresponding to where it appears on a real card). This will also help the user to avoid making a typo in the number and to ensure they have picked the right card.

We can identify the bank of every user’s card by the first six digits, which contain the Issuer Identification Number (IIN) or Bank Identification Number (BIN). <a href="https://github.com/ramoona/banks-db">Banks DB</a> by Ramoona is a database that gets a bank’s name and brand color from this prefix. The author has set up a <a href="https://ramoona.github.io/banks-db-demo/">demo of Banks DB</a>.

This database is community-driven, so it doesn’t contain all of the world’s bank. If a user’s bank isn’t represented, the space for the bank’s name will be empty and the background will show the default color (<code>#fafafa</code>).

Banks DB assumes one of two ways of using it: with PostCSS or with CSS in JavaScript. We are using it with PostCSS. If you are new to PostCSS, this is a good reason to start using it. You can learn more about PostCSS in the <a href="https://github.com/postcss/postcss">official documentation</a> or in Drew Minns’ article “<a href="https://www.smashingmagazine.com/2015/12/introduction-to-postcss/">An Introduction to PostCSS</a>”.

We need to install the <a href="https://github.com/ramoona/postcss-banks-db">PostCSS Banks DB</a> plugin to set the CSS template for Banks DB and install the <a href="https://github.com/stephenway/postcss-contrast">PostCSS Contrast</a> plugin to improve the readability of the bank’s name:

<pre><code class="language-bash">npm install banks-db postcss-banks-db postcss-contrast --save
</code></pre>

After that, we’ll add these new plugins to our PostCSS process in accordance with the module bundler and the load configuration used in our project. For example, with Webpack and <a href="https://github.com/michael-ciniawsky/postcss-load-config">postcss-load-config</a>, simply add the new plugins to the <code>.postcssrc</code> file.

Then, in our <code>style.css</code> file, we need to add a new class rule template for Banks DB with the postcss-contrast plugin:

<pre><code class="language-css">@banks-db-template {
  .card_bank-%code% {
    background-color: %color%;
    color: contrast(%color%);
  }
}
</code></pre>

We could also set a long <code>transition</code> on the whole <code>.card</code> class to smoothly fade in and out the background and text color, so as not to startle users with an abrupt change:

<pre><code class="language-css">.card {
  …
  transition: background 0.6s, color 0.6s;
}
</code></pre>

Now, import Banks DB in <code>index.js</code>, and use it in the <code>input</code> event listener. If the BIN is represented in the database, we’ll add the class containing the bank’s name to the form in order to insert the name and change the form’s background.</p>

<div class="break-out">

<pre><code class="language-javascript">import banksDB from 'banks-db';

const billingForm = document.querySelector('.card');
const bankName = document.querySelector('.card__bank-name');
const cardNumber = document.getElementById('card__input_number');

cardNumber.addEventListener('input', (event) =&gt; {
  const number = event.target.value;
  const bank = banksDB(number);

  if (bank.code) {
    billingForm.classList.add(`card_bank-${(bank.code || 'other')}`);
    bankName.innerText = bank.country === 'ru' ? bank.localTitle : bank.engTitle;
  } else {
    billingForm.className = 'card';
    bankName.innerText = '';
  }
});
</code></pre></div>

If you use webpack, add json-loader for the <code>.json</code> file extension to webpack’s configuration in order to input the database in the bundle correctly.

Here is a working example of Banks DB:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b42b1d82-f5bc-4c3b-9dd8-205a819c5f51/5-db.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b42b1d82-f5bc-4c3b-9dd8-205a819c5f51/5-db.gif" alt="Banks DB example" width="613" height="413" /></a><figcaption>Form coloring with Banks DB</figcaption></figure>

In case you see no effect with your bank card, you can <a href="https://github.com/ramoona/banks-db#contributing">open an issue or add your bank to the database.</a>

## Conclusion

Improving your billing form can make the user experience much more intuitive and, as a result, ensure user convenience and increase confidence in your product. It’s an important part of web applications. We can improve it quickly and easily using these simple features:

*   suitable `autocomplete` and `name` attributes for autofilling,
*   `placeholder` attribute to inform the user of the input format,
*   `pattern` and `require` attributes to prevent incorrect submission of form,
*   VanillaMasker to separate card digits,
*   fast-luhn to verify the card number,
*   Halter font for easy comparison,
*   Banks DB for a nicer presentation of colors.

Note that only Banks DB requires a module bundler; you can use the others within the simple script. Adding all of this functionality to your checkout page would most likely take less than a day.

{{< signature "rb, al, il" >}}

