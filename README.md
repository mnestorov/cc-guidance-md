# 🤖 AI Development Assistant

### CLAUDE.md File
This project includes a comprehensive `CLAUDE.md` file designed to guide AI development assistants (specifically Claude Code from Anthropic) when working with the codebase.

**What it does:**
- **Project Context**: Provides complete understanding of the WordPress project structure
- **Coding Standards**: Defines PHP, TypeScript, and SCSS development standards
- **Architecture Guide**: Explains monorepo structure and component organization
- **Command Reference**: Lists all available development commands
- **Best Practices**: Outlines security, performance, and WordPress-specific guidelines
- **Code Examples**: Includes practical examples for common development tasks

**Why it's useful:**
- Ensures consistent code quality when working with AI assistants
- Reduces onboarding time for new developers
- Maintains project-specific standards and conventions
- Provides quick reference for complex development workflows

The file serves as a "developer handbook" that enables AI tools to understand the project's unique architecture, coding standards, and development practices, resulting in more accurate and contextually appropriate code suggestions and implementations.

## 🚀 Deployment

### Production Build
```bash
# Build all assets for production
pnpm build

# Optional: Clean and rebuild
pnpm deps:clean:all
pnpm deps:install
pnpm build
```

### Environment Configuration
- Copy `wp-config-sample.php` to `wp-config.php`
- Configure database credentials
- Set up Redis cache configuration
- Configure SMTP settings for email

## 📊 Performance Features

- **Redis Object Caching**: Full-page and object caching
- **Image Optimization**: EWWW Image Optimizer integration
- **Asset Optimization**: Minified and concatenated CSS/JS
- **Lazy Loading**: Images and content optimization
- **Database Optimization**: Efficient queries and indexing

## 🌍 Multi-language Support

- **Polylang Integration**: Complete multi-language setup
- **Translation Ready**: All strings properly internationalized
- **RTL Support**: Right-to-left language compatibility
- **SEO Optimized**: Proper hreflang and meta tag implementation

## 📝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Follow the coding standards defined in `CLAUDE.md`
4. Run linting and tests (`pnpm lint && pnpm format`)
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

## 📞 Support

For development questions or issues:
- Review the `CLAUDE.md` file for detailed development guidance
- Check the WordPress Codex for WordPress-specific questions
- Refer to the build tool documentation (@wordpress/scripts)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

Built with ❤️ using modern WordPress development practices
