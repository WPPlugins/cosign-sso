=== CoSign Single Signon ===
Contributors: jiangxin
Tags: authentication, sso, cosign, ldap, login
Donate link: 
Requires at least: unknown
Tested up to: 2.9.2
Stable tag: 0.3.1

Alternative authentication plugin for WordPress. This plugin add several login method: LDAP login and two Single Sign-on(SSO) login method: CoSign V2, CoSign V3.

== Description ==

**CoSign SSO** is a WordPress plugin that provides several alternative authentication methods to WordPress, and it maybe easily extend to support more SSO login methods. CoSign v2 and CoSign v3 are the first two Single Sign-on(SSO) addins, that whay this plugin named. The other login method is just a by-product which provides LDAP authentication.

When this plugin is enabled, and the login method is set to *SSO*, then using a external CoSign single sign-on login service. When user click login, browser will redirect to remote login url, and will redirect back after successful logged in. If set login method to *LDAP*, login with the familiar login screen, but authentication backend changed to LDAP.

Whether using *SSO* or *LDAP* login method, LDAP options must provided to fetch user account information. If the logged in user account does not exists, create it on the fly by default.

== Installation ==

This section describes how to install the plugin and get it working.

1. Download the archive and expand it.
2. Upload the *cosign-sso* folder into your *wp-content/plugins/* directory
3. In your *WordPress Administration Area*, go to the *Plugins* page and click *Activate* for *CoSign SSO*

Once you have *CoSign SSO* installed and activated you can change it's settings in *Settings > CoSign SSO*.

== Settings ==

The settings for *CoSign SSO* are extremely simple. **But** before you change the login method to 'SSO' or 'LDAP', you mast check options for cosign and ldap carefully. **Wrong configrations will ban all users including yourself!**

If you cannot login any more, don't blame me. A trick may help you:

    $ touch <PLUGIN_DIR>/cosign-sso/FALLBACK

If the fallback file contains "ldap", "cosign2", or "cosign3", it will fallback to the right login method.

After you correct the settings, not forgot to remove the *FALLBACK* file.

Notes for CoSign 3.x:

* CoSign 3.x filter needs to add a "/cosign/valid" location as cosign handler.
* If wordpress uses a permlink, which means the RewriteRule in .htaccess may conflict with the "/cosign/valid" handler.
* You can hack wp-includes/rewrite.php, add "RewriteRule ^cosign/valid - [L]" right after "RewriteBase" directive.

== Screenshots ==

1. Options for *CoSign SSO* in English.
2. Options for *CoSign SSO* in Chinese.


== Localization ==

This section describes how to localized, which means let cosign-sso speak in your language.

* POT file : *cosign-sso/languages/cosign_sso.pot*
* Copy pot file to your locale, such as *cosign-sso/languages/cosign_sso-zh_CN.pot* for Chinese.
* Translate it using your favorate editor. lokalize and kbabel are recommended.
* Convert po to mo using command: 
<pre>
      $ cd plugins/cosign-sso/languages
      $ msgfmt cosign_sso-zh_CN.po -o cosign_sso-zh_CN.mo
</pre>

== Changelog ==
= 0.3.1 =

1. Code refactor.
2. Add CoSign v3 support as a new login method.

= 0.3.0 =

1. Add support for CoSign 3.x protocol.
2. Add cosign protocol settings in admin pannel, which support for both 2.x and 3.x.

= 0.2 =

1. FALLBACK to LDAP auth backend if a FALLBACK file exists with "LDAP" in it.
2. A blank file FALLBACK exists, disable this plugin totally.

= 0.1 =

1. Initial release.

== Frequently Asked Questions ==

= CoSign login url changed, can not login!!! =

If CoSign login url changed, when user login the web browser will redirect to wrong place.
If this happens, you can simply *FALLBACK* to LDAP authenticate backend or *DISABLE* this plugin totally.

* To disable this plugin, simply create a file named *FALLBACK* under the plugin directory.
<pre>
    $ echo -n > <PLUGIN_DIR>/cosign-sso/FALLBACK
</pre>
* To fallback to LDAP auth backend, simply create a file named *FALLBACK* with the content "LDAP".
<pre>
    $ echo LDAP > <PLUGIN_DIR>/cosign-sso/FALLBACK
</pre>

After you correct the settings, not forgot to remove the *FALLBACK* file.

== Upgrade Notice ==

Nothing.

== Known Issues ==

No known issues at this time. 

If you find any bugs or want to request some additional features for future releases, please log them on the wordpress project of [homepage for our interest projects](http://redmine.ossxp.com/)

