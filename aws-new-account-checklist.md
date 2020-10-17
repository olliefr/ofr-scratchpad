
# AWS new account checklist

* Enable 2FA (hardware or software).
* Change the payment currency in `My Account`, `Payment Currency Preferences`.
* Set up a billing alarm:
  
  In `My Billing` dashboard, choose `Account/Billing Preferences` and set options:
    - `Receive PDF invoice by email`
    - `Receive free tier usage alerts` (input email only if different)
    - `Receive billing alerts`

* Add a `CloudWatch` alarm:

  - Enter `CloudWatch` dashboard
  - `Alarms`, `Add alarm`, 
  - `Select metric`, `Billing`, `Total estimated charge`, 
  - `USD`, `Select metric`, 
  - input $10, `In alarm`, `Create a new topic`, 
  - input a suitable name such as `Billing_Alert`, 
  - input email to notify probably the root email, `Create topic`, 
  - input name such as `Billing Alert` and description, `Create alert`)

* AC recommends filling out *Billing* and *Security* contacts for even for personal accounts. I don't see much point tbh.

* Enable access to billing information for an upcoming `iamadmin` user:

  *By default* only the `root` user has access to that.

  - `My Account`
  - `IAM User and Role Access to Billing Information`, `Edit`
  - &hellip;

* Add IAM Admin User [use instead of `root` when admin privileges are needed]

  - Helpful to name it `iamadmin`.
  - Set up 2FA for the admin user.
  - Add the *access keys*, if necessary.
