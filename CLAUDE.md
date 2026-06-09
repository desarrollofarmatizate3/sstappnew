# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **CodeIgniter 3** PHP MVC application running on **Laragon** (Windows local dev stack). The project is named `SSTAPP` and is in its early stages — currently only the default Welcome controller exists.

- **Local URL**: `http://sstappnew.test/`
- **Database**: `SSTAPP_20260601` on `localhost` (MySQL via `mysqli` driver)
- **PHP requirement**: 5.6+ (7.x+ recommended)

## Running the Application

The app runs via Laragon's built-in Apache/Nginx server. Start Laragon and the site is served automatically at `http://sstappnew.test/`. No build step is needed — PHP is interpreted directly.

Environment is controlled via `CI_ENV` server variable (defaults to `development`), configured in `index.php`.

## MVC Routing

CodeIgniter 3 uses convention-based routing: `http://sstappnew.test/controller/method/param`.

- Controllers live in `application/controllers/` and extend `CI_Controller`
- Models live in `application/models/` and extend `CI_Model`
- Views live in `application/views/`
- Default controller is `Welcome` (set in `application/config/routes.php`)
- `index_page` is blank — clean URLs are active via `.htaccess` (no `index.php` in URLs)

Custom routes are defined in `application/config/routes.php`. Subdirectory controllers follow `application/controllers/subdir/Controller.php` → URL `/subdir/controller/method`.

## Key Configuration Files

| File | Purpose |
|------|---------|
| `application/config/config.php` | Base URL, encryption key, session settings |
| `application/config/database.php` | DB credentials (localhost, `ingenieria` user) |
| `application/config/routes.php` | URL routing rules |
| `application/config/autoload.php` | Libraries/helpers loaded on every request |

To enable autoloaded libraries (database, session, etc.), edit `$autoload['libraries']` in `autoload.php`.

## Database

Uses CodeIgniter's Query Builder. Load the DB manually in a controller/model:
```php
$this->load->database();
```
Or add `'database'` to `$autoload['libraries']` in `autoload.php` to auto-connect on every request.

Query Builder example:
```php
$query = $this->db->get('table_name');
$result = $query->result();
```

## Code Style

- **Indentation**: Tabs (see `.editorconfig`)
- **Line endings**: LF
- **Charset**: UTF-8
- Every controller/model file must start with: `defined('BASEPATH') OR exit('No direct script access allowed');`

## Tests

PHPUnit is listed as a dev dependency in `composer.json` (versions 4.*, 5.*, or 9.*). No test suite is configured yet. To run tests once configured:
```bash
composer run test:coverage
```
