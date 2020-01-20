# js-onepageadal-PBIE

### Single page Power BI Embedded application using ADAL.js

The following code sample demonstrates how to create single page HTML+JavaScript Power BI Embedded SaaS (or "user owns data") web application. It can be used to address this common question coming from the PBIE Developer community:

__How to create simple Power BI embedded application with the least amount of client side only code and without using .Net?__

The majority of friction points in Power BI Embedded projects typically revolve around authentication and authorization. Active Directory team provided ADAL.js and MSAL.js to help with obtaning AAD token in client side code only web apps.  

This sample code allows developers to:

* Obtain Power BI REST API token that is valid for 60 min using ADAL.js (i.e., no dependencies on .Net libraries). Incidentally this token can also be used on Power BI Embedded JavaScript demo [page](https://aka.ms/pbijs) if you want to experiment with embedding your own content in the JavaScript Playground environment provided by the Power BI Embedded team.
* Use that token in a single page app to experiment with embedding all supported in PBIE objects like reports, tiles, dashboards and Q&A.
* This authentication flow may help with embedding Power BI content into 3rd party applications that support HTML+JS extensibility.

NOTE: Although this approach can also be used for simulating user activity, recommended for Power BI load testing methodology is described in this [blog post](https://powerbi.microsoft.com/en-us/blog/power-bi-premium-know-what-your-premium-capacity-can-handle/).

__Prerequisites to use the sample code are:__

1. Register your Power BI app in AAD as described [here](https://docs.microsoft.com/en-us/power-bi/developer/register-app). The web app auth flow requires the app to have valid callback URL, so that ADAL could return the token in the query string of the redirect. This means that you can’t just open a local HTML file on your machine. Since you need to obtain the token from the redirect URL, you will need to host your page on a web server. IIS Express included in Visual Studio projects works perfectly, but any web server that you have access to should work just fine as well. If you already have an AAD Power BI app registered, you may need to tweak its manifest per these [instructions](https://community.dynamics.com/crm/b/akmscrmblog/posts/response-type-token-is-not-enabled-for-the-application).  This app manifest parameter: `oauth2AllowImplicitFlow` needs to be set to `true`. Code comments explicitly call out this critical configuration step and contain instructions URL as well.
2. Download [Power BI client side JavaScript library](https://github.com/Microsoft/PowerBI-JavaScript/tree/master/dist) if you don’t want to use GitHub content delivery version URL that is included with this sample. You only need one library file to include with your page. Use powerbi.js if you expect to do a lot of client side debugging or powerbi.min.js for simple apps.

I’ve put this sample together from the bits and pieces that I found in various documents, code samples and in comments on stackoverflow. There were several code adjustments and extra configuration steps that had to be tweaked for the app to render an embedded report. Code lines that require extra configuration steps have been annotated with appropriate comments. Code includes several helper variables and functions that could assist with troubleshooting potential issues. For example, sample REST API call to get embed token trial usage information in browser console can be removed since it has no impact on Power BI object embedding. However, if your report is not loading or rendering as expected, this call could be helpful to validate that you have proper AAD and Power BI REST API access tokens and are dealing with Power BI Embedded configuration issue  instead (e.g., missing workspace access).
