---
title: User Authentication For Web And iOS Apps With AWS Cognito (Part 2)
slug: user-authentication-web-ios-apps-aws-cognito-part-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/562ea666-a30e-40b0-83b4-ce2b5630ba3f/cognito-diagram-preview-opt.png
date: 2017-09-21T20:50:42.000Z
author: davidtucker
description: >-
  If you regularly create new web or mobile applications, then Amazon Cognito is
  a powerful tool that can cut 90% of the time it usually takes to set up a
  custom user-management solution.
categories:
  - Mobile
  - Tools
  - Workflow
  - Authentication
  - Security
  - iOS
---
## In Our Last Episode

In the [previous article](https://www.smashingmagazine.com/2017/08/user-authentication-web-ios-apps-aws-cognito-part-1/), I introduced the concept of user management and how complicated it is in our current digital landscape. In addition, I introduced [Amazon Cognito](https://aws.amazon.com/cognito/) (henceforth referred to as Cognito), a service provided through Amazon Web Services, as a way to deal with this complexity. To illustrate this, I created an iOS application that uses Cognito to provide a login for users using a custom user pool.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bd80d98-79f1-4129-adfe-a2694c0f04c9/cognito-diagram-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f00eda1d-a10b-4474-9e5e-83344fb43deb/cognito-diagram-800w-opt.jpg" width="800" height="527" alt="" /></a><figcaption>Cognito custom user pool diagram (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bd80d98-79f1-4129-adfe-a2694c0f04c9/cognito-diagram-large-opt.jpg">View large version</a>)
</figcaption></figure>

Now that we have the basics of an application in place, I want to implement several aspects of user management within the sample application. These aspects include user signup, email verification, password resetting and multi-factor authentication. After that, I want to talk through some of the additional value that Cognito provides through its security model and how you could use it to secure the back end of your application.

{{% feature-panel %}}

To get up and running for this article, you'll need to leverage the user pool that was created in the [previous article](https://www.smashingmagazine.com/2017/08/user-authentication-web-ios-apps-aws-cognito-part-1/). If you haven't done that work, you can be up and running in about 30 minutes and ready to move forward with what I am covering today.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Rethinking Common Password Habits</h4>
<p>The more services we use, the more passwords we’re forced to remember. Is there a way to improve this? Well, just like everything else, we need to do what’s right for our users. <a href="https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/" class="btn btn--medium btn--blue">Read a related article →</a></p>
</div>

## Sample Code

If you are following along with the sample code, you will need to have set up a user pool, configured it properly, and added the settings to a `plist` file before the application will work. This is a fairly simple (but lengthy) process that was covered thoroughly in the [previous article](https://www.smashingmagazine.com/2017/08/user-authentication-web-ios-apps-aws-cognito-part-1/). Most every section of this article will include a link to the Git tag that is used at that point of the code. I hope this will make it easier to follow along.</p>

## Letting Users Sign Up

The first step in a user's journey in your application is the signup process. Cognito provides the capability to allow for users to sign up or to allow only administrators to sign up users. In the previous article, we configured the user pool to allow users to sign up.

One key element to remember in regards to signup is that this is where your attribute settings and password policy are enforced. If you set attributes as required in the user pool, you will have to submit all of those values in order for your signup call to be successful. In our case, we need to gather the user's first name, last name, email address and desired password.

In this new view controller, `SignupViewController`, we have an action that gets called when the user clicks the “Complete Registration” button. We need to respond to a few things if they occur:

*   If there is an error, we need to present the error to the end user and allow them to resubmit the form.
*   If we are successful with the signup, we need to check whether the user requires verification of their email address. According to how we set up the user pool, this is a requirement. In most all cases, the user will be required to go to the next step and verify their email address.

The following code represents this process in action:

<pre><code class="language-c">@IBAction func signupPressed(_ sender: AnyObject) {
    // Get a reference to the user pool
    let userPool = AppDelegate.defaultUserPool()
    // Collect all of the attributes that should be included in the signup call
    let emailAttribute = AWSCognitoIdentityUserAttributeType(name: "email", value: email.text!)
    let firstNameAttribute = AWSCognitoIdentityUserAttributeType(name: "given_name", value: firstName.text!)
    let lastNameAttribute = AWSCognitoIdentityUserAttributeType(name: "family_name", value: lastName.text!)
    // Actually make the signup call passing in those attributes
    userPool.signUp(UUID().uuidString, password: password.text!, userAttributes: [emailAttribute, firstNameAttribute, lastNameAttribute], validationData: nil)
    .continueWith { (response) -&gt; Any? in
        if response.error != nil {
            // Error in the signup process
            let alert = UIAlertController(title: "Error", message: response.error?.localizedDescription, preferredStyle: .alert)
            alert.addAction(UIAlertAction(title: "OK", style: .default, handler:nil))
            self.present(alert, animated: true, completion: nil)
        } else {
            self.user = response.result!.user
            // Does user need verification?
            if (response.result?.userConfirmed != AWSCognitoIdentityUserStatus.Confirmed.rawValue) {
                // User needs confirmation, so we need to proceed to the verify view controller
                DispatchQueue.main.async {
                    self.performSegue(withIdentifier: "VerifySegue", sender: self)
                }
            } else {
                // User signed up but does not need verification
                DispatchQueue.main.async {
                    self.presentingViewController?.dismiss(animated: true, completion: nil)
                }
            }
        }
        return nil
    }
}
</code></pre>

## Verifying Email Addresses

Email verification is configured in the creation of the user pool, which we covered in the previous article. As you can see in the following image, we chose to require email validation for users. By verifying email addresses, we can leverage the addresses for other use cases, such as resetting passwords.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b59cd5e9-6ce4-411f-a77d-ed43dd9a5bd9/userpool-step4-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4603fc08-b890-405c-9d5d-79a2fcb46c4a/userpool-step4-800w-opt.jpg" width="800" height="425" alt="" /></a><figcaption>Step 4 of user pool creation: configuring verifications for the user pool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b59cd5e9-6ce4-411f-a77d-ed43dd9a5bd9/userpool-step4-large-opt.jpg">View large version</a>)
</figcaption></figure>

### Workflow

The entire signup process will also include verification if the user pool was configured that way. The “happy path” representation of this flow would be as follows:

1.  The user is presented with the login screen when launching the application.
2.  The user presses the “Sign up for an account” option on the login screen.
3.  The user is presented with the signup form.
4.  The user fills out the signup form correctly with their information.
5.  The user is presented with the email verification form.
6.  The user enters the code from their email.
7.  The user is sent back to the login form, where they can now log in with their new account.

This flow can be seen in the following view controllers, which are a part of the sample application:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce549d54-93bc-4d97-bad3-d1653f59d77e/auth-verification-flow-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43586315-a496-4c7d-9ca6-db81b171c897/auth-verification-flow-800w-opt.jpg" width="800" height="388" alt="" /></a><figcaption>Signup and verification flow (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce549d54-93bc-4d97-bad3-d1653f59d77e/auth-verification-flow-large-opt.jpg">View large version</a>)
</figcaption></figure>

