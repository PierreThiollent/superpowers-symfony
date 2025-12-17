# Superpowers Symfony

A Claude Code plugin providing Symfony-specific guidance, skills, and workflows. This plugin enhances your development experience with TDD support, Doctrine guidance, API Platform patterns, and best practices for Symfony 6.4 LTS, 7.x, and 8.0.

## Features

- **TDD Workflows** - RED-GREEN-REFACTOR with Pest PHP or PHPUnit
- **Doctrine Mastery** - Relations, migrations, transactions, Foundry fixtures
- **API Platform** - Resources, filters, serialization, versioning
- **Symfony Messenger** - Async processing, handlers, retry strategies
- **Security** - Voters for granular authorization
- **Architecture** - Hexagonal/Ports & Adapters, DI patterns
- **Quality** - PHP-CS-Fixer, PHPStan integration
- **Docker Support** - Docker Compose standard + Symfony Docker (FrankenPHP)

## Installation

```bash
# From Claude Code marketplace
claude plugins install superpowers-symfony

# Or manually
git clone https://github.com/your-org/superpowers-symfony ~/.claude/plugins/superpowers-symfony
```

## Usage

### Interactive Commands

```bash
/superpowers-symfony:brainstorm       # Start brainstorming session
/superpowers-symfony:write-plan       # Create implementation plan
/superpowers-symfony:execute-plan     # Execute plan with TDD
/superpowers-symfony:symfony-check    # Run quality checks
/superpowers-symfony:symfony-tdd-pest # TDD with Pest
```

### Skills

Skills are automatically suggested based on context. You can also invoke them directly:

- `symfony:tdd-with-pest` - TDD workflow with Pest PHP
- `symfony:tdd-with-phpunit` - TDD workflow with PHPUnit
- `symfony:doctrine-relations` - Entity relationships guide
- `symfony:doctrine-migrations` - Migration management
- `symfony:symfony-messenger` - Async message handling
- `symfony:api-platform-resources` - API Platform configuration
- `symfony:api-platform-state-providers` - State Providers & Processors
- `symfony:api-platform-dto-resources` - DTO-based API Resources
- `symfony:symfony-voters` - Authorization with voters
- `symfony:quality-checks` - Code quality tools

## Supported Versions

| Framework | Version | Status |
|-----------|---------|--------|
| Symfony | 6.4 LTS | Supported |
| Symfony | 7.x | Supported |
| Symfony | 8.0 | Supported |
| API Platform | 3.x | Supported |
| API Platform | 4.x | Supported |

## Docker Support

The plugin automatically detects your Docker setup:

### Symfony Docker (FrankenPHP)

```bash
# Detected via compose.yaml with frankenphp
docker compose exec php bin/console
```

### Docker Compose Standard

```bash
# Detected via docker-compose.yml
docker compose exec app bin/console
```

### Host Environment

```bash
# Fallback when no Docker detected
php bin/console
```

## Project Structure

```
superpowers-symfony/
├── .claude-plugin/
│   └── plugin.json          # Plugin configuration
├── .github/
│   └── workflows/           # CI/CD automation
│       ├── validate-skills.yml
│       └── test-session-start.yml
├── docs/
│   └── symfony/             # Framework documentation
│       ├── api-platform.md
│       ├── state-providers-processors.md
│       └── dto-resources.md
├── skills/                   # Skill definitions (49 skills)
│   ├── tdd-with-pest/
│   ├── doctrine-relations/
│   ├── symfony-messenger/
│   ├── api-platform-state-providers/   # NEW
│   ├── api-platform-dto-resources/     # NEW
│   └── ...
├── commands/                 # Slash commands
│   ├── brainstorm.md
│   ├── write-plan.md
│   └── ...
├── hooks/
│   ├── hooks.json           # Hook configuration
│   └── session-start.sh     # Auto-detection script
├── scripts/
│   └── validate_skills.ts   # Validation script
├── RELEASE-NOTES.md         # Version history
└── LICENSE
```

## Skills Categories

### Onboarding & Configuration
- `using-symfony-superpowers` - Entry point
- `runner-selection` - Docker vs Host
- `bootstrap-check` - Project verification

### Testing
- `tdd-with-pest` - Pest PHP workflow
- `tdd-with-phpunit` - PHPUnit workflow
- `functional-tests` - WebTestCase guide

### Doctrine
- `doctrine-relations` - Entity relationships
- `doctrine-migrations` - Schema versioning
- `doctrine-fixtures-foundry` - Test data factories
- `doctrine-transactions` - Transaction handling

### API Platform
- `api-platform-resources` - Resource configuration
- `api-platform-filters` - Search and filtering
- `api-platform-serialization` - Serialization groups
- `api-platform-state-providers` - Custom State Providers & Processors
- `api-platform-dto-resources` - DTO-based API Resources

### Messenger & Async
- `symfony-messenger` - Message handling
- `messenger-retry-failures` - Error handling

### Security
- `symfony-voters` - Authorization logic
- `form-types-validation` - Form validation
- `rate-limiting` - Rate limiter

### Architecture
- `interfaces-and-autowiring` - DI patterns
- `ports-and-adapters` - Hexagonal architecture
- `strategy-pattern` - Tagged services

### Quality
- `quality-checks` - PHP-CS-Fixer, PHPStan
- `symfony-cache` - Caching strategies

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add/modify skills in `skills/` directory
4. Run validation: `npx tsx scripts/validate_skills.ts`
5. Submit a pull request

### Skill Format

Each skill is a directory with a `SKILL.md` file:

```markdown
---
name: symfony:skill-name
description: Brief description of the skill
---

# Skill Title

Content with code examples, best practices, etc.
```

## License

MIT License - see [LICENSE](LICENSE) for details.

## Acknowledgments

Inspired by [superpowers-laravel](https://github.com/jpcaparas/superpowers-laravel) by JP Caparas.

## Support

- Issues: [GitHub Issues](https://github.com/your-org/superpowers-symfony/issues)
- Discussions: [GitHub Discussions](https://github.com/your-org/superpowers-symfony/discussions)
