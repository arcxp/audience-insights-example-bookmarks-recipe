Example code is provided by a community of developers. They are intended to help you get started more quickly, but are not guaranteed to cover all scenarios nor are they supported by Arc XP.

> These examples are licensed under the [MIT license](https://mit-license.org/): THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Reiterated from license above, all code in this example is free to use, and as such, there is NO WARRANTY, SLA or SUPPORT for these examples.

-----

# Description
<!-- In this example we will listen for the `story:create` and `story:update` events so that we can send a formatted payload containing some ANS fields to an external service. Pipedream is used here, but can be replaced with any external service. Keep in mind with example code you will likely always have to make *some* changes. -->
Audience Insights Bookmarking feature let readers save articles for later. 
You can use it to quickly set up options for your users to bookmark and save content. This is directly connected to content with the ANS ID.
It can be implemented as standard PageBuilder Theme blocks and can be used together or independently to deliver a lightweight save-for-later experience.

What you’ll build:

* **Bookmark button on article pages**

    * Reader can bookmark the current article.

    * Reader can see on initial load if it’s already bookmarked.

* **Bookmark list component (My Bookmarks)**

    * Reader can see their list of saved bookmarks.

    * Reader can delete a bookmark from the list.

# Quick Overview

We provide a set of APIs and SDK methods that allow you to connect your end users with our system. For tracking user calls and accessing protected public APIs, most of our public APIs requires an access token. This access token is in JWT (JSON web tokens) format and is returned after the user is logged in to the system.

When the user logs in, two JWTs are returned if the request is successful:

* **Access token:** This token has a limited lifetime (15 minutes by default) and identifies the user. It must be passed as a Bearer token in the protected request.

* **Refresh token:** This token is used to refresh and obtain a new access token when the old one expires. You can customize the lifetime of the refresh token through the CSR tool.

To interact with our system, you can either call the APIs directly or use our SDK packages. Our SDK methods act as wrappers that help developers interact with our APIs more easily. We strongly recommend using our SDKs, as these libraries handle various tasks for you. For more details.

The Arc XP Bookmark SDK is published to NPM.

After you install npm, to install the Arc SDKs, execute the following command in your npm project:

`npm i @arc-publishing/sdk-bookmarks`

After you have them installed, include the SDKs in your code:

`import Audience Insights from '@arc-publishing/sdk-bookmarks'`;

To access the right API endpoints through the SDKs, specify an API Origin before calling any other SDK methods.

```shell 
Identity.options({
apiOrigin: '{your api origin or CDN here}'
});
```
:::note
If you are using _Page Builder_, you can set up the API origin directly on the code (blocks.json file) or through the Page Builder app (Site Properties tab). 
Check <Link blank href={`https://dev.arcxp.com/subscriptions/identity/configure/arc-xp-identity-themes-blocks-configuration-customization-deep-dive/`} text="How-to: ArcXP Identity Themes Blocks Configuration & Customization Deep Dive" /> for additional information.
If you are using our blocks, we call `Identity.options()` for you.
:::

For more information about the available SDK methods, see <Link blank href={`https://dev.arcxp.com/subscriptions/developer-docs/arc-xp-subscriptions-sdks/`} text="Arc XP Subscriptions SDKs" />.


## Set up  

In this example we will walk through creating Bookmarks so that your users bookmark and save content. We are using custom blocks here. Keep in mind with example code you will likely always have to make *some* changes.

This example code can also be used as a starting point for other behaviors. With some modification, you can format data from other external systems and use that information to automate performance of actions within Arc.

→ Download the working bundle from PageBuilder Deployer bundles

→ Unzip it and open in your IDE

→ Create `.env` file in the root of your project and add your github token 

```
# Modify to put your org's URL
CONTENT_BASE=https://api.sandbox.[org].arcpublishing.com

# This is just for testing, never commit PATs in your code!
ARC_ACCESS_TOKEN=[your Arc XP PAT]

# Add your github token
GITHUB_TOKEN=[your github token]
```
→ Create `.npmrc` file in the root of your project and add your github token 

→ In package.json add `@arc-publishing/sdk-bookmarks` with version number

→ In components/features create folder for bookmark and bookmark-list and add the code provided, update it according to your needs. ANS id field have to be updated based on how your organization retrieves ANS id for articles.

→ Run `npm i` in your project to install dependencies

→ Run `npx fusion start` to test it locally

→ Zip your bundle using `npx fusion zip` and upload the bundle to Pagebuilder Deployer. Once uploaded, deploy and promote it to make it live.

→ Now you can start testing the custom bookmarks blocks

For more information on how to manage bundles refer to this documentation https://docs.arcxp.com/en/products/pagebuilder/pagebuilder-editor/developer-tools-overview/deployer-overview/managing-your-bundles.html

Check <Link blank href={`https://dev.arcxp.com/subscriptions/identity/configure/arc-xp-identity-themes-blocks-configuration-customization-deep-dive/`} text="How-to: ArcXP Identity Themes Blocks Configuration & Customization Deep Dive" /> for additional information on how to use the custom blocks.