There is one important note about verification to consider. If you decide to require both email address and phone number for verification, Cognito will choose to insert the phone number verification into the signup process. You will then have to detect whether the email address is verified and include the logic required to verify it. However, in most cases, if you verify one of the attributes and use it for password resetting, then there isn't as much of a need to verify the other. If you plan to use multi-factor authentication, I would recommend requiring phone-number verification only.</p>

### Coding the Email Verification

Two key actions need to be supported in the view controller that is handling the verification process: submitting the verification code, and requesting that the code be sent again. Luckily, these two actions are fairly easy to implement, and the code can be seen below:

<pre><code class="language-c">func resetConfirmation(message:String? = "") {
    self.verificationField.text = ""
    let alert = UIAlertController(title: "Error", message: message, preferredStyle: .alert)
    alert.addAction(UIAlertAction(title: "Retry", style: .default, handler: nil))
    self.present(alert, animated: true, completion:nil)
}

@IBAction func verifyPressed(_ sender: AnyObject) {
    // Confirm / verify the user based on the text in the verify field
    self.user?.confirmSignUp(verificationField.text!)
    .continueWith(block: { (response) -&gt; Any? in
        if response.error != nil {
            // In this case, there was some error or the user didn't enter the right code.
            // We will just rely on the description that Cognito passes back to us.
            self.resetConfirmation(message: response.error!.localizedDescription)
        } else {
            DispatchQueue.main.async {
                // Return to Login View Controller - this should be handled a bit differently, but added in this manner for simplicity
                self.presentingViewController?.presentingViewController?.dismiss(animated: true, completion: nil)
            }
        }
        return nil
    })
}

