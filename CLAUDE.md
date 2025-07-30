# CLAUDE.md

This file provides comprehensive guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Introduction

You are an expert in WordPress, PHP, modern web development technologies, and this specific WordPress project architecture. This project uses a monorepo structure with pnpm workspaces for efficient development and asset management.

## Core Development Principles

- **Code Quality**: Write concise, technical responses with accurate PHP examples and TypeScript implementations
- **WordPress Standards**: Strictly follow WordPress coding standards and best practices
- **Modern PHP**: Leverage PHP 8.2+ features (typed properties, arrow functions, enums, readonly properties)
- **Modularity**: Use object-oriented programming with dependency injection and single responsibility principle
- **Security First**: Implement proper sanitization, validation, nonces, and capability checks
- **Performance**: Optimize for speed, use caching strategies, and minimize database queries
- **Maintainability**: Write self-documenting code with clear naming conventions and comprehensive documentation

## PHP/WordPress Development Standards

### Modern PHP Features

```php
<?php
declare(strict_types=1);

namespace MyThemeName\Theme\Core;

class ExampleClass {
    public function __construct(
        private readonly string $option,
        private array $config = []
    ) {}
}
```

### Code Organization

- **Namespace**: All theme code uses `MyThemeName\Theme\{Namespace}`
- **PSR-4 Autoloading**: Classes auto-loaded via Composer
- **File Structure**: Follow WordPress theme/plugin directory conventions
- **Naming**: Use descriptive function, variable, and file names
- **Directories**: Lowercase with hyphens (e.g., `wp-content/themes/my-theme`)

### Error Handling & Logging

```php
try {
    // Risky operation
} catch (Exception $e) {
    error_log('Error in ' . __METHOD__ . ': ' . $e->getMessage());
    // Handle gracefully
}
```

### Database Operations

```php
// Always use prepared statements
$results = $wpdb->get_results(
    $wpdb->prepare(
        "SELECT * FROM {$wpdb->posts} WHERE post_status = %s AND post_date > %s",
        'publish',
        $date
    )
);
```

## WordPress Best Practices

### Security Implementation

- **Data Validation**: Use `sanitize_*()` and `wp_unslash()` functions
- **Output Escaping**: Always escape output with `esc_*()` functions
- **Nonce Verification**: Implement for all form submissions
- **Capability Checks**: Verify user permissions before sensitive operations
- **SQL Injection Prevention**: Use `$wpdb->prepare()` for all queries

### Performance Optimization

- **Caching**: Utilize WordPress transients API and Redis integration
- **Asset Management**: Use `wp_enqueue_script()` and `wp_enqueue_style()`
- **Database Optimization**: Minimize queries, use `WP_Query` efficiently
- **Background Processing**: Implement `wp_cron()` for heavy operations

### WordPress APIs

- **Hooks System**: Prefer actions/filters over core modifications
- **Custom Post Types**: Use `register_post_type()` with proper arguments
- **Options API**: Store configuration using `get_option()`/`update_option()`
- **REST API**: Implement custom endpoints when needed
- **Internationalization**: Use `__()`, `_e()`, `_n()` functions with domain `mythemename`

## Frontend Development

### SCSS/CSS Standards

- **NO `!important`**: Use proper CSS specificity and cascade
- **Component Architecture**: Organize styles by components in `assets/src/scss/`
- **BEM Methodology**: Use Block-Element-Modifier naming convention
- **Mobile First**: Write responsive CSS starting from mobile breakpoints

### TypeScript Development

- **Type Safety**: Use strict TypeScript configuration
- **Interfaces**: Define clear interfaces for data structures
- **DOM Manipulation**: Type DOM elements properly
- **Modules**: Use ES6 imports/exports consistently

### Asset Structure

```text
assets/
├── src/
│   ├── scss/
│   │   ├── basics/        # Reset, typography, base styles
│   │   ├── components/    # Reusable UI components
│   │   ├── helpers/       # Utility classes
│   │   ├── mixins/        # SCSS mixins and functions
│   │   └── templates/     # Page-specific styles
│   └── ts/
│       ├── types/         # TypeScript definitions
│       ├── components/    # JavaScript components
│       └── utils/         # Utility functions
└── dist/                  # Built assets (auto-generated)
```

## Project Architecture

### Monorepo Structure

```text
root/
├── frontend/
│   ├── wp/                    # WordPress core
│   └── wp-content/
│       ├── themes/mythemename/    # Main theme
│       └── plugins/mythemename*/  # Custom plugins
├── wp-scripts/                # Build configuration
└── package.json               # Workspace configuration
```

### Theme Architecture

- **Namespace**: `MyThemeName\Theme`
- **Build Tool**: `@wordpress/scripts` with custom webpack config
- **Translation Domain**: `mythemename`
- **PHP Version**: 8.3+ required

