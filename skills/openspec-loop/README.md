# OpenSpec Subagent-Driven Development

A Claude Code skill for systematically implementing OpenSpec change proposals through **fresh subagents at each iteration**.

Inspired by the [Ralph](https://ghuntley.com/ralph/) Technique and Jesse Vincent's [Superpowers](https://github.com/obra/superpowers) skill collection.

## What is this?

The key insight: **A fresh subagent for each spec means clean context, no contamination, better results.**

Traditional approaches accumulate context across multiple specs, leading to confusion and lower quality. This skill takes the opposite approach:

1. **Dispatch a completely fresh subagent** for each spec
2. **Subagent starts with `/clear`** - guaranteed clean slate
3. **Subagent implements one spec** - focused attention
4. **Subagent terminates** - context is discarded
5. **Repeat** - next spec gets a fresh subagent

**Result:** Each spec is implemented with pristine context, as if it's the only thing that matters.

## When to Use

Use this skill when you have:
- Multiple OpenSpec change proposals to implement
- Specs that are independent changes (not tightly coupled)
- Need for clean context per spec to avoid confusion

**Don't use** if specs are tightly coupled or require shared context.

## Installation

### From Claude Plugin Marketplace

```bash
cd ~/.claude/skills
git clone https://github.com/viteinfinite/openspec-subagent-driven-development.git
```

### Direct Installation

```bash
mkdir -p ~/.claude/skills
cd ~/.claude/skills
git clone https://github.com/viteinfinite/openspec-subagent-driven-development.git
```

Restart Claude Code to load the skill.

## Usage

Simply invoke the skill when you want to implement OpenSpec specs:

```
Hey Claude, use OpenSpec Subagent-Driven Development to implement my pending specs
```

The skill will:
1. Run `openspec view` to discover active specs
2. Present the list to you for confirmation
3. For each spec (sequentially):
   - Dispatch a fresh general-purpose subagent
   - Subagent executes `/clear` for clean context
   - Subagent exports context usage tracking
   - Subagent applies the spec with `/openspec:apply [spec-id]`
   - Subagent implements all changes
   - Subagent archives the spec with `/openspec:archive [spec-id]`
   - Verify archiving succeeded
4. Provide implementation summary

## Example Workflow

```
You: I'm using OpenSpec Subagent-Driven Development to implement pending specs.

[Discovers 3 active specs]

Claude: Found 3 active specs:
  1. add-base-image-uploads
  2. add-strapi-tag-creation
  3. some-other-feature

You: Implement in this order: add-base-image-uploads, then add-strapi-tag-creation

Claude: Confirmed. Starting implementation...

=== Spec 1: add-base-image-uploads ===
[Dispatches subagent with clean context]
[Subagent implements changes]
[Subagent archives spec]

✅ add-base-image-uploads completed and archived

=== Spec 2: add-strapi-tag-creation ===
[Dispatches fresh subagent with clean context]
[Subagent implements changes]
[Subagent archives spec]

✅ add-strapi-tag-creation completed and archived

=== Summary ===
All requested specs implemented successfully:
  ✅ add-base-image-uploads
  ✅ add-strapi-tag-creation

Remaining: some-other-feature
```

## Key Benefits

### The Fresh Context Advantage

**The core benefit:** Each spec implementation starts from zero. No accumulated assumptions, no bleed-through from previous work, no context pollution.

Think of it like this:
- **Traditional approach:** One long conversation getting increasingly complex
- **This approach:** Fresh conversation per spec, clean mental model each time

**Why this matters:**
- **No confusion:** Subagent doesn't carry baggage from previous specs
- **No contamination:** Failed attempts don't pollute future implementations
- **Better quality:** Each spec gets full, focused attention as if it's the only task
- **Easier debugging:** Problems are isolated to specific specs
- **Clear boundaries:** When a subagent terminates, that spec's context is gone

### Additional Benefits

- Automatic context usage tracking per spec
- Spec archiving confirms completion
- Clear progress tracking
- Sequential execution prevents conflicts
- Clean audit trail per spec

## Requirements

This skill requires:
- **OpenSpec** - For managing change proposals
- **openspec:apply** skill - For applying specs to the workspace
- **openspec:archive** skill - For archiving completed specs
- **Context monitoring** - For tracking context usage per spec (path configurable)

## How It Works

Each subagent receives these instructions:

```
You are implementing a specific OpenSpec change proposal. Your workflow:

1. FIRST ACTION: Execute `/clear` to ensure clean context
2. SECOND ACTION: Export context usage tracking
3. THIRD ACTION: Execute `/openspec:apply [spec-id]` to apply the spec
4. Implement all changes described in the spec
5. After successful implementation, archive the spec
6. Report completion and terminate
```

## Error Handling

**If a subagent fails:**
- The failure is reported to you
- You choose whether to: retry with new subagent, skip to next spec, or abort
- Failure reason is documented

**If a spec cannot be applied:**
- Implementation stops and waits for your direction
- Explicit confirmation required before continuing

## Credits & Inspiration

This skill is inspired by:

- **[Ralph](https://github.com/ralphhq/ralph)** - The pioneering agentic coding framework that demonstrated the power of fresh context and clean delegation patterns
- **[Superpowers](https://github.com/coleam00/ottomator-agents)** - Particularly the `superpowers:subagent-driven-development` skill, which established the pattern of disciplined subagent workflows

This skill adapts those concepts specifically for OpenSpec workflows, with emphasis on:
- Fresh subagent per spec (Ralph's clean context principle)
- Sequential execution with isolation (Superpowers' disciplined delegation)
- Automated archiving and tracking (OpenSpec integration)

## Related Skills

- **superpowers:subagent-driven-development** - Original task-based workflow (use for non-OpenSpec tasks)

## License

MIT

## Contributing

Issues and pull requests welcome at the GitHub repository.