@IBAction func resendConfirmationCodePressed(_ sender: AnyObject) {
    self.user?.resendConfirmationCode()
    .continueWith(block: { (response) -&gt; Any? in
        let alert = UIAlertController(title: "Resent", message: "The confirmation code has been resent.", preferredStyle: .alert)
        alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
        self.present(alert, animated: true, completion:nil)
        return nil
    })
}
</code></pre>

As discussed in the signup and verification flow section, if the user is successful in verifying their address, they will be sent back to the login screen. After this login, the user will be able to get into the protected view within the application, which will display their attributes.

Signup and verification were relatively painless. If you want to see the code at this point of the article, check out the `signup-verify` tag of the [code on GitHub](https://github.com/davidtucker/CognitoSampleApplication/releases/tag/signup-verify).</p>

## Forgot Password

Another key use case in user management is helping users to reset their password securely. Cognito provides this functionality through either email or text message, depending on how the user pool has been configured.

It is important to note that verification is required for resetting a user's password. If you don't specify either the phone number or email address to be verified, then the user will have to reach out to you to reset their password. In short, every user pool should have, at minimum, one verified attribute.</p>

### Workflow

Just as with signup and verification, the forgot-password workflow is a multi-step process. To achieve the goal of resetting the user's password, we need to follow these steps (which only include the happy path):

1.  We need to get the user's email address to get a reference to the user.
2.  We need to request that a verification code be sent to the user. If the user pool has a verified phone number, it will be sent as an SMS. If there isn't a verified phone number, it will be sent as an email.
3.  We need to inform the user where to look for the code in a secure manner. Cognito returns a masked version of the phone number or email address, to give the user a heads up of where to look.
4.  We allow the user to fill out a form, including both the verification code and a new password.
5.  We submit the password and verification code to Cognito.
6.  We let the user know that their password reset was successful, and they can now log into the application.
7.  We send them back to the login screen.

This flow can be seen in the following view controllers, which are a part of the sample application:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9afad56-e232-4364-bccd-4240c22517a9/forgot-password-views-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a26449b-643e-4620-90e5-32da6ae2424b/forgot-password-views-800w-opt.jpg" width="800" height="605" alt="" /></a><figcaption>Forgot-password workflow (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9afad56-e232-4364-bccd-4240c22517a9/forgot-password-views-large-opt.jpg">View large version</a>)
</figcaption></figure>

### Coding the Forgot-Password Workflow

The first step in coding this workflow is to request that the user be sent a verification code. To do this, `LoginViewController` will pass the email address to `ForgotPasswordViewController` before the segue is performed. Once the new view appears, the email address will be used to get a reference to the user and request a verification code.</p>

<pre><code class="language-c">override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)
    if !emailAddress.isEmpty {
        // Get a reference to the user pool
        let pool = AppDelegate.defaultUserPool()
        // Get a reference to the user using the email address
        user = pool.getUser(emailAddress)
        // Initiate the forgot password process, which will send a verification code to the user
        user?.forgotPassword()
        .continueWith(block: { (response) -&gt; Any? in
            if response.error != nil {
                // Cannot request password reset due to error (for example, the attempt limit is exceeded)
                let alert = UIAlertController(title: "Cannot Reset Password", message: (response.error! as NSError).userInfo["message"] as? String, preferredStyle: .alert)
                alert.addAction(UIAlertAction(title: "OK", style: .default, handler: { (action) in
                    self.clearFields()
                    self.presentingViewController?.dismiss(animated: true, completion: nil)
                }))
                self.present(alert, animated: true, completion: nil)
                return nil
            }
            // Password reset was requested and message sent. Let the user know where to look for code.
            let result = response.result
            let isEmail = (result?.codeDeliveryDetails?.deliveryMedium == AWSCognitoIdentityProviderDeliveryMediumType.email)
            let destination:String = result!.codeDeliveryDetails!.destination!
            let medium = isEmail ? "an email" : "a text message"
            let alert = UIAlertController(title: "Verification Sent", message: "You should receive \(medium) with a verification code at \(destination).  Enter that code here along with a new password.", preferredStyle: .alert)
            alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
            self.present(alert, animated: true, completion: nil)
            return nil
        })
    }
}
</code></pre>

