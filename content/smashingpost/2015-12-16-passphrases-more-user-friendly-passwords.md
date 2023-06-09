---
title: Why Passphrases Are More User-Friendly Than Passwords
slug: passphrases-more-user-friendly-passwords
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a074ffbc-4c0d-400d-a1f7-00d59043410c/08-passphrase-validation-opt.png
date: 2015-12-16T00:17:36.000Z
author: anthony-t
description: >-
  A user’s account on a website is like a house. The password is the key, and
  logging in is like walking through the front door. When a user can’t remember
  their password, it’s like losing their keys. When a user’s account is hacked,
  it’s like their house is getting broken into.

  Nearly half of Americans (47%) have had their account hacked in the last year
  alone. Are web designers and developers taking enough measures to prevent
  these problems? Or do we need to rethink passwords?
categories:
  - UX
  - User Interaction
  - Security
---
A user’s account on a website is like a house. The password is the key, and logging in is like walking through the front door. When a user can’t remember their password, it’s like losing their keys. When a user’s account is hacked, it’s like their house is getting broken into.</p>

<a href="https://money.cnn.com/2014/05/28/technology/security/hack-data-breach/">Nearly half of Americans</a> (47%) have had their account hacked in the last year alone. Are web designers and developers taking enough measures to prevent these problems? Or do we need to rethink passwords?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Current State Of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
*   [Better Password Masking For Sign-Up Forms](https://www.smashingmagazine.com/2012/10/password-masking-hurt-signup-form/)
*   [Stop Wasting Users’ Time](https://www.smashingmagazine.com/2014/04/stop-wasting-users-time/)

## The See-Saw Of Password Security And Usability

### Compromising Security

On most websites, you need to create an account to do more than browse. Users will create many passwords in their lifetime. But remembering them all is no easy task. They could use the same password for every account, but that makes them more vulnerable to attack if one gets compromised. They could use passwords that are easy to remember, but an easy password is an easy target for brute-force hacking.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a12958c-8acd-4dad-9b90-80d1772bf87f/01-usability-over-security-opt.png" alt="When users create a password with usability in mind, they often end up compromising security" /><br>
<figcaption>When users create a password with usability in mind, they often end up compromising security.</figcaption></figure>

They could jot down or store all of their passwords in case they forget, but if someone gets ahold of that paper or file, then all of their accounts will be compromised. As well, it’s easy to misplace papers and files and inconvenient to pull them out every time you want to log in somewhere.

No matter what they do, when users create a password with usability in mind, they often end up compromising security.</p>

### Compromising Usability

To keep their accounts secure, users could create passwords that meet the maximum requirements of a “strong” password. Such a password would include:

*   numbers,
*   lowercase letters,
*   capital letters,
*   punctuation symbols,
*   and a certain number of characters.

And it should not include:

*   a dictionary word,
*   a common password,
*   or words found in your name, username or company name.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d605738-7771-4a35-81d1-996e26ecbf25/02-security-over-usability-opt.png" alt="When a user finally comes up with a password, it’s often so random that it’s almost impossible to remember." /><br>
<figcaption>When a user finally comes up with a password, it’s often so random that it’s almost impossible to remember.</figcaption></figure>

Coming up with a password that meets these requirements would take most users a long time. You risk losing registrations if they take longer than expected. When a user finally comes up with a password, it’s often so random that it’s almost impossible to remember. This increases the chance that the user will forget and be unable to log in. Also frustrating is when a user is locked out of their account after trying too many passwords.

Typing passwords isn’t easy either, much less remembering them. Users are prone to error when they have to hold the Shift key to type capital letters or symbols. A password that’s secure but not usable won’t do users any good.</p>

## Are Password Managers The Solution?

Some users prefer to use <a href="https://en.wikipedia.org/wiki/Password_manager">password managers</a> to balance security and usability. Password managers are apps that store all of your passwords in a database with one master password. Instead of memorizing a different password for each account, all you have to do is memorize the master password.</p>

### A Solution For Users, Not For Websites

If you forget your master password, you’re out of luck. Most password managers don’t have a reset and recovery process like websites. If you forget your password on a particular website, you can always reset it. This gives websites control over their users’ security.

Password managers cost money. Developers can’t require all users to buy a password manager before using their website. That would be impractical and would cause many users to drop off. Websites should not put the responsibility of security on third-party applications, but rather should provide a solution that balances security and usability.</p>

### Many Don’t Trust Or Understand Password Managers

While some users trust password managers, many don’t. A <a href="https://people.scs.carleton.ca/~paulv/papers/usenix06.pdf">research study</a> (PDF) found that many are “uncomfortable with using the software and do not trust it because they do not understand it.”

Users don’t feel comfortable “relinquishing control to a computer program.” Even though they know that password security is a problem, they feel that “they are best equipped to care for their own passwords.”

Designers and developers cannot expect password managers to be a solution. It is their responsibility to provide users with secure and usable access to their account.</p>

## Passphrases: A Change For The Better

Balancing security and usability is a must, but passwords today don’t cut it. Websites need to change for the better and need to upgrade from passwords to <a href="https://en.wikipedia.org/wiki/Passphrase">passphrases</a>.

Passwords and passphrases serve the same purpose. But passwords are generally short, hard to remember and easier to crack. Passphrases are easier to remember and to type, and they’re considered more secure due to their length and because you don’t need to write them down.</p>

## Why Passphrases Are More Secure

### Longer Requirement Stops Brute-Force Attacks

Most passwords have a minimum requirement of 8 characters. But most passphrases have a minimum requirement of 16 characters. This greater length provides more security because it takes far longer to crack.

Increasing character length increases the total number of possible correct passwords. The longer a password is, the longer a brute-force program will take to guess the right one. Let’s put this to the test by comparing a complex password with a simple passphrase using a sophisticated <a href="https://password-checker.online-domain-tools.com/">password checker</a>.

The complex password will not have any dictionary words and will contain numbers, capital letters and symbols, making it as strong as can be. The simple passphrase will contain dictionary words and only lowercase letters, making it as weak as can be.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0db670f9-44be-487a-922b-785e5a81bc28/03-brute-force-attack-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80ab3469-d40a-4392-9655-91e9d6efd29f/03-brute-force-attack-opt-small.png" alt="The complex password will not have any dictionary words and will contain numbers, capital letters and symbols, making it as strong as can be." /></a><figcaption>The complex password will not have any dictionary words and will contain numbers, capital letters and symbols, making it as strong as can be.(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0db670f9-44be-487a-922b-785e5a81bc28/03-brute-force-attack-opt.png">View large version</a>)</figcaption></figure>

When comparing the two, we can see that the simple weak passphrase is impossible to brute-force hack. But the strong, complex password would take less than two years to hack. You would expect the password to take longer than that because of its high character complexity. That goes to show that character length is what protects users from brute-force attacks, not character complexity.</p>

### Multiple Words Stop Dictionary Attacks

Brute force isn’t the only way to hack a password. Hackers can also use dictionary attacks. But a passphrase will protect users against dictionary attacks more than a password. Although using a password that contains only dictionary words is not recommended, it is still common and can get hacked easily. But if users were to use only dictionary words in a passphrase, they would stay safe from this type of attack.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f04fbe1f-e9a2-4093-a579-725dedffd30a/04-dictionary-attack-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47b35dd5-119e-4340-a4c2-3c133254ce55/04-dictionary-attack-opt-small.png" alt="Passphrase will protect users against dictionary attacks more than a password." /></a><figcaption>Passphrase will protect users against dictionary attacks more than a password. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f04fbe1f-e9a2-4093-a579-725dedffd30a/04-dictionary-attack-opt.png">View large version</a>)</figcaption></figure>

