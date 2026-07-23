---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Project Setup

{% stepper %}
{% step %}
## Install the Package



COZY can be installed in two ways. For more frequent updates and access to beta builds, use the GitHub installation. For more stable builds, use the Unity Asset Store installation.

{% tabs %}
{% tab title="Unity Package Manager" %}
Navigate to your Unity project and open the Package Manager (Window/Package Manager). Now navigate to `My Assets` and search for COZY 3

![](https://distant-lands.gitbook.io/cozy-stylized-weather-documentation/~gitbook/image?url=https%3A%2F%2F2041269432-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FrqKsGNTyQFMrNJSWMHS0%252Fuploads%252FlIu3vVYlzg2X2baXlOU4%252Fimage.png%3Falt%3Dmedia%26token%3D46616060-008c-4380-a003-82a7d31293ff\&width=768\&dpr=3\&quality=100\&sign=29121704\&sv=2)

Locate the COZY: Stylized Weather 3 package and click `Download` if this is your first time installing or Import to project if you have downloaded the package before.

![](https://distant-lands.gitbook.io/cozy-stylized-weather-documentation/~gitbook/image?url=https%3A%2F%2F2041269432-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FrqKsGNTyQFMrNJSWMHS0%252Fuploads%252FwkKo05k72CpivWyQaPaC%252Fimage.png%3Falt%3Dmedia%26token%3Df03f83f5-7af4-45fa-8dab-6ad17b1e2c44\&width=768\&dpr=3\&quality=100\&sign=5c717bf0\&sv=2)
{% endtab %}

{% tab title="GitHub" %}
COZY 3 now has GitHub support for version control and package download. To get GitHub access, you must be verified via your Unity Asset Store [invoice number](https://support.unity.com/hc/en-us/articles/205790859-How-can-I-get-an-invoice-for-an-Asset-Store-purchase). Email your INV number to contact@distantlands.space using the email address attached to your GitHub account to receive access.

Once you receive access, you can add the package by following these steps:

**Clone the Git URL**

Navigate to the GitHub page

<img src="https://distant-lands.gitbook.io/cozy-stylized-weather-documentation/~gitbook/image?url=https%3A%2F%2F2041269432-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FrqKsGNTyQFMrNJSWMHS0%252Fuploads%252FeMdFWEZqW8UiSYEwarVs%252Fimage.png%3Falt%3Dmedia%26token%3Dec7e4474-082e-4e00-a1fd-819d81747013&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=37f9bddd&#x26;sv=2" alt="" width="563">

Using the green **`<> Code`** button, copy the clone URL using HTTPS

<img src="https://distant-lands.gitbook.io/cozy-stylized-weather-documentation/~gitbook/image?url=https%3A%2F%2F2041269432-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FrqKsGNTyQFMrNJSWMHS0%252Fuploads%252FMDIIbRuU4KN9AeWFZJjl%252Fimage.png%3Falt%3Dmedia%26token%3D47f26034-f6be-4702-879c-c3b30c2b93f9&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=f6220f6d&#x26;sv=2" alt="" width="563">

**Install the Package**

Now, navigate to your Unity project and open the Package Manager (Window/Package Manager). Click the button and then select `Install package from git URL...`

<img src="https://distant-lands.gitbook.io/cozy-stylized-weather-documentation/~gitbook/image?url=https%3A%2F%2F2041269432-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FrqKsGNTyQFMrNJSWMHS0%252Fuploads%252FJwzwsz1H2g3sbjIWA3VV%252Fimage.png%3Falt%3Dmedia%26token%3Dc3930421-0431-4bd6-9cbb-a11c07759eb8&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=97e4175c&#x26;sv=2" alt="" width="563">

In the dialog box, paste the git clone URL and click install

<img src="https://distant-lands.gitbook.io/cozy-stylized-weather-documentation/~gitbook/image?url=https%3A%2F%2F2041269432-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FrqKsGNTyQFMrNJSWMHS0%252Fuploads%252FiK3DpGLOmjlF3nMeOjLv%252Fimage.png%3Falt%3Dmedia%26token%3De8177cdb-f655-4dd5-98f5-236bf45c76f8&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=16fb9f03&#x26;sv=2" alt="" width="563">

Unity will now install the package from GitHub! Be sure to check the GitHub page often for updates.
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
## Update Project Settings

COZY 4 has a one click setup helper to make starting a new project as simple as possible.

Navigate to Tools/COZY: Weather 4/Setup Scene to open the window

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

This window contains various tests and fixes for common setup issues

<figure><img src="../.gitbook/assets/image (13).png" alt="" width="563"><figcaption></figcaption></figure>

Once all warnings are errors have been resolved, your project is ready to work with COZY 4!
{% endstep %}

{% step %}
## Configure Preferences (Optional)

COZY comes with lots of available options for localization and toggleable features that allow you to get the most out of your installation. For the best results, take a look over the [preferences.md](../using-cozy/preferences.md "mention") window.

COZY is pre-configured for a U.S. based project making use of Imperial units for temperature, pressure, time format, and date format.


{% endstep %}
{% endstepper %}
