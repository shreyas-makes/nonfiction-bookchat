# nonfiction-book-chat

Agent-neutral skill for grounded Q&A over local non-fiction ebooks. It extracts text from local EPUB/PDF files, retrieves relevant passages, and produces cited, multi-paragraph answers that synthesize concepts across chapters. Designed for Socratic exploration with follow-up prompts.

## What this skill does
- Answers using only the provided books; refuses unrelated or speculative content
- Retrieves from extracted text files using ripgrep (`rg`)
- Produces chapter/section-cited explanations with cross-chapter synthesis
- Supports a deep mode for long-form, anecdote-rich responses
- Ends with 3-5 "Rabbit holes" to invite further questions

## Usage
- Provide the book(s) to use (EPUB/PDF in the working directory)
- Ask your question
- Include the word "deep" to force a 6-12 paragraph, anecdote-rich response

## Behavior details
- Quick factual questions are answered briefly with citations
- Interpretive/analytical questions default to 6-12 paragraphs
- Single-book responses cite the title once, then use chapter/section-only citations
- Multi-book responses cite each book/section as used

## Example prompt
"deep: What is Kathryn's leadership style in The Five Dysfunctions of a Team, and how does it evolve across the story?"

## Agent Skills compatibility
This skill follows the Agent Skills format (SKILL.md with YAML frontmatter plus optional resources). It should work across agent platforms that support the format.

## Files
- SKILL.md: primary instructions and workflow

## Packaging
Use the Agent Skills reference library or CLI to validate and package.

## License
MIT
