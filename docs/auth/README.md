This folder describes third-party authentications supported by AWX. These authentications can be configured and enabled inside AWX.

When a user wants to log into AWX, she can explicitly choose some of the supported authentications to log in instead of AWX's own authentication using username and password. Here is a list of such authentications:
* Google OAuth2
* Github OAuth2
* Github Organization OAuth2
* Github Team OAuth2
* Github Enterprise OAuth2
* Github Enterprise Organization OAuth2
* Github Enterprise Team OAuth2
* Microsoft Azure Active Directory (AD) OAuth2

On the other hand, the other authentication methods use the same types of login info (username and password), but authenticate using external auth systems rather than AWX's own database. If some of these methods are enabled, AWX will try authenticating using the enabled methods *before AWX's own authentication method*. The order of precedence is:
* LDAP
* RADIUS
* TACACS+
* SAML

AWX will try authenticating against each enabled authentication method *in the specified order*, meaning if the same username and password is valid in multiple enabled auth methods (*e.g.*, both LDAP and TACACS+), AWX will only use the first positive match (in the above example, log a user in via LDAP and skip TACACS+).

## Notes:
SAML users, RADIUS users and TACACS+ users are categorized as 'Enterprise' users. The following rules apply to Enterprise users:

  * Enterprise users can only be created via the first successful login attempt from remote authentication backend.
  * Enterprise users cannot be created/authenticated if non-enterprise users with the same name has already been created in AWX.
  * AWX passwords of Enterprise users should always be empty and cannot be set by any user if there are enterprise backends enabled.
  * If enterprise backends are disabled, an Enterprise user can be converted to a normal AWX user by setting password field. But this operation is irreversible (the converted AWX user can no longer be treated as Enterprise user).
