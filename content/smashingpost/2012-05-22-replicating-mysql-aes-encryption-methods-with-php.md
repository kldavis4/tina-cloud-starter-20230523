---
title: Replicating MySQL AES Encryption Methods With PHP
slug: replicating-mysql-aes-encryption-methods-with-php
image: null
date: 2012-05-22T18:54:39.000Z
author: chad-smith-derek-woods
description: >-
  At our company, we process a lot of requests on the leading gift cards and
  coupons websites in the world. The senior developers had a meeting in late
  October to discuss working on a solution to replicate the MySQL functions of
  `AES_ENCRYPT` and `AES_DECRYPT` in the language of PHP.
categories:
  - Coding
  - PHP
  - Security
---
At our company, we process a lot of requests on the leading gift cards and coupons websites in the world. The senior developers had a meeting in late October to discuss working on a solution to replicate the MySQL functions of <code>AES_ENCRYPT</code> and <code>AES_DECRYPT</code> in the language of PHP. This article centers on what was produced by senior developer Derek Woods and how to use it in your own applications.

Security should be at the top of every developer’s mind when building an application that could hold sensitive data. We wanted to replicate MySQL’s functions because a lot of our data is already AES-encrypted in our database, and if you’re like us, you probably have that as well.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/)
*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [Speeding Up Your Website’s Database](https://www.smashingmagazine.com/2011/03/speeding-up-your-websites-database/)
*   [Why Static Website Generators Are The Next Big Thing](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)

## Why Does Encryption Matter?

We will begin by examining why security and encryption matter at all levels of an application. Every application, no matter how large or small, needs some form of security and encryption. Any user data you have is extremely valuable to potential hackers and should be protected. Basic encryption should be used when your application stores a password or some other form of identifying information.

{{% feature-panel %}}

Different levels of sensitive data require different encryption algorithms. Knowing which level to use can be determined by answering the basic question, “Will I ever need access to the original data after it has been encrypted?” When storing a user’s password, using a heavily salted MD5 hash and storing that in the database is sufficient; then, you would use the same MD5 hashing on the input and compare the result from the database. When storing other sensitive data that will need to be returned to its original input, you would not be able to use a one-way hashing algorithm such as MD5; you would need a two-way encryption scheme to ensure that the original data can be returned after it’s been encrypted.

Encryption is only as powerful as the key used to protect it. Imagine that an attacker breaches your firewall and has an exact clone of your database; without the key, breaking the encryption that protects the sensitive data would be nearly impossible. Keeping the key in a safe place should always be priority number one. Many people use an <code>ini</code> file that’s read at runtime and that is not publicly accessible within the scope of the Web server. If your application requires two-way encryption, there are industry standards for protecting such data, one being AES encryption.</p>

## What Is AES Encryption?

AES, which stands for Advanced Encryption Standard, was developed by Joan Daemen and Vincent Rijmen. They named their cipher, Rijndael, after a play on their two names. AES was announced as the winner of a five-year competition conducted by the National Institute of Standards and Technology (NIST) on 26 November 2001.

AES is a two-way encryption and decryption mechanism that provides a layer of security for sensitive data while still allowing the original data to be retrieved. To do this, it uses an encryption key that is used as a seed in the AES algorithm. As long as the key remains the same, the original data can be decrypted. This is necessary if your sensitive data needs to be returned to its original state.</p>

### How Does It Work?

AES uses a complex mathematical algorithm, which we will explore later, to combine two main concepts: confusion and diffusion. Confusion is a process that hides the relationship between the original data and the encrypted result. A classic example of this is the Caesar Cipher, which applies a simple shift of letters so that A becomes C, B becomes D, etc. Diffusion is a process that shifts, adjusts or otherwise alters the data in complex ways. This can be done using bit-shifts, replacements, additions, matrix manipulations and more. A combination of these two methods provides the layer of security that AES needs in order to give us a secure algorithm for our data.

In order to be bi-directional, the confusion and diffusion process is managed by the secret key that we provide to AES. Running the algorithm in one direction with a key and data will output an obfuscated string, thus encrypting the data. By passing that string back into the algorithm with the same key, running the algorithm in reverse will output the original data. Instead of attempting to keep the algorithm secret, the AES algorithm relies on complete key secrecy. According to its <a href="https://www.owasp.org/index.php/Cryptographic_Storage_Cheat_Sheet#Rule_-_Rekey_data_at_least_every_one_to_three_years">cryptographic storage guidelines</a>, OWASP recommends rotating the key every one to three years. The guidelines also go through methods of rotating AES keys.</p>

### PHP Mcrypt Specifics

PHP provides AES implementation through the Mcrypt extension, which gives us a number of other ciphers as well. In addition to the algorithm itself, Mcrypt provides multiple modes that alter the security level of the AES algorithm to make it more secure. The two definitions that we will need to use in our PHP functions are <code>MCRYPT_RIJNDAEL_256</code> and <code>MCRYPT_MODE_ECB</code>. Rijndael 256 is the encryption cipher that we will use for our AES encryption. Additionally, the code uses an “Electronic Code Book” that segments the data into blocks and encrypts them separately. Alternative and more secure modes are available, but MySQL uses ECB by default, so we will be crafting our PHP implementation around that.</p>

## Why Should You Avoid AES In MySQL?

Using MySQL’s AES encryption and decryption functions is very simple. Setting up requires less work, and it is generally far easier to understand. Apart from the obvious benefit of simplicity, there are three main reasons why PHP’s Mcrypt is superior to MySQL’s AES functions:

1.  MySQL needs a database link between the application and database in order for encryption and decryption to occur. This could lead to unnecessary scalability issues and fatal errors if the database has internal failures, thus rendering your application unusable.
2.  PHP can do the same MySQL decryption and encryption with some effort but without a database connection, which improves the application’s speed and efficiency.
3.  MySQL often logs transactions, so if the database’s server has been compromised, then the log file would produce both the encryption key and the original value.</p>

## MySQL AES Key Modification

Out of the box, PHP’s Mcrypt functions unfortunately do not provide encrypted strings that match those of MySQL. There are a few reasons for this, but the root cause of the difference is the way that MySQL treats both the key and the input. To understand the causes, we have to delve into MySQL’s default AES encryption algorithm. The code segments presented below have been tested up to the latest version of MySQL, but MySQL could possibly alter their encryption scheme. The first problem we encounter is that MySQL will break up our secret key into 16-byte blocks and XOR the characters together from left to right. XOR is an exclusive disjunction, and if the two bytes are the same, then the output is <code>0</code>; if they are different, then the output is <code>1</code>. Additionally, it begins with a 16-byte block of null characters, so if we pass in a key of fewer than 16 bytes, then the rest of the key will contain null characters.

Say we have a 34-character key: <code>123456789abcdefghijklmnopqrstuvwxy</code>. MySQL will start with the first 16 characters.

<pre><code class="language-php">new_key = 123456789abcdefg</code></pre>

The second step taken is to XOR (⊕) the next 16 characters in the value in <code>new_key</code> with the first 16.

<pre><code class="language-php">new_key = new_key ^ hijklmnopqrstuvw
new_key = 123456789abcdefg ^ hijklmnopqrstuvw
new_key = Y[Y_Y[YWI</code></pre>

Finally, the two remaining characters will be XOR’d starting from the left.

<pre><code class="language-php">new_key = new_key ^ xy
new_key =  Y[Y_Y[YWI ^ xy
new_key = !"Y_Y[YWI</code></pre>

This is, of course, drastically different from our original key, so if this process does not take place, then the return value from the decrypt/encrypt functions will be incorrect.</p>

### Key Padding

The second major difference between Mcrypt PHP and MySQL is that the length of the Mcrypt value must have padding to ensure it is a multiple of 16 bytes. There are numerous ways to do this, but the standard is to pad the key with the byte value equal to the number of bytes left over. So, if our value is 34 characters, then we would pad with a byte value of 14.

To calculate this, we use the following formula:

<pre><code class="language-php">$pad_value = 16-(strlen($value) % 16);</code></pre>

Using our 34-character example, we would end up with this:

<pre><code class="language-php">$pad_value = 16-(strlen("123456789abcdefghijklmnopqrstuvwxy") % 16);
$pad_value = 16-(34 % 16);
$pad_value = 16-(2);
$pad_value = 14;</code></pre>

## MySQL Key Function

In the previous section, we dove into the issues surrounding the MySQL key used to encrypt and decrypt. Below is the function that’s used in both our encryption and decryption functions.

<pre><code class="language-php">function mysql_aes_key($key)
{
	$new_key = str_repeat(chr(0), 16);
	for($i=0,$len=strlen($key);$i&lt;$len;$i++)
	{
		$new_key[$i%16] = $new_key[$i%16] ^ $key[$i];
	}
	return $new_key;
}</code></pre>

First, we instantiate our key value with 16 null characters. Then we iterate through each character in the key and XOR it with the current position in <code>new_key</code>. Since we’re moving from left to right and using modulus 16, we will always be XOR’ing the correct characters together. This function changes our secret key to the MySQL standard and is the first step in achieving interoperability between PHP and MySQL.</p>

## Value Transformation

We run into the last caveat when we pull the data from MySQL. For the data encrypted with AES, the padded values that we added before encryption will remain tacked onto the end after we decrypt. In general, this would go unnoticed if we were only fetching the data in order to display it; but if we’re using any of basic string functions on the decrypted data, such as <code>strlen</code>, then the results will be incorrect. There are a couple ways to handle this, and we will be removing all characters with a byte position of 0 through 16 from the right of our value since they are the only characters used in our padding algorithm.

The code below will handle the transformation.

<pre><code class="language-php">$decrypted_value = rtrim($decrypted_value, "..16");</code></pre>

Throwing all the concepts together, we have a few main points:

1.  We have to transform our AES key to MySQL’s standards;
2.  We have to pad the value that we want to encrypt if it’s not a multiple of 16 bytes in size;
3.  We have to strip off the padded values after we decrypt the encrypted value from MySQL.

It’s advantageous to segment these concepts into components that can be reused throughout the project and in other areas that use AES encryption. The following two functions are the end result and perform the encryption and decryption before sending the data to MySQL for storage.</p>

### MySQL AES Encryption

<pre><code class="language-php">function aes_encrypt($val)
{
	$key = mysql_aes_key('Ralf_S_Engelschall__trainofthoughts');
	$pad_value = 16-(strlen($val) % 16);
	$val = str_pad($val, (16*(floor(strlen($val) / 16)+1)), chr($pad_value));
	return mcrypt_encrypt(MCRYPT_RIJNDAEL_128, $key, $val, MCRYPT_MODE_ECB, mcrypt_create_iv( mcrypt_get_iv_size(MCRYPT_RIJNDAEL_128, MCRYPT_MODE_ECB), MCRYPT_DEV_URANDOM));
}</code></pre>

The first line is where we get the MySQL encoded key using the previously defined <code>mysql_aes_key</code> function. We are not using our real key in this article, but are instead paying homage to one of the creators of OpenSSL (among other technologies that he’s been involved in). The next line determines the character value with which to pad our data. The last two lines perform the actual padding of our data and call the <code>mcrypt_encrypt</code> function with the appropriate key and value. The return of this function will be the encrypted value that can be sent to MySQL for storage — or used anywhere else that requires encrypted data.</p>

### MySQL AES Decryption

<pre><code class="language-php">function aes_decrypt($val)
{
	$key = mysql_aes_key('Ralf_S_Engelschall__trainofthoughts');
	$val = mcrypt_decrypt(MCRYPT_RIJNDAEL_128, $key, $val, MCRYPT_MODE_ECB, mcrypt_create_iv( mcrypt_get_iv_size(MCRYPT_RIJNDAEL_128, MCRYPT_MODE_ECB), MCRYPT_DEV_URANDOM));
	return rtrim($val, "..16");
}</code></pre>

The first line of the decrypt function again generates the MySQL version of our secret key using <code>mysql_aes_key</code>. We then pass that key, along with the encrypted data, to the <code>mcrypt_decrypt</code> function. The final line returns the original data after stripping away any padded characters that we might have used in the encryption process.</p>

## See It In Action

To show that the encryption and decryption schemes here do in fact work, we must exercise both encryption and decryption functions in PHP and MySQL and compare the results. In this example, we have integrated the <code>aes_encrypt</code>/<code>aes_decrypt</code> and key function into a CakePHP model, and we are using Cake to run the database queries for MySQL. You can replace the CakePHP functions with <code>mysql_query</code> to obtain the results outside of Cake. In the first group, we are encoding the same data with the same key in both PHP and MySQL. We then <code>base64_encode</code> the result and print the data. The second group runs the MySQL encrypted data through PHP decrypt, and vice versa for the PHP encrypted data. We’re also outputting the result. The final block guarantees that the inputs and outputs are identical.

<pre><code class="language-php">define('MY_KEY','Ralf_S_Engelschall__trainofthoughts');

// Group 1
$a = $this-&gt;User-&gt;aes_encrypt('test');
echo base64_encode($a).'
';

$result = $this-&gt;User-&gt;query("SELECT AES_ENCRYPT('test', '".MY_KEY."') AS enc");
$b = $result[0][0]['enc'];
echo base64_encode($b).'
';

// Group 2
$result = $this-&gt;User-&gt;query("SELECT AES_DECRYPT('".$a."', '".MY_KEY."') AS decc");
$c = $result[0][0]['decc'];
echo $c."
";

$d = $this-&gt;User-&gt;aes_decrypt($b);
echo $d."
";

// Comparison
var_dump($a===$b);
var_dump($c===$d);</code></pre>

### Output

The snippet below is the output when you run the PHP commands listed above.

<pre><code class="language-php">L8534Dj1sH6IRFrUXXBkkA==
L8534Dj1sH6IRFrUXXBkkA==
test
test
bool(true) bool(true)</code></pre>

## Final Thoughts

AES encryption can be a bit painful if you are not familiar with the specifics of the algorithm or familiar with any differences between implementations that you might have to work with in your various libraries and software packages. As you can see, it is indeed possible to use native PHP functions to handle encryption and decryption and to actually make it work seamlessly with any legacy MySQL-only encrypted data that your application might have. These methods should be used regardless so that you can use MySQL to decrypt data if a scenario arises in which that is the only option.

{{< signature "al" >}}