### Key Theme Directories

```text
themes/mythemename/
├── includes/
│   ├── Admin/         # Admin-specific functionality
│   ├── Core/          # Core theme functionality
│   ├── Helpers/       # Utility classes and functions
│   ├── Markup/        # HTML generation classes
│   └── Plugins/       # Plugin integration
├── partials/          # Reusable PHP template parts
├── template-parts/    # WordPress template hierarchy parts
├── patterns/          # Block patterns
├── languages/         # Translation files
└── assets/            # Source and built assets
```

## Development Commands

### Essential Commands

```bash
# Development
pnpm start              # Start development with hot reloading
pnpm build:dev          # Build for development
pnpm build              # Build for production

# Quality Assurance
pnpm lint               # Run all linting
pnpm lint:fix           # Auto-fix linting issues
pnpm format             # Check code formatting
pnpm format:fix         # Fix formatting
dip sniff-fix [path]    # PHP CodeSniffer fixes

# Dependencies
pnpm deps:install       # Install all dependencies
pnpm deps:clean:all     # Clean all node_modules

# WordPress CLI (always prefix with 'dip')
dip wp cache flush      # Clear WordPress cache
dip wp db export        # Export database
```

### Workspace-Specific Commands

```bash
# Theme workspace
pnpm --filter="theme-bundler" run build
pnpm --filter="theme-bundler" run start

# Plugin workspace  
pnpm --filter="plugin-bundler" run build

# Translations
pnpm translate:theme    # Generate theme translation files
```

## Development Workflows

### Creating New Components

1. **SCSS Component**:

   ```scss
   // assets/src/scss/components/_component-name.scss
   .component-name {
     // Component styles
     
     &__element {
       // Element styles
     }
     
     &--modifier {
       // Modifier styles
     }
   }
   ```

2. **PHP Class**:

   ```php
   <?php
   declare(strict_types=1);
   
   namespace MyThemeName\Theme\Components;
   
   class ComponentName {
       public function render(array $args = []): string {
           // Component logic
       }
   }
   ```

3. **TypeScript Module**:

   ```typescript
   interface ComponentOptions {
       element: HTMLElement;
       config?: Record<string, unknown>;
   }
   
   export class ComponentName {
       constructor(private options: ComponentOptions) {}
   }
   ```

### Testing Approach

- **PHP**: Use WordPress's `WP_UnitTestCase` for unit tests
- **JavaScript**: Jest testing framework (via @wordpress/scripts)
- **Manual Testing**: Use local development environment with Docker

### Translation Workflow

1. Use translation functions: `__()`, `_e()`, `_n()` with domain `mythemename`
2. Generate POT file: `pnpm translate:theme`
3. Translate using Poedit or similar tool
4. JSON files auto-generated for JavaScript translations

## Integration Points

### Plugin Dependencies

- **Carbon Fields**: Custom fields and meta boxes
- **Polylang**: Multi-language support
- **Yoast SEO**: Search engine optimization
- **Redis Cache**: Object caching
- **EWWW Image Optimizer**: Image optimization

### Third-Party Libraries

- **Swiper**: Carousel and slider components
- **jQuery**: Legacy support (minimize usage)
- **React**: WordPress block development

## Performance Considerations

### Database Optimization

- Use `WP_Query` with proper arguments
- Implement pagination with `paginate_links()`
- Cache expensive queries with transients
- Use `wp_cache_*()` functions for object caching

### Asset Optimization

- Minimize HTTP requests through bundling
- Use image sprites where appropriate
- Implement lazy loading for images
- Optimize critical CSS path

### Caching Strategy

```php
// Transient caching example
$cache_key = 'expensive_operation_' . md5($params);
$data = get_transient($cache_key);

if (false === $data) {
    $data = expensive_operation($params);
    set_transient($cache_key, $data, HOUR_IN_SECONDS);
}
```

## Troubleshooting

### Common Issues

- **Build Errors**: Clear `node_modules` and reinstall dependencies
- **PHP Errors**: Check WordPress debug logs
- **Asset Loading**: Verify enqueue hooks and dependencies
- **Translation Missing**: Regenerate POT files and JSON translations

### Debug Mode

```php
// wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

## Code Review Checklist

- [ ] Security: All inputs sanitized, outputs escaped
- [ ] Performance: No N+1 queries, appropriate caching
- [ ] Standards: Follows WordPress coding standards
- [ ] Types: PHP and TypeScript properly typed
- [ ] Tests: Unit tests written for complex logic
- [ ] Documentation: Code properly documented
- [ ] Accessibility: WCAG 2.1 AA compliance
- [ ] Internationalization: All strings properly translated