One point to note on this is that Cognito returns information that enables you to tell the user where to find the code. In the code above, we are detecting whether the code will be sent to an email address or phone number, as well as the masked version of the destination. This can be seen in the sample application in the image below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19ec0a7d-7459-4fa5-9f08-2545e5c426e7/forgot-password-prompt-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19ec0a7d-7459-4fa5-9f08-2545e5c426e7/forgot-password-prompt-preview-opt.jpg" width="750" height="1334" alt="" /></a><figcaption>Forgot-password prompt
</figcaption></figure>

After requesting the code, we need to allow the user to enter the new code and updated password. This code from `ForgotPasswordViewController` is triggered when the user clicks on the “Reset Password” button.</p>

<pre><code class="language-c">@IBAction func resetPasswordPressed(_ sender: AnyObject) {
    // Kick off the 'reset password' process by passing the verification code and password
    user?.confirmForgotPassword(self.verificationCode.text!, password: self.newPassword.text!)
    .continueWith { (response) -&gt; Any? in
        if response.error != nil {
            // The password could not be reset - let the user know
            let alert = UIAlertController(title: "Cannot Reset Password", message: (response.error! as NSError).userInfo["message"] as? String, preferredStyle: .alert)
            alert.addAction(UIAlertAction(title: "Resend Code", style: .default, handler: { (action) in
                self.user?.forgotPassword()
                .continueWith(block: { (result) -&gt; Any? in
                    print("Code Sent")
                    return nil
                })
            }))
            alert.addAction(UIAlertAction(title: "Cancel", style: .cancel, handler: { (action) in
                DispatchQueue.main.async {
                    self.presentingViewController?.dismiss(animated: true, completion: nil)
                }
            }))
            self.present(alert, animated: true, completion: nil)
        } else {
            // Password reset. Send the user back to the login and let them know they can log in with new password.
            DispatchQueue.main.async {
                let presentingController = self.presentingViewController
                self.presentingViewController?.dismiss(animated: true, completion: {
                    let alert = UIAlertController(title: "Password Reset", message: "Password reset.  Please log into the account with your email and new password.", preferredStyle: .alert)
                    alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
                    presentingController?.present(alert, animated: true, completion: nil)
                        self.clearFields()
                    }
                )
            }
        }
        return nil
    }
}
</code></pre>

Once this process is complete, the user is returned to the login screen and informed that the password reset was successful. At this point, the user can log into the application using their new password.

