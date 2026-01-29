# Superpowers Symfony

A Claude Code plugin providing Symfony-specific guidance, skills, and workflows. This plugin enhances your development experience with TDD support, Doctrine guidance, and best practices for Symfony 6.4 LTS, 7.x, and 8.0.

## Features

- **TDD Workflows** - RED-GREEN-REFACTOR with PHPUnit
- **Doctrine Mastery** - Relations, migrations, transactions, Foundry fixtures
- **Symfony Messenger** - Async processing, handlers, retry strategies
- **Security** - Voters for granular authorization
- **Architecture** - Hexagonal/Ports & Adapters, DI patterns
- **Quality** - PHP-CS-Fixer, PHPStan integration
- **Docker Support** - Docker Compose standard + Symfony Docker (FrankenPHP)

**Complexity tiers**: See `docs/complexity-tiers.md` for simple/medium/complex examples and how to adapt output.

## Installation

```bash
# From Claude Code marketplace
claude plugins install superpowers-symfony

# Or manually
git clone https://github.com/MakFly/superpowers-symfony ~/.claude/plugins/superpowers-symfony
```

### Enable plugin (Claude + GLM)

```json
// ~/.claude/settings.json
{
  "enabledPlugins": {
    "superpowers-symfony@custom": true
  }
}
```

```json
// ~/.claude-glm/.claude.json
{
  "enabledPlugins": {
    "superpowers-symfony@custom": true
  }
}
```

Restart Claude Code.

### Fallback: symlink skills (if plugin skills don’t load)

```bash
ln -s ~/.claude/plugins/superpowers-symfony/skills/doctrine-relations ~/.claude/skills/symfony-doctrine-relations
```

Then call:
```
Use the skill symfony:doctrine-relations
```

### Troubleshooting (Unknown skill)

If you see `Unknown skill`:
1. Restart Claude Code.
2. Run `What skills are available?` to confirm the plugin is loaded.
3. Ensure `enabledPlugins` includes `superpowers-symfony@custom` in both configs.
4. Use the fallback symlink if the plugin still does not expose skills.

## How to Use Skills

