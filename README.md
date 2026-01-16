# nonfiction-book-chat

Agent-neutral skill for grounded Q&A over local non-fiction ebooks. It extracts text from local EPUB/PDF files, retrieves relevant passages, and produces cited, multi-paragraph answers that synthesize concepts across chapters. Designed for Socratic exploration with follow-up prompts.

## What this skill does
- Answers using only the provided books; refuses unrelated or speculative content
- Retrieves from extracted text files 
- Produces chapter/section-cited explanations with cross-chapter synthesis
- Supports a "deep" mode for long-form, anecdote-rich responses
- Ends with 3-5 "Rabbit holes" to invite further questions

## Usage
- Add the book (EPUB/PDF) to the folder, and then open your favourite agent CLI, either Codex, Claude Code, etc..
- Ask your question (engage in a socratic dialogue to learn concepts deeper)
- Include the word "deep" to force a 6-12 paragraph, anecdote-rich response from the agents

## Behavior details
- Quick factual questions are answered briefly with citations
- Interpretive/analytical questions default to 6-12 paragraphs
- Single-book responses cite the title once, then use chapter/section-only citations
- Multi-book responses cite each book/section as used

## Example prompt
"deep: What is Kathryn's leadership style in The Five Dysfunctions of a Team, and how does it evolve across the story?"

## Agent Skills compatibility
This skill follows the Agent Skills format (SKILL.md with YAML frontmatter plus optional resources). It should work across agent platforms that support the format.

## Installation
### Non-technical quick install (ask your agent)
If you prefer to use your agent instead of the terminal, copy/paste one of these prompts and fill in the folder path. Replace `/chat` with whatever chat command your agent uses.

Codex CLI:
```
/chat Please install the nonfiction-book-chat skill from this folder:
/Users/yourname/Downloads/nonfiction-book-chat
Then add it to my AGENTS.md.
```

Claude Code:
```
/chat Install the nonfiction-book-chat skill from this folder:
/Users/yourname/Downloads/nonfiction-book-chat
Then add it to my project's AGENTS.md.
```

GitHub Copilot (in a repo):
```
/chat Add the nonfiction-book-chat skill instructions to this repo by copying SKILL.md to .github/copilot-instructions.md.
```

If your agent has a `/skills` command, you can also ask it to “install a skill from a local folder” and give the same path.

### Codex
```bash
# From the repo root
mkdir -p "$CODEX_HOME/skills"
cp -R . "$CODEX_HOME/skills/nonfiction-book-chat"
```
Add or update your `AGENTS.md` to include the skill entry pointing at `$CODEX_HOME/skills/nonfiction-book-chat/SKILL.md`.

### Claude Code
Claude Code supports Agent Skills when they are listed in your project `AGENTS.md` and the skill folder is on disk.
```bash
# Put the skill in a shared skills directory you use for Claude Code
mkdir -p "$HOME/.claude/skills"
cp -R . "$HOME/.claude/skills/nonfiction-book-chat"
```
Then reference the skill in your project `AGENTS.md` with the path to `~/.claude/skills/nonfiction-book-chat/SKILL.md`.

### GitHub Copilot
Copilot does not currently consume Agent Skills directly. Use the SKILL.md contents as instructions:
```bash
mkdir -p .github
cp SKILL.md .github/copilot-instructions.md
```
Keep the skill folder next to your books so Copilot can follow the extraction/retrieval steps.

## Files
- SKILL.md: primary instructions and workflow

## Packaging
Use the Agent Skills reference library or CLI to validate and package.

## License
MIT
