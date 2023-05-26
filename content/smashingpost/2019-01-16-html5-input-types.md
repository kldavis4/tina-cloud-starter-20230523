---
title: 'HTML5 Input Types: Where Are They Now?'
slug: html5-input-types
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2941eeca-2d65-4699-bc70-6a40fea29e29/html5-input-types-custom-keyboards.png
date: 2019-01-16T14:30:11+01:00
summary: >-
  HTML5 introduced thirteen new types of form input, adding significantly to the number of different fields web designers and developers could add to our forms. These new types all require browsers to support them, and take-up has been slower than some of us would have liked. What is the state of those field types in 2019? Which can we use, and which should still be avoided?
description: >-
  HTML5 introduced thirteen new types of form input, adding significantly to the number of different fields web designers and developers could add to our forms. But what is the state of those field types in 2019? Let’s find out.
categories:
  - HTML5
  - Browsers
---
One of the stand-out headline features of HTML5 for many designers and developers was the addition of a number of new types of form input that could be used. For years, we’d been confined to using single-line text inputs (`type="text"`) and laying on JavaScript and user instructions to try an accurately capture valid data of different types through that one unsophisticated field.

HTML5 brought with it new values of the `type` attribute that enabled us to be much more specific about the types of data we needed to capture through the field, with the promise being that the browser would then provide the interface and validation required to coerce the user into completing the field accurately.

From URLs to emails, and from search fields to dates, the hope was that instead of needing to write cumbersome JavaScript to try and validate those fields, we could just leave it to the browser to do that hard work for us. What’s more, by adding what it knows about the user’s context (type of device, type of interaction, timezones, and so on) the browser would be able to do a much better job of tailoring the interface to meet the user’s needs that we ever could as page authors.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/08/ux-html5-mobile-form-part-2/">UX And HTML5: Let’s Help Users Fill In Your Mobile Form</a></em></p>

Having new items in a spec is one thing, but it doesn’t really mean too much unless the browsers our audience are using support those features. These new values of the `type` attribute had the big advantage of falling back to `type="text"` if the browser had no support, but this may have also come at the cost of removing the browsers makers' imperative when it came to implementing those new types in their products.

It’s the start of 2019, and HTML5 has been the current version of HTML now for more than four years. Which of those new types have been implemented, which can we use, and are there any we should be avoiding?

