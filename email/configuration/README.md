Configuration
=====

By default, Mastodon uses the SMTP protocol to send emails. In most cases, you will point Mastodon to an SMTP server that will receive emails from Mastodon and deliver them to the user's email provider on your behalf.

This document highlight the different configuration options available to mastodon instance administrator:
- [Using Mastodon without email](README.md#without-emails)
- [Understanding SMTP parameters](README.md#smtp-parameters)
- [Configure an SMTP provider: mailgun example](README.md#mailgun-example)
- [SMTP best practice](README.md#smtp-best-practice)
- [Configure a sendmail compatible relay](README.md#sendmail-example)
- [Best practice for email](README.md#email-best-practice)

### Without email
An administrator can bypass email confirmation via a rake task:
`RAILS_ENV=production bundle exec rails mastodon:confirm_email USER_EMAIL=user@example.com` 
Also an adminsitrator can wipe users that never confirmed e-mail and never signed in.
`RAILS_ENV=production bundle exec rails mastodon:clear`

### SMTP parameters
The parameters are configurable in the `.env.production` file. These are used by ActionMailer in `config/environments/production.rb`

#### Configure a local SMTP server without authentication
If you have a local SMTP server that doesn't require authentication, you only need to change `SMTP_SERVER`, `SMTP_PORT` and `SMTP_FROM_ADDRESS` from their defaults.

### Mailgun example


### Sendmail example
To use sendmail you need to set `SMTP_DELIVERY_METHOD=sendmail`

### SMTP best practices
To initiate a secure conversation with the SMTP service, it is best practice to use StartTLS by setting `SMTP_ENABLE_STARTTLS_AUTO=true`.
To authenticate to the host you're conversing with, you need to tell ActionMailer to tell OpenSSL to verify the host.
You can discard any failures with `SMTP_OPENSSL_VERIFY_MODE=none`.
You can choose to enforce the validity of the SSL/TLS certificate of server with `SMTP_OPENSSL_VERIFY_MODE=peer`.
To verify the authenticity of the certificate, OpenSSL will need to have a certificate authority file itslef. Make sure to set `SMTP_CA_FILE=/etc/ssl/certs/ca-certificates.crt` in your `.env.production` file.
Change your `config/environments/production.rb` to have a `:ca_file => ENV['SMTP_CA_FILE'],` in the `config.action_mailer.smtp_settings` section.

### Email best practices
On the receiving end, providers might expect you to follow certain method to validate the email sender and authenticate your domain.

#### SPF
(todo)

#### DKIM
(todo)

#### DMARC
(todo)