Skills are markdown files containing expert knowledge about specific Symfony topics. Since this plugin uses a custom skill system (not Claude Code's native Skill tool), here are the different ways to use them.

### Calling a Skill

To invoke a skill, simply ask Claude using one of these patterns:

```bash
# Basic syntax
Use the skill symfony:<skill-name>

# Examples
Use the skill symfony:tdd-with-phpunit
Use the skill symfony:doctrine-relations
```

**Quick Reference:**
| What you type | What happens |
|---------------|--------------|
| `Apply symfony:doctrine-relations` | Claude reads and applies Doctrine relations patterns |

### Method 1: Ask Claude Directly (Recommended)

Simply ask Claude to use a specific skill in your conversation:

```
Use the skill symfony:tdd-with-phpunit and help me write tests for my UserService

Apply the symfony:doctrine-relations skill to design my e-commerce entities
```

Claude will read the skill file from `~/.claude/plugins/superpowers-symfony/skills/` and apply its knowledge to your request.

### Method 2: Copy Commands to Your Project

Copy the plugin's slash commands to your project for quick access:

```bash
# Create commands directory in your project
mkdir -p .claude/commands

# Copy all superpowers commands
cp ~/.claude/plugins/superpowers-symfony/commands/*.md .claude/commands/

# Or copy specific commands
cp ~/.claude/plugins/superpowers-symfony/commands/symfony-tdd-phpunit.md .claude/commands/
```

Then use them with:
```
/symfony-tdd-phpunit
/symfony-check
/write-plan
```

### Method 3: Reference in Project CLAUDE.md (Not recommended)

Avoid `@` file references in `CLAUDE.md` because they force-load large files and increase context usage. Prefer explicit skill invocation instead:

```
Use the skill symfony:tdd-with-phpunit
Use the skill symfony:doctrine-relations
```

### Method 4: Direct Skill Path Reference

Ask Claude to read a specific skill file:

```
Read and apply ~/.claude/plugins/superpowers-symfony/skills/symfony-voters/SKILL.md

Load the skill at ~/.claude/plugins/superpowers-symfony/skills/quality-checks/SKILL.md
and run the checks on my project
```

## Usage Examples

### Example 1: Doctrine Relations

```
User: Apply symfony:doctrine-relations - I need User, Order, and Product entities

Claude: [Reads doctrine-relations skill]
        Let me design the relationships:

        - User (1) <-> (N) Order (OneToMany)
        - Order (N) <-> (N) Product via OrderItem (ManyToMany with pivot)
        - Product (N) <-> (N) Category (ManyToMany)
```

### Example 3: Quality Checks

```
User: Use the quality-checks skill to analyze my codebase

Claude: [Reads quality-checks skill]
        Running quality checks:

        1. PHP-CS-Fixer (code style)
        2. PHPStan level 8 (static analysis)
        3. Psalm (type coverage)

        [Executes checks and reports issues]
```

### Example 4: Combining Multiple Skills

```
User: I want to build a blog with posts and comments.
      Use these skills: doctrine-relations, tdd-with-phpunit

Claude: [Reads both skills]
        Let me combine these patterns:

        1. First, I'll design the entity relationships (doctrine-relations)
        2. Then write tests using TDD (tdd-with-phpunit)
```

## Available Skills

### Onboarding & Configuration
| Skill | Description |
|-------|-------------|
| `using-symfony-superpowers` | Entry point and overview |
| `runner-selection` | Docker vs Host environment detection |
| `bootstrap-check` | Project verification and setup |

### Testing
| Skill | Description |
|-------|-------------|
| `tdd-with-phpunit` | TDD workflow with PHPUnit |
| `functional-tests` | WebTestCase for HTTP testing |
| `test-doubles-mocking` | Mocks, stubs, and fakes |
| `e2e-panther-playwright` | End-to-end browser testing |

### Doctrine ORM
| Skill | Description |
|-------|-------------|
| `doctrine-relations` | Entity relationships (1:1, 1:N, N:N) |
| `doctrine-migrations` | Schema versioning |
| `doctrine-fixtures-foundry` | Test data factories |
| `doctrine-transactions` | Transaction handling |
| `doctrine-batch-processing` | Bulk operations |
| `doctrine-fetch-modes` | Performance optimization |

### Messenger & Async
| Skill | Description |
|-------|-------------|
| `symfony-messenger` | Message handling basics |
| `messenger-retry-failures` | Error handling and retries |
| `symfony-scheduler` | Scheduled tasks |

### Security
| Skill | Description |
|-------|-------------|
| `symfony-voters` | Authorization logic |
| `form-types-validation` | Form and validation |
| `rate-limiting` | Rate limiter configuration |

### Architecture
| Skill | Description |
|-------|-------------|
| `interfaces-and-autowiring` | Dependency injection |
| `ports-and-adapters` | Hexagonal architecture |
| `strategy-pattern` | Tagged services pattern |
| `cqrs-and-handlers` | Command/Query separation |
| `value-objects-and-dtos` | Value objects design |

### Quality & Performance
| Skill | Description |
|-------|-------------|
| `quality-checks` | PHP-CS-Fixer, PHPStan |
| `symfony-cache` | Caching strategies |
| `controller-cleanup` | Thin controllers pattern |

## Slash Commands

Available commands (copy to `.claude/commands/` to use):

| Command | Description |
|---------|-------------|
| `brainstorm.md` | Start a brainstorming session |
| `write-plan.md` | Create an implementation plan |
| `execute-plan.md` | Execute plan with TDD |
| `symfony-check.md` | Run quality checks |
| `symfony-tdd-phpunit.md` | TDD workflow with PHPUnit |
| `symfony-migrations.md` | Doctrine migrations helper |
| `symfony-fixtures.md` | Generate test fixtures |
| `symfony-doctrine-relations.md` | Design entity relations |
| `symfony-voters.md` | Implement authorization |
| `symfony-messenger.md` | Setup async messaging |
| `symfony-cache.md` | Configure caching |

## Supported Versions

| Framework | Version | Status |
|-----------|---------|--------|
| Symfony | 6.4 LTS | Supported |
| Symfony | 7.x | Supported |
| Symfony | 8.0 | Supported |

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
├── skills/                   # Skill definitions (34 skills)
│   ├── doctrine-relations/
│   │   └── SKILL.md
│   └── ...
├── commands/                 # Slash commands
│   ├── brainstorm.md
│   ├── write-plan.md
│   └── ...
├── docs/
│   └── symfony/             # Additional documentation
├── hooks/
│   ├── hooks.json           # Hook configuration
│   └── session-start.sh     # Auto-detection script
├── scripts/
│   └── validate_skills.ts   # Validation script
├── RELEASE-NOTES.md         # Version history
└── LICENSE
```

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

- Issues: [GitHub Issues](https://github.com/MakFly/superpowers-symfony/issues)
- Discussions: [GitHub Discussions](https://github.com/MakFly/superpowers-symfony/discussions)
