# Email links & Tokens Authorization

When we send an email to the user we often send links to the eTools portal.  
In some cases we also need to authorize user automatically, so there is a complex mechanism with the chain of redirects to be assured that everything we need will be performed.

Here is an example of such url:

> https://etools2.razortheory.com/tokens/email/login/?next=%2Fusers%2Fapi%2Fchangecountry%2F%3Fcountry%3D9%26next%3D%252Ftpm%252Fvisits%252F232%252Fdetails&url\_auth\_token=693906

  
It consists of three important steps:

1. Base url is `tokens/email/login`. This view is simply checking the authorization. This is very important step, because it wraps changecountry api view \(_in case of unauthorized user there will be plain response, which is not informative enough_\). If user is authenticated \(or auth token is provided\), user will be redirected to the next step, else user will be asked to authorize and if everything is ok, user can continue to the original path. Remaining part of the url is coded inside the `next` argument.
2. Next is `users/api/changecountry` endpoint, which switch country to the desired one to be ensured user will be in the correct workspace when attempting to open the page. Again, next part of path is inside `next` argument.
3. And, finally, we are on the correct page.

Example of redirects chain:

![](../.gitbook/assets/nvw4gz.jpg)

### Tokens Authorization

Sometimes there's a need to authorize user automatically \(for example, for Third Party Monitors or Auditors\). In this case we add auth token, which is used by django middleware and authorize user without asking credentials. More information can be found in `TokenAuthenticationMiddleware` . Also, there is a view which can be accessed by `tokens/email/login` endpoint, where user can ask newer auth token by user's email. In this case`next`argument will be coded into the form context and will be remembered for future usage in token renewal link.