Most dictionary passwords contain one or two words. A dictionary attack is more likely to succeed here because of the limited number of words in the dictionary. Even an uncommon dictionary word wouldn’t stop a dictionary attack. A dictionary passphrase would contain at least five words. The virtually infinite number of word combinations makes it impossible for a dictionary attack to succeed.</p>

### Multiple Parts of Speech Make It Harder to Guess

Passwords that are easy to guess often contain a single piece of personal information: the user’s name, birthdate or pet, their favorite color, food or place, etc. All of these nouns easily meet the character-length requirement for a password.

The longer character-length requirement of a passphrase prevents users from using personal information. A single noun isn’t enough to meet the requirement. This forces users to add other parts of speech to their passphrase, making it harder to guess.</p>

## Why Passphrases Are More Usable

### Phrases Are Easier to Remember Than Random Characters

It’s easier to recall a phrase than random characters. Phrases are meaningful and relatable. This is why users are able to remember a passphrase more than a password. When users create a password, they have to meet the form's password policy. Many forms do not allow dictionary words to keep users safe from dictionary attacks. Users have no choice but to add randomness to their password.

But a random non-dictionary word is the hardest for users to remember. Many will opt to use a word and add random characters within it. But that’s still hard to remember because the random characters could go in many places.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da1cdb3a-e293-4cd9-881d-7d23479a29aa/05-using-phrases-opt.png" alt="Using phrases" /></figure>

Adding complexity to a passphrase is easier because you can add elements between words. This makes the randomness easier to remember because there are fewer places between words. A passphrase doesn’t need the high level of randomness of passwords. A little complexity goes a long way because of the security that a passphrase brings. Some people use the first letter of each word in a sentence as their password. This is much more memorable but still not as secure as a passphrase.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d45badbd-a6f9-404c-a822-43809e3ef976/06-character-length-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4cde54e-6d0a-458c-a5f0-1649c3bea8b7/06-character-length-opt-small.png" alt="The difference in character length has a huge impact on security." /></a><figcaption>The difference in character length has a huge impact on security. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d45badbd-a6f9-404c-a822-43809e3ef976/06-character-length-opt.png">View large version</a>)</figcaption></figure>