1.	[Search Fields](#a1)
2.	[Telephone Number Fields](#a2)
3.	[URL Fields](#a3)
4.	[Email Fields](#a4)
5.	[Number Fields](#a5)
6.	[Range Fields](#a6)
7.	[Color Fields](#a7)
8.	[Date Fields](#a8)

{{% feature-panel %}}

## <a href="#" name="a1" id="a1"></a>1. Search Fields

The `type="search"` input is intended to be used for search fields. Functionally, these are very the same as basic text fields, but having a dedicated type enables the browser to apply different styling. This is particularly useful if the user’s operating system has a set style for search fields, as this enables the browser to style the search fields on web pages to match.

The specification states that the difference between `search` and `text` is purely stylistic, so it may be best to avoid this if you intend to restyle the field with CSS anyway. There appears to be no semantic advantage to its use.

<p class="ciu_embed" data-feature="input-search" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-search">Can I Use input-search?</a> Data on support for the input-search feature across the major browsers from caniuse.com.</p>

### Recommendation

Use `type="search"` if you intend to leave the styling of the search field up to the browser.

## <a href="#" name="a2" id="a2"></a>2. Telephone Number Fields

The `type="tel"` input is used for entering telephone numbers. These are like the unique usernames used by Whatsapp. If you’re unsure, ask your grandparents.

Internationally, telephone numbers take on lots of different formats, for both technical and localization reasons. Due to this, the `tel` input doesn’t attempt to validate the format of a phone number. You can make use of the associated validation tools such as the `pattern` attribute on the tag, or the `setCustomValidity()` JavaScript method to enforce a format if required.

On desktop browsers, the use of telephone fields seems to have little impact. On devices with virtual keyboards, however, they can be really useful. For example, on iOS, focusing input on a telephone field brings up a numeric keypad ready for keying in a number. In addition, the device’s autocomplete mechanisms kick in and suggest phone numbers that can be autofilled with a single tap.

<p class="ciu_embed" data-feature="input-email-tel-url" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-email-tel-url">Can I Use input-email-tel-url?</a> Data on support for the input-email-tel-url feature across the major browsers from caniuse.com.</p>

### Recommendation

Use `type="tel"` for any phone number fields. It’s very useful where implemented, and comes at no cost when it’s not.

## <a href="#" name="a3" id="a3"></a>3. URL Fields

The `type="url"` field can be used for capturing URLs. You might use this when asking a user to input their website address for a business directory, for example. The curious thing about the URL field is that it takes only full, _absolute_ URLs. There’s no option to be able to capture just a domain name, or just a path, for example. This does restrict its usefulness in some respects, as I imagine CMS and web app developers would have found lots of uses for a field that accepts and validates relative paths.

While this would be a valid absolute URL:

<pre><code class="language-html">https://twitter.com/drewm
</code></pre>

Both of these would not pass the field’s validation:

<div class="break-out">

<pre><code class="language-html">smashingmagazine.com
/2019/01/css-multiple-column-layout-multicol/
</code></pre></div>

It feels like a missed opportunity that different parts of a URL cannot be specified, but that’s what we have. Browser support is across the board pretty great, with virtual keyboard devices offering some customization for URL entry. iOS customizes its keyboard with `.`, `/` and an autocomplete button for common TLDs such as `.com` and for my locale, `.co.uk`. This is a good example of the browser being able to offer more intelligent choices than we can as web developers.

<p class="ciu_embed" data-feature="input-email-tel-url" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-email-tel-url">Can I Use input-email-tel-url?</a> Data on support for the input-email-tel-url feature across the major browsers from caniuse.com.</p>

### Recommendation

Use `type="url"` whenever you need to collect a full, absolute URL. Browser support is great, but remember that it’s no good for individual URL components.

## <a href="#" name="a4" id="a4"></a>4. Email Fields

Possibly one of the most commonly used of the newer options is `type="email"` for email addresses. Much like we’ve seen with telephone numbers and URLs, devices with virtual keyboards customize the keys (to include things like `@` buttons) and enable autofill from their contacts database.

Desktop browsers make use of this too, with Safari on macOS also enabling autofill for email fields, based on data in the system Contacts app.

{{% ad-panel-leaderboard %}}

Email addresses often seem like they follow a very simple format, but the variations actually make them quite complex. A naive attempt to validate email addresses can result in a perfectly good address being marked as invalid, so it’s great to be able to lean on the browser’s more sophisticated and well-tested validation methods to check the format.

Usefully, the `multiple` attribute can be added to email fields to collect a list of email addresses. In this case, each email address in the list is individually validated.

<pre><code class="language-html">&lt;input type="email" multiple&gt;
</code></pre>

<p class="ciu_embed" data-feature="input-email-tel-url" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-email-tel-url">Can I Use input-email-tel-url?</a> Data on support for the input-email-tel-url feature across the major browsers from caniuse.com.</p>

### Recommendation

Use `type="email"` for email address fields whenever possible.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2941eeca-2d65-4699-bc70-6a40fea29e29/html5-input-types-custom-keyboards.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2941eeca-2d65-4699-bc70-6a40fea29e29/html5-input-types-custom-keyboards.png" sizes="100vw" caption="Safari on iOS shows custom keyboards for telephone, email and number fields, amongst others. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2941eeca-2d65-4699-bc70-6a40fea29e29/html5-input-types-custom-keyboards.png'>Large preview</a>)" alt="A combined screenshot showing the three custom keyboards offered by Safari on iOS for telephone, email and number field types." >}}

## <a href="#" name="a5" id="a5"></a>5. Number Fields 

The `type="number"` field is designed for numerical values, and has some very useful attributes along with it in the shape of `min`, `max` and `step`. A valid value for a number field must be a floating point number between any minimum and maximum value specified by the `min` and `max` attributes. 

If `step` is set, then a valid value is divisible by the step value.

<pre><code class="language-html">&lt;input type="number" min="10" max="30" step="5"&gt;
</code></pre>

Valid input for the above field would be `10`, `15`, `20`, `25` and `30`, with any other value being rejected.

Browser support is broad, again with virtual keyboards often defaulting to a numeric input mode for keying in values.

Some desktop browsers (including Chrome, Firefox and Safari, but not Edge) add toggle buttons for nudging the values up and down by the value of `step`, or if no step is specified, the default step appears to be `1` in each implementation.

<p class="ciu_embed" data-feature="input-number" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-number">Can I Use input-number?</a> Data on support for the input-number feature across the major browsers from caniuse.com.</p>

### Recommendation

Use `type="number"` for any floating point numbers, as it’s widely supported and can help prevent accidental input.

## <a href="#" name="a6" id="a6"></a>6. Range Fields

Less obvious in use that some of the other types, `type="range"` can be thought of as being an alternative for `type="number"` where the user doesn’t care about the exact value.

Range fields take, and will often use, the same `min`, `max` and `step` attributes as number fields, and browsers almost universally display this as a graphical slider. The user doesn’t necessarily get to see the exact value they’re setting.

Range fields might be useful for those sorts of questions on forms like "How likely are you to recommend this to a friend?" with "Likely" at one end and "Unlikely" at the other. The user could slide the slider to wherever they think represents their opinion, and under the hood that gets submitted as a numerical value that you can store and process.

Browser support is good, although the appearance varies between implementations.

<p class="ciu_embed" data-feature="input-range" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-range">Can I Use input-range?</a> Data on support for the input-range feature across the major browsers from caniuse.com.</p>

### Recommendation

The uses for `type="range"` might be a bit niche, but support is good and the slider provides a user-friendly input method where appropriate.

## <a href="#" name="a7" id="a7"></a>7. Color Fields

The `type="color"` field is design for capturing RGB colors in hexadecimal notation, such as `#aabbcc`. The HTML specification calls this a "color well control", with the intention that the browser should provide a user-friendly color picker of some sort.

Some browsers do provide this, notably Chrome and Firefox both providing access to the system color picker through a small color swatch.

Neither IE nor Safari provide any support here, leaving the user to figure out that they’re supposed to enter a 7-digit hex number all by themselves.

{{% ad-panel-leaderboard %}}

Color fields might find use in theming for personalization and in CMS use, but unless the users are sufficiently technical to deal with hex color codes, it may be better not to rely on the browser providing a nice UI for these.

<p class="ciu_embed" data-feature="input-color" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-color">Can I Use input-color?</a> Data on support for the input-color feature across the major browsers from caniuse.com.</p>

### Recommendation

Unless you know your users will be happy to fall back to entering hexadecimal color codes, it’s best not to rely on browsers supporting `type="color"`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f700b51-6916-49ef-a8b9-6858232cf985/html5-input-types-fields.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f700b51-6916-49ef-a8b9-6858232cf985/html5-input-types-fields.png" sizes="100vw" caption="Range, color and date fields as displayed by Edge, Firefox and Chrome. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f700b51-6916-49ef-a8b9-6858232cf985/html5-input-types-fields.png'>Large preview</a>)" alt="A combined screenshot showing the different visual representations of range, color and date fields in three different browsers: Edge, Firefox and Chrome." >}}

## <a href="#" name="a8" id="a8"></a>8. Date Fields

HTML5 introduced a number of different `type` values for creating inputs for dates and times. These included `date`, `time`, `datetime-local`, `month` and `week`.

At first glance, these appear to be heaven-sent, as collecting dates in a form is a difficult experience for both developer and user, and they’re needed pretty frequently.

The promise here is that the new field types enable the browser to provide a standardized, accessible and consistent user interface to capture dates and times from the user with ease. This is really important, as date and time formats vary world-over based on both language and locale, and so a friendly browser interface that translates an easy-to-use date selection into an unambiguous technical date format really does sound like the ideal solution.

As such, valid input for `type="date"` field is an unambiguous _year-month-day_ value such as `2019-01-16`. Developers like these, as they map pretty much to the ISO 8601 date format, which is used in most technical contexts. Unfortunately, few regular human beings use this date format and aren’t likely to reach for it when asked to provide a date in a single empty text field.

And, of course, a single empty text field is what the user is presented with if their browser does not provide a user interface for picking dates. In those cases, it then becomes very difficult for a user to enter a valid date value unless they happen to be familiar with the format required or the input is annotated with clear instructions.

Many browsers do provide a good user interface for picking dates, however. Firefox has a really excellent date picker, and Chrome and Edge also have pretty good interfaces. However, there’s no support in poor old IE and none in Safari, which could be an issue.

<p class="ciu_embed" data-feature="input-datetime" data-periods="current" data-accessible-colours="false"> <a href="https://caniuse.com/#feat=input-datetime">Can I Use input-datetime?</a> Data on support for the input-datetime feature across the major browsers from caniuse.com. </p>

### Recommendation

While convenient where it works, the failure mode of `type="date"` and its associated date and time types is very poor. This makes it a risky choice that could leave users struggling to meet validation criteria.

## Conclusion 

A lot has changed in the browser landscape in the four years since the HTML5 specification became a recommendation. Support for the newer types of input is fairly strong &mdash; particularly in mobile devices with virtual keyboards such as tablets and phones. In most cases, these inputs are safe to use and provide some extra utility to the user.

There are a couple of notable exceptions, the worst of which being the date and time fields, which not only lack utility, but also have more patchy browsers support. When support isn’t available, the fallback mode of these fields is poor. In these cases, it might be best to stick to JavaScript-based solutions for progressively enhancing the basic `type="text"` input fields.

If you’d like to read more, I’d thoroughly recommend the [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) on these field types, and as ever, the [W3C specification](https://www.w3.org/TR/html/sec-forms.html#the-input-element).

<script src="https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/caniuse-embed.min.js"></script>

{{< signature "ra, il" >}}
