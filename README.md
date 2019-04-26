# Login OAuth2 Plugin

The **Login OAuth2** Plugin for [Grav CMS](http://github.com/getgrav/grav) allows user authentication against an OAuth2 Authentication Provider. This plugin makes use of [The League OAuth2 Client](http://oauth2-client.thephpleague.com/) 

Currently the core plugin supports the following providers:

* **Facebook** - https://developers.facebook.com/docs/facebook-login/web
* **GitHub** - https://developer.github.com/apps/building-oauth-apps/creating-an-oauth-app/
* **Google** - https://developers.google.com/identity/protocols/OpenIDConnect
* **Instagram** - https://www.instagram.com/developer/authentication/
* **LinkedIn** - https://developer.linkedin.com/docs/oauth2

It's also possible to extend this plugin an create a new AOauth2 for specific providers. 


### Installation

Installing the Login OAuth2 plugin can be done in one of two ways. The GPM (Grav Package Manager) installation method enables you to quickly and easily install the plugin with a simple terminal command, while the manual method enables you to do so via a zip file.

### GPM Installation (Preferred)

The simplest way to install this plugin is via the [Grav Package Manager (GPM)](http://learn.getgrav.org/advanced/grav-gpm) through your system's terminal (also called the command line).  From the root of your Grav install type:

    bin/gpm install login-oauth2

This will install the Login OAuth2 plugin into your `/user/plugins` directory within Grav. Its files can be found under `/your/site/grav/user/plugins/login-oauth2`.

### Manual Installation

To install this plugin, just download the zip version of this repository and unzip it under `/your/site/grav/user/plugins`. Then, rename the folder to `login-oauth2`. You can find these files on [GitHub](https://github.com/trilbymedia/grav-plugin-login-oauth2) or via [GetGrav.org](http://getgrav.org/downloads/plugins#extras).

You should now have all the plugin files under

    /your/site/grav/user/plugins/login-oauth2
    
Before configuring this plugin, you should copy the `user/plugins/login-oauth2/login-oauth2.yaml` to `user/config/plugins/login-oauth2.yaml` and only edit that copy.    

### Admin Installation

If you use the admin plugin, you can install directly through the admin plugin by browsing the to `Plugins` in the sidebar menu and clicking on the `Add` button.

Configuring the Login OAuth2 plugin is as easy as navigating to the `Plugins` manager, and editing the configuration options.

## Configuration Options

The default configuration and an explanation of available options:

```yaml
enabled: true
callback_uri: '/task:callback.oauth2'

built_in_css: true
button_style: row
save_grav_user: false
store_provider_data: true
default_access_levels:
  access:
    site:
      login: 'true'

providers:
  github:
    enabled: true
    client_id: ''
    client_secret: ''
    options:
      scope: ['user', 'user:email']

  instagram:
    enabled: true
    client_id: ''
    client_secret: ''
    options:
      scope: ['basic', 'likes', 'comments']
      host: 'https://api.instagram.com'

  facebook:
    enabled: true
    app_id: ''
    app_secret: ''
    options:
      scope: ['email', 'public_profile', 'user_hometown']
      graph_api_version: 'v2.10'

  google:
    enabled: true
    client_id: ''
    client_secret: ''
    hd: '*'
    options:
      scope: ['email', 'profile']
      avatar_size: 200

  linkedin:
    enabled: true
    client_id: ''
    client_secret: ''
    options:
      scope: ['r_basicprofile','r_emailaddress']



admin:
  enabled: false
  built_in_css: true
  button_style: row
  callback_uri: '/task:callback.oauth2'

  providers:
    github:
      enabled: false
      client_id: ''
      client_secret: ''
      options:
        scope: ['user', 'user:email']

    instagram:
      enabled: false
      client_id: ''
      client_secret: ''
      options:
        scope: ['basic', 'likes', 'comments']
        host: 'https://api.instagram.com'

    facebook:
      enabled: false
      app_id: ''
      app_secret: ''
      options:
        scope: ['email', 'public_profile', 'user_hometown']
        graph_api_version: 'v2.10'

    google:
      enabled: false
      client_id: ''
      client_secret: ''
      hd: '*'
      options:
        scope: ['email', 'profile']
        avatar_size: 200

    linkedin:
      enabled: false
      client_id: ''
      client_secret: ''
      options:
        scope: ['r_basicprofile','r_emailaddress']
```

### Server Settings

|Key                   |Description                 | Values |
|:---------------------|:---------------------------|:-------|
|enabled|Enables the plugin | [default: `true`] \| `false`|
|built_in_css|Enables the plugin-provided CSS to be loaded| [default: `true`] \| `false`|
|button_style|If you want to provide your own custom CSS, feel free to disable the CSS provided by the plugin| [default: `row`] \| `square`|
|save_grav_user|Store the grav user account as a local YAML account | true \| [default: `false`] |
|store_provider_data|If storing a local Grav user, you can also store OAuth2 Provider data so its available in Grav| true \| [default: `false`] |
|default_access_levels.access|You can find more information on access levels in the https://learn.getgrav.org/advanced/groups-and-permissions#permissions|[default: `site: { login: 'true' }`]|
|callback_uri|This is the URI that the provider will call when it has authenticated the user remotely. You shouldn't need to change this|[default: `/task:callback.oauth2`]|


### OAuth2 Providers

#### GitHub

|Key                   |Description                 | Values |
|:---------------------|:---------------------------|:-------|
|enabled|Enable or disable this specific provider. This stops its showing as an valid login option| [default: `true`] \| `false` |
|client_id|The **Client ID** Provided by GitHub when you register an application for OAuth2 authentication | `<string>` |
|client_secret|The **Client Secret** Provided by GitHub when you register an application for OAuth2 authentication | `<string>` |
|scope|An array of strings that define the OAuth2 scope. These can enable retrieving more data, but often require more permissions | e.g. `['user', 'user:email', 'repo']` |

#### Instagram

|Key                   |Description                 | Values |
|:---------------------|:---------------------------|:-------|
|enabled|Enable or disable this specific provider. This stops its showing as an valid login option| [default: `true`] \| `false` |
|client_id|The **Client ID** Provided by Instagram when you register an application for OAuth2 authentication | `<string>` |
|client_secret|The **Client Secret** Provided by Instagram when you register an application for OAuth2 authentication | `<string>` |
|scope|An array of strings that define the OAuth2 scope. These can enable retrieving more data, but often require more permissions | e.g. `['basic', 'likes', 'comments']` |
|host|The host address of the Instagram OAuth2 API service _[don't change this unless you know what you are doing]_| e.g. `https://api.instagram.com` |

#### Facebook

|Key                   |Description                 | Values |
|:---------------------|:---------------------------|:-------|
|enabled|Enable or disable this specific provider. This stops its showing as an valid login option| [default: `true`] \| `false` |
|app_id|The **App ID** Provided by Facebook when you register an application for OAuth2 authentication | `<string>` |
|app_secret|The **App Secret** Provided by Facebook when you register an application for OAuth2 authentication | `<string>` |
|scope|An array of strings that define the OAuth2 scope. These can enable retrieving more data, but often require more permissions | e.g. `['email', 'public_profile', 'user_hometown']` |
|graph_api_version|The Graph AP version to use _[don't change this unless you know what you are doing]_. | e.g. `v2.10` |

#### Google

|Key                   |Description                 | Values |
|:---------------------|:---------------------------|:-------|
|enabled|Enable or disable this specific provider. This stops its showing as an valid login option| [default: `true`] \| `false` |
|client_id|The **Client ID** Provided by Google when you register an application for OAuth2 authentication | `<string>` |
|client_secret|The **Client Secret** Provided by Google when you register an application for OAuth2 authentication | `<string>` |
|scope|An array of strings that define the OAuth2 scope. These can enable retrieving more data, but often require more permissions | e.g. `['email', 'profile']` |
|avatar_size|The size in pixels of the avatar URL to store | e.g. `200` |

#### Instagram

|Key                   |Description                 | Values |
|:---------------------|:---------------------------|:-------|
|enabled|Enable or disable this specific provider. This stops its showing as an valid login option| [default: `true`] \| `false` |
|client_id|The **Client ID** Provided by Instagram when you register an application for OAuth2 authentication | `<string>` |
|client_secret|The **Client Secret** Provided by Instagram when you register an application for OAuth2 authentication | `<string>` |
|scope|An array of strings that define the OAuth2 scope. These can enable retrieving more data, but often require more permissions | e.g. `['r_basicprofile','r_emailaddress']` |


> Note that if you use the admin plugin, a file with your configuration will be saved in the `user/config/plugins/login-oauth2.yaml`.

### Usage

Once properly configured, the functionality of the OAuth2 plugin is simple for the user.  The login form will display `enabled` OAuth2 Providers, and the user can click on one which will then redirect them to the provider to authenticate and `accept` the permissions requested via the `scope` fields.  Upon completion of this process, the user will then be redirected back to the site where they will now be logged in.

#### OAuth2 User Data

Any user data available via the `scope` provider options will be retrieved.  Core fields like `username`, and `email` will be stored on the Grav user object, and anything else that is provider-specific can be optionally stored as well.  By default, the Grav user object **is not** persisted to a physical Grav account YAML file, instead it's just kept in session temporarily.

#### Storing Grav User

By default the OAuth2 plugin does not store any local user information.  Upon successfully authenticating against the OAuth2 user, a user is created and is available during the session.  However, upon returning, the user must re-authenticate and the OAuth2 data is retrieved again.

If you want to be able to set user data (extra fields, or specific user access) for a particular user, you can enable the `save_grav_user` option, and this will create a local Grav user in the `accounts/` folder.  This is a local record of the user and attributes can be set here.  

> NOTE: Any attribute stored under the provider key (e.g. `github:`) in the user account file will be overwritten by the plugin during the next login.  This information is always in sync with latest data from the provider.  
>  
> Also note that the password will never be stored in the Grav user under `accounts/`.

#### OAuth2 to Grav Access Mapping

The OAuth2 plugin provides a flexible way to map your OAuth2 users into Grav.  

> For Groups and Access mapping to work properly a valid `search_dn`, `query_dn` and `group_query` is required.

The default configuration for `default_access_levels.access` looks like:

```yaml
user:
  site:
    login: true
```

In order for a front-end user to be able to log into a Grav site the minimum of `site: [login: true]` is required. You can of course configure this with any access settings you wish to provide. 

It is not advised to provide any `admin` access via OAuth2 accounts, but if you wish a particular OAuth user to be able to log into the admin, you should enable the `save_grav_user` option, so the userdata is persisted as a Grav Account YAML file, and then manually add the desired permissions.  These **will not** be reset to the default values on each login.

> NOTE: See the [Groups and Permissions Documentation](https://learn.getgrav.org/advanced/groups-and-permissions?target=_blank) for more information about how Grav permissions work in conjunction with access levels and groups.

### Troubleshooting

To get a quick state of your OAuth2 configuration, you can simply dump out the Grav user on a temporary _secure_ page:

```markdown
---
title: OAuth2 Test
cache_enabled: false
process:
    twig: true
access:
    site.login: true
---

# Grav User

{{ vardump(grav.user) }}
```