For example, the sentence “I lived in Germany for two years” could be turned into “iliGf2yrs.” Even with a capital letter, a number and random letters, it’s still vulnerable to brute-force hacking. The same sentence spelled out as the passphrase “ilivedinGermanyfor2yrs” would be unhackable. The difference in character length has a huge impact on security.</p>

### Words Are Allowed

Finding a password that doesn’t include a dictionary word is the toughest password requirement for users to meet. Carnegie Mellon’s research data show that “creating a password is significantly more difficult under stricter password policies, particularly those involving dictionary checks.”

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/195eec01-9c2c-4d06-a3a3-02f2ae421c8e/07-using-words-opt.png" alt="Using words" /></figure>

Coming up with a random non-dictionary word is hard to do and hard to remember. Passphrases don’t need strict dictionary checks. Words are allowed as long as they meet the passphrase’s length requirement. The compromise of usability for security in password policies is too wide a gap to ignore. Passphrase policies balance both, minimizing registration abandonment or user frustration.</p>

### Passphrase Policies Are Less Strict In Registration Forms

Users often get stuck on registration pages when they can’t create a password that meets the website’s policy. This happens because password policies have too many requirements, creating frustration in users and leading them to abandon forms.
<table class="article-table two-columns"><br>
<tbody>
<tr>
<th>Password Policy</th>
<th>Passphrase Policy</th>
</tr>
<tr>
<td>
<ul>
 	<li>has at least 8 characters</li>
 	<li>includes capital and lowercase letters</li>
 	<li>includes one or more digits</li>
 	<li>includes one or more symbols (@, #, $, etc.)</li>
 	<li>prohibits words found in dictionary</li>
 	<li>prohibits user’s personal information</li>
</ul>
</td>
<td>
<ul>
 	<li>has at least 16 characters</li>
 	<li>includes a capital letter or number</li>
</ul>
</td>
</tr>
</tbody>
</table>

Passphrase policies don’t need to be as strict to give users security. The only requirement a passphrase needs is to be 16 character or longer. <a href="https://cups.cs.cmu.edu/rshay/pubs/passwords_and_people2011.pdf">Carnegie Mellon’s findings</a> (PDF) back this up. The researchers found that “a 16-character minimum with no additional requirements provides the most entropy while proving more usable on many measures than the strongest alternative.” This helps users to create accounts more easily while maintaining security.

Password policies vary between websites. This forces users to create a different password to meet each website’s requirements. Users end up with a long list of different passwords to manage. Passphrase policies wouldn’t vary between websites, though. All that is needed for maximum security is a length of 16 or more characters and a capital letter or number.</p>

### Longer Character Length Means More Typos

The only drawback to passphrases is that more characters means more typing for users, which can cause more typos, triggering form errors.

If you enforce passphrases, don’t lock out users after multiple attempts. Users have probably mistyped their passphrase. Instead, give them a CAPTCHA to solve after a high number of attempts. This way, you’ll prevent hacks while still allowing users to access their account.</p>

## What Websites Should Do

### Replace “Word” With “Phrase”

The first step is to take the “word” out of password. The term “password” gives users the impression that the website expects them to use a word. But a word isn’t secure under any circumstances.

Change the user’s understanding by using the term “passphrase” instead. This tells them that you expect a phrase, not a word. By making this expectation clearer, users will know that a phrase is more secure than a word.</p>

### Revise the Policy

The next step is to replace your password policy with a passphrase policy. This includes increasing the length requirement to at least 16 characters. It also includes requiring at least one capital letter or number. You could suggest adding more than one capital letter or number for extra security, but that’s not necessary.</p>

### Make the Policy Clear

Most users are accustomed to seeing password policies. Let them know that a passphrase policy is different by displaying the requirements upon registration. Pop up a tooltip over the passphrase text field.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a074ffbc-4c0d-400d-a1f7-00d59043410c/08-passphrase-validation-opt.png" alt="Passphrase validation" /><br>
<figcaption></figcaption></figure>

Don’t make users have to count 16 characters when creating a passphrase. Do it for them by designing a tooltip to validate their input. When the user meets the requirement, a green checkmark should appear next to the field.</p>

## Final Thoughts

The state of passwords today causes more headache than happiness. Passphrases are a better alternative because they are more secure and usable. A few websites out there enforce passphrases. More should follow suit in order to decrease account breaches and user frustration. No user should feel like they’ve lost their keys or had their house broken into.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e2c0e21-cb4c-4efc-9a8c-1aec7599b398/09-passphrase-login-opt.png" alt="Passphrase login" /><br>
<figcaption></figcaption></figure>

The good news is that switching to passphrases doesn’t require a technical overhaul. It’s as simple as introducing the concept to users and requiring a higher character length. The toughest part is understanding and accepting that the solution to the world’s password problems is so simple.

{{< signature "cc, ml, al" >}}

