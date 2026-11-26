# Changelog

All notable changes to the HomeGadgets.ca Tools repository and the tools it
documents are listed here. Dates are UTC.

## [Unreleased]

Release preparation (branch `release-prep`). Nothing here is published until
the owner approves it.

### Added

- README in English and French: what each tool is, its status, and a link to
  its page on homegadgets.ca.
- Price Now risk notice at the top of the README, in English
  (`NOTICE_PRICE_NOW.md`) and French (`docs/fr/NOTICE_PRICE_NOW.md`), the one
  text every surface copies word for word.
- Guides in `docs/`: MCP server, public API, browser extension, Price Now
  (install, use, troubleshooting, privacy, FAQ), and French install steps in
  `docs/fr/installation.md`.
- Price Now licence, `PRICE_NOW_LICENSE.md` and `PRICE_NOW_LICENSE.fr.md`. The
  MIT licence in `LICENSE` covers the documentation only.
- `SECURITY.md` and `CONTRIBUTING.md`.
- Release notes and checksum file for Price Now in `releases/price-now/`.

### Changed

- The README no longer says the MCP server is "coming soon": it has been live
  at `https://mcp.homegadgets.ca/mcp` since before this release.
- The README no longer says the extension does "live price checks": it shows
  prices we recorded, with their dates.

### Tool versions documented

- MCP server: Beta 0.9 (four tools: `search_products`, `get_price`,
  `compare_retailers`, `server_info`).
- Browser extension: HomeGadgets Price Check 0.4.5, Chrome Web Store.
- Price Now for Windows: 0.4.2611 (Experimental), installer not code-signed.
  A newer monthly build replaces it before 2026-12-06.

## 2026-07-29

- Repository scaffold: README, CHANGELOG, LICENSE.
