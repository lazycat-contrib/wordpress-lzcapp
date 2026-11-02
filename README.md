# WordPress (LazyCat LPK)

The world's most popular CMS.

- Upstream: https://github.com/WordPress/WordPress
- Image: `library/wordpress:7.1.4-php8.4-apache` (official Docker Hub image, mirror mode, digest-matched)
- License: GPL-2.0 (full text in `content/licenses/LICENSE`)
- Containers: WordPress + MariaDB 10.11

## Notes

- **Composite tags.** Upstream no longer publishes bare `x.y.z` tags; the current form is
  `7.1.4-php8.4-apache`. The Action config therefore uses a `version_regex` with a named
  `version` capture group to extract `7.1.4` from the tag, plus a `version_template` that
  rebuilds the full tag. Pure-semver `tag_regex` alone would match nothing.
- The image writes `wp-config.php` from `WORDPRESS_DB_*` env vars; the admin account is created
  in the browser installer — no seeded credential.
- `WORDPRESS_CONFIG_EXTRA` pins `WP_HOME`/`WP_SITEURL` to the app's https domain and forces
  `$_SERVER['HTTPS']` behind the proxy, so the admin panel and permalinks don't redirect to localhost.
- Webroot at `/lzcapp/var/html`, database at `/lzcapp/var/db`.
- No mail service configured.
- Not yet verified on a real device.
