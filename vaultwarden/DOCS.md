# Home Assistant Community Add-on: Vaultwarden (Bitwarden)

This is forked from the original Vaultwarden [community-addon].
Updates in the original addon repo takes too long.

Credit goes to [frenck] for the base addon and [StrausFuenf] for extending it by push notification and fail2ban

This Addon adds Push notification support and Fail2ban for more security

## Vaultwarden

Bitwarden is an open-source password manager that can store sensitive
information such as website credentials in an encrypted vault.

The Bitwarden platform offers a variety of client applications including
a web interface, desktop applications, browser extensions and mobile apps.

This add-on is based upon the lightweight and opensource
[Vaultwarden][vaultwarden] implementation, allowing you to self-host
this amazing password manager.

Password theft is a serious problem. The websites and apps that you use are
under attack every day. Security breaches occur and your passwords are stolen.
When you reuse the same passwords everywhere hackers can easily access your
email, bank, and other important accounts. USE A PASSWORD MANAGER!

## Installation

The installation of this add-on is pretty straightforward and not different in
comparison to installing any other Home Assistant add-on.

1. Click the Home Assistant My button below to open the add-on on your Home
   Assistant instance.

   [![Open this add-on in your Home Assistant instance.][addon-badge]][addon]

1. Click the "Install" button to install the add-on.
1. Start the "Vaultwarden (Bitwarden)" add-on.
1. Check the logs of the "Vaultwarden (Bitwarden)" add-on to see if everything
   went well and to get the admin token/password.
1. Click the "OPEN WEB UI" button to open Vaultwarden.
1. Add `/admin` to the URL to access the admin panel, e.g.,
   `http://hassio.local:7277/admin`. Log in using the admin token you got
   in step 4.
1. The admin/token in the logs is only shown until it is saved or changed.
   Hit save in the admin panel to use the randomly generated password or
   change it to one of your choosing.
1. Be sure to store your admin token somewhere safe. **The add-on will never
   show it again!**

## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

Example add-on configuration:

```yaml
push_enabled: true
fail2ban: true
push_key: "123"
push_id: "123"
log_level: info
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### Option: `log_level`

The `log_level` option controls the level of log output by the addon and can
be changed to be more or less verbose, which might be useful when you are
dealing with an unknown issue. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `warning`: Exceptional occurrences that are not errors.
- `error`: Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. Add-on becomes unusable.

Please note that each level automatically includes log messages from a
more severe level, e.g., `debug` also shows `info` messages. By default,
the `log_level` is set to `info`, which is the recommended setting unless
you are troubleshooting.

### Option: `fail2ban`

Enable or Disable fail2ban for more security. Set it `true` to enable it, `false` otherwise.

### Option: `push_enabled`

Enable or Disable Vaultwarden mobile push. Set it `true` to enable it, `false` otherwise.

**Note**: _This needs push_id and push_key!_

### Option: `push_id`

The Bitwarden Push ID create one on: https://bitwarden.com/host/

**Note**: _Vaultwarden only supports bitwarden.com you cant use bitwarden.eu_

### Option: `push_key`

The Bitwarden Push ID create one on: https://bitwarden.com/host/

**Note**: _Vaultwarden only supports bitwarden.com you cant use bitwarden.eu_

## Known issues and limitations

- This add-on cannot support Ingress at this time due to technical limitations
  of the Bitwarden Vault web interface.
- Some web browsers, like Chrome, disallow the use of Web Crypto APIs in
  insecure contexts. In this case, you might get an error like
  `Cannot read property 'importKey'`. To solve this problem, you need to enable
  SSL and access the web interface using HTTPS.

You could also [open an issue here][issue] GitHub.

## Authors & contributors

The original setup of this repository is by [StrausFuenf][strausfuenf].

## License

MIT License

Copyright (c) 2019-2023 Franck Nijhof

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_bitwarden&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[frenck]: https://github.com/frenck
[vaultwarden]: https://github.com/dani-garcia/vaultwarden
[community-addon]: https://github.com/hassio-addons/repository/tree/master/bitwarden
[strausfuenf]: https://github.com/strausfuenf