If you want to see the code at this point of the article, check out the `forgot-password` tag of the [code on GitHub](https://github.com/davidtucker/CognitoSampleApplication/releases/tag/forgot-password).</p>

## Multi-Factor Authentication

Multi-factor authentication (MFA) is becoming a standard for anything requiring heightened security. Right now, if I want to log into my email, my bank, my mortgage account or even GitHub, I have to enter a code that I get via text message. Because of this extra layer of security, we prevent anyone from logging into an account if they have both my username and password. Instead of just using a single factor (the password) with the username, they have to use multiple factors (password and the code via SMS).

The great thing is that Cognito supports this out of the box through SMS. The Cognito team has stated that it is also working to add support for email MFA; however, at the time of writing, this isn't an option. To make this work, we'll need to change some configuration settings in AWS and create a new user pool.</p>

### New User Pool

To properly demonstrate the capabilities of multi-factor authentication using SMS, I will be creating a new custom user pool with only a few modifications compared to our previous user pool. Note that some features (such as required attributes) cannot be modified once a user pool has been created. Because of this, you’ll want to have a solid strategy around your user pool before starting to use it.

The modifications that I made compared to the previous user pool are detailed below:

*   Phone number has been added as a required attribute.
*   Users can sign in using their email address or phone number (we will still choose the email address here).
*   Multi-factor authentication has been set as optional.
*   Email verification has been disabled, and phone number verification has been enabled.</p>

### Using SMS Instead of Email

If you are going to send anything more than a few SMS messages per month, you'll need to request a higher Simple Notification Service (SNS) limit for SMS messages. This is mostly painless, but it is a requirement if you are going to ship an app. The following excerpt from Cognito’s documentation will point you in the right direction. While the team responds to requests fairly quickly, it isn't instant. I would recommend submitting the request at least a few weeks before a push to production. According to “[Specifying User Pool MFA Setting and Email and Phone Verification Settings](https://docs.aws.amazon.com/cognito/latest/developerguide/user-pool-settings-email-phone-verification.html)” in the Amazon Cognito Documentation:

<blockquote>
<p>The default spend limit per account (if not specified) is 1.00 USD per month. If you want to raise the limit, submit an <a href="https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html">SNS Limit Increase case</a> in the AWS Support Center. For <strong>New limit value</strong>, enter your desired monthly spend limit. In the <strong>Use Case Description</strong> field, explain that you are requesting an SMS monthly spend limit increase.</p>
</blockquote>

### Workflow

Because we aren't forcing multi-factor authentication for the user pool (although you certainly could), we will have a multi-step process to enable and then execute multi-factor authentication. These steps are detailed below (these are the happy path steps):

1.  When the user signs up for an account, they will be asked to verify their phone number (instead of their email address).
2.  After logging into the application, the user will be able to enable multi-factor authentication in their profile.
3.  After enabling multi-factor authentication, the user will be presented with the authentication challenge upon their next login.
4.  Upon entering the multi-factor authentication code correctly, the user will be able to use the application as expected.</p>

### Coding Multi-Factor Authentication

The Cognito SDK triggers the display of the multi-factor authentication view controller. You have to define how you want to handle that trigger. In the sample application, this happens in `AppDelegate`. Because our `AppDelegate` implements `AWSCognitoIdentityInteractiveAuthenticationDelegate`, we have the option to define how we want this to be handled. The code below shows the implementation in the sample application:

<pre><code class="language-c">func startMultiFactorAuthentication() -&gt; AWSCognitoIdentityMultiFactorAuthentication {
    if (self.multiFactorAuthenticationController == nil) {
        self.multiFactorAuthenticationController = self.storyboard?.instantiateViewController(withIdentifier: "MultiFactorAuthenticationController") as? MultiFactorAuthenticationController
    }

    DispatchQueue.main.async {
        if(self.multiFactorAuthenticationController!.isViewLoaded || self.multiFactorAuthenticationController!.view.window == nil) {
            self.navigationController?.present(self.multiFactorAuthenticationController!, animated: true, completion: nil)
        }
    }

    return self.multiFactorAuthenticationController!
}
</code></pre>

In the case above, we instantiate the view controller from the storyboard, and then we present it. Finally, this view controller is presented.

Within `MultiFactorAuthenticationController`, we handle the process much like we did in `LoginViewController`. The view controller itself implements a protocol that is specific to this use case: `AWSCognitoIdentityMultiFactorAuthentication`. By implementing this protocol, you get an instance in the `getCode` method, which you must use to pass in the code for verification. The result of this verification will trigger the `didCompleteMultifactorAuthenticationStepWithError` method.</p>

<pre><code class="language-c">class MultiFactorAuthenticationController: UIViewController {

    @IBOutlet weak var authenticationCode: UITextField!
    @IBOutlet weak var submitCodeButton: UIButton!

    var mfaCompletionSource:AWSTaskCompletionSource?

    @IBAction func submitCodePressed(_ sender: AnyObject) {
        self.mfaCompletionSource?.set(result: NSString(string: authenticationCode.text!))
    }

}

extension MultiFactorAuthenticationController: AWSCognitoIdentityMultiFactorAuthentication {

    func getCode(_ authenticationInput: AWSCognitoIdentityMultifactorAuthenticationInput, mfaCodeCompletionSource: AWSTaskCompletionSource) {
        self.mfaCompletionSource = mfaCodeCompletionSource
    }

    func didCompleteMultifactorAuthenticationStepWithError(_ error: Error?) {
        DispatchQueue.main.async {
            self.authenticationCode.text = ""
        }
        if error != nil {
            let alertController = UIAlertController(title: "Cannot Verify Code",
                                                    message: (error! as NSError).userInfo["message"] as? String,
                                                    preferredStyle: .alert)
            let resendAction = UIAlertAction(title: "Try Again", style: .default, handler:nil)
            alertController.addAction(resendAction)

            let logoutAction = UIAlertAction(title: "Logout", style: .cancel, handler: { (action) in
                AppDelegate.defaultUserPool().currentUser()?.signOut()
                self.dismiss(animated: true, completion: {
                    self.authenticationCode.text = nil
                })
            })
            alertController.addAction(logoutAction)

            self.present(alertController, animated: true, completion:  nil)
        } else {
            self.dismiss(animated: true, completion: nil)
        }
    }

}
</code></pre>

One additional piece needs to be noted. Because we didn't force every user to use multi-factor authentication, we have to give the user the option to enable it. To do this, we'll need to update the user's settings. The code below (from `AppViewController`) demonstrates how to both enable and disable multi-factor authentication by using `UISwitch` as input:

<pre><code class="language-c">let settings = AWSCognitoIdentityUserSettings()
if mfaSwitch.isOn {
    // Enable MFA
    let mfaOptions = AWSCognitoIdentityUserMFAOption()
    mfaOptions.attributeName = "phone_number"
    mfaOptions.deliveryMedium = .sms
    settings.mfaOptions = [mfaOptions]
} else {
    // Disable MFA
    settings.mfaOptions = []
}
user?.setUserSettings(settings)
.continueOnSuccessWith(block: { (response) -&gt; Any? in
    if response.error != nil {
        let alert = UIAlertController(title: "Error", message: (response.error! as NSError).userInfo["message"] as? String, preferredStyle: .alert)
        alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
        self.present(alert, animated: true, completion:nil)
        self.resetAttributeValues()
    } else {
        self.fetchUserAttributes()
    }
    return nil
})
</code></pre>

To see the code at this point of the article, check out the `mfa` tag of the [code on GitHub](https://github.com/davidtucker/CognitoSampleApplication/releases/tag/mfa).</p>

## Taking It Further: API Security

One of the benefits of using Cognito for user management is how it integrates with other AWS services. One great example of this is how it integrates with API Gateway. If you want to have a set of APIs that only logged-in users can access, you can use the user group authorizer for API Gateway. This allows you to pass the token you receive when logging into your API calls, and API Gateway will handle the authorization for you.

This can be particularly powerful if you want to set up a serverless back end (via Lambda) that is exposed through API Gateway. This means you could pretty quickly set up a secured set of API endpoints to power your web or mobile application. If you are interested in exploring this more, feel free to check the following article from the API Gateway documentation: “[Use Amazon Cognito User Pools with API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html).”

Unfortunately, setting up a back end with Lambda is beyond the scope of this article. However, Amazon has provided a resource on getting started with Lambda: “[Build an API to Expose a Lambda Function](https://docs.aws.amazon.com/apigateway/latest/developerguide/getting-started.html).”

## Conclusion

Within a couple of articles, we have managed to progress from an insecure application to an application that supports all of the common user management use cases. What's even better is that this user management capability is a service supported by AWS, and until you get over 10,000 active users, it is mostly free to use. I believe that whether you are a web, iOS or Android developer, this toolset will prove to be a valuable one. I'm sure you've got an idea of what you can build to test this out. Feel free to use the [sample code](https://github.com/davidtucker/CognitoSampleApplication) to help you in that process.

Happy coding!

### Links and Resources

*   [Amazon Cognito](https://aws.amazon.com/cognito/)
*   “[Developer Resources](https://aws.amazon.com/cognito/dev-resources/),” Amazon Cognito
*   “[AWS Mobile SDK](https://aws.amazon.com/mobile/sdk/),” AWS

{{< signature "da, yk, al, il" >}}

