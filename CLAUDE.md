# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Development Environment

- `composer dev` - Start full development environment (Laravel server, queue worker, logs, and Vite)
- `php artisan serve` - Start Laravel development server only
- `npm run dev` - Start Vite development server for frontend assets

### Testing

- `composer test` - Run all tests (static analysis + Pest tests)
- `composer test:pest` - Run Pest tests only
- `composer test:static` - Run all static analysis (format, lint, Pint, PHPStan, Rector)
- `composer test:phpstan` - Run PHPStan static analysis
- `composer test:pint` - Check PHP code style with Laravel Pint
- `composer test:rector` - Check for automated refactoring opportunities

### Code Quality

- `composer pint:fix` - Fix PHP code style issues with Laravel Pint
- `composer rector:fix` - Apply automated refactoring with Rector
- `npm run lint:fix` - Fix JavaScript/CSS linting issues
- `npm run format:fix` - Fix code formatting with Prettier

### Building

- `npm run build` - Build frontend assets for production

## Architecture Overview

### Laravel + Filament Admin Panel

This is a Laravel 12 application with Filament v4 admin panel. The project uses:

- **Laravel Breeze** for authentication scaffolding
- **Filament Admin** for backend administration
- **Pest** for testing framework
- **Tailwind CSS v4** for styling

### Key Directories

- `app/Filament/Admin/Resources/` - Filament admin panel resources and schemas
- `app/Http/Controllers/Auth/` - Laravel Breeze authentication controllers
- `routes/web.php` - Main web routes (home page and authenticated routes)
- `routes/auth.php` - Authentication routes from Laravel Breeze

### Filament Resource Structure

Filament resources follow a modular pattern with separate schema files:

- `UserResource.php` - Main resource definition
- `Schemas/UserForm.php` - Form configuration
- `Schemas/UserInfolist.php` - View/detail configuration
- `Tables/UsersTable.php` - Table configuration
- `Pages/` - Resource page implementations

### Frontend Stack

- **Vite** for asset bundling
- **Alpine.js** for JavaScript interactions
- **Tailwind CSS v4** with PostCSS
- **Prettier** with Blade template support for formatting

### Quality Tools

- **PHPStan** (Larastan) for static analysis with 2GB memory limit
- **Laravel Pint** for PHP code style (Laravel's PSR-12 implementation)
- **Rector** with Laravel rules for automated refactoring
- **ESLint** + **Prettier** for JavaScript/CSS quality

## Development Workflow

### Running the Application

Use `composer dev` to start the full development environment which includes:

- Laravel development server
- Queue worker with retry limit of 1
- Real-time log monitoring via Laravel Pail
- Vite development server for hot reloading

### Testing Strategy

**CRITICAL**: Always run `composer test:static` after making any code changes. This runs all static analysis checks:

1. Code formatting compliance (Prettier, Pint)
2. Linting passes (ESLint)
3. Static analysis passes (PHPStan)
4. No Rector refactoring suggestions

Run the full test suite with `composer test` before committing changes to also include Pest tests.

### Database

Uses SQLite for development (database/database.sqlite). Migrations are automatically run during project setup.

## Commit Messages

Write clear, concise git commit messages following conventional commit format.

### Guidelines

- Use conventional commit format: `<type>(<scope>): <subject>`
- Write subject line in imperative mood (e.g., "fix bug", not "fixed bug")
- Keep subject line lowercase except for proper nouns and acronyms
- Limit subject line to 72 characters maximum
- Omit commit message body - keep commits concise
- Do not end subject line with a period

### Commit Types - Rule of Thumb

Choose the type based on the **primary intent** of your change:

| Type       | Rule of Thumb                                         | Description                              |
| ---------- | ----------------------------------------------------- | ---------------------------------------- |
| `feat`     | Does this introduce a new user-facing capability?     | New features users can see/interact with |
| `fix`      | Does this correct an error impacting user experience? | Bug fixes and error corrections          |
| `style`    | Does this only affect visual presentation/formatting? | Cosmetic changes, code formatting        |
| `refactor` | Does this restructure code without changing behavior? | Internal improvements for readability    |
| `perf`     | Does this specifically make the app faster/efficient? | Performance optimizations                |
| `test`     | Does this involve only test-related changes?          | Adding/modifying automated tests         |
| `build`    | Does this relate to build system or dependencies?     | Build configuration, dependency updates  |
| `ci`       | Does this only affect CI configuration/scripts?       | Continuous Integration changes           |
| `docs`     | Does this only affect documentation files?            | Documentation updates                    |
| `chore`    | Is this maintenance not modifying source/test files?  | Routine maintenance tasks                |
