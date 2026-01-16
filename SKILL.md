---
name: nonfiction-book-chat
description: Use local non-fiction ebooks to answer questions with grounded citations only from those books; refuse unrelated or speculative answers. Use when a user wants multi-paragraph, chapter-cited explanations that synthesize concepts across chapters while avoiding redundant single-book citations and weaving in concrete anecdotes from the text.
license: MIT
compatibility: agent-skills
---

# Non-fiction book chat
- Scope: Only use the provided non-fiction books; if a question is unrelated or the book lacks info, say so and do not improvise.
- Discovery: Ask which book(s) to use; list candidates with `ls *.epub *.pdf` in the working folder.
- Extraction (EPUB stdlib, no extra deps):
```bash
python - <<'PY'
import sys, zipfile, html
from html.parser import HTMLParser
from pathlib import Path

path = Path(sys.argv[1])
out = path.with_suffix('.txt')

class Stripper(HTMLParser):
    def __init__(self):
        super().__init__()
        self.parts = []
    def handle_data(self, d):
        self.parts.append(html.unescape(d))
    def get(self):
        return '\n'.join(self.parts)

with zipfile.ZipFile(path) as zf:
    texts = []
    for name in zf.namelist():
        if name.lower().endswith(('.xhtml', '.html', '.htm')):
            s = Stripper()
            s.feed(zf.read(name).decode('utf-8', 'ignore'))
            texts.append(s.get())
out.write_text('\n\n'.join(texts))
print(f'wrote {out}')
PY
python script_above.py "Book.epub"
```
- Extraction (PDF, if needed): prefer `pdftotext Book.pdf Book.txt` if available; otherwise explain the limitation.
- Retrieval: search the extracted `.txt` with `rg "term" Book.txt` to grab nearby paragraphs before answering.
- Answering rules:
  - Match depth to the question type: for quick factual questions, answer briefly with citations; for interpretive or analytical questions, write 6-12 paragraphs.
  - Treat the word "deep" in the user request as an explicit trigger for the 6-12 paragraph, anecdote-rich format.
  - In deep answers, ensure each paragraph advances the argument and connects ideas across chapters/sections.
  - Weave in concrete anecdotes or scenes from the book to anchor claims, without over-quoting.
  - Be associative: connect ideas across chapters/sections and explain how they relate or build on each other.
  - If the response draws from multiple chapters/sections, cite each chapter/section used for that paragraph's claims.
  - If only one book is used, avoid repeating the same book title in every citation; cite the book title once (first citation or lead line) and then use short chapter/section-only citations for the rest of the response.
  - End with 3-5 concise "Rabbit holes" as questions that invite further Socratic exploration.
  - Paraphrase rather than quote large blocks; keep answers within the book(s) asked; if confidence is low, say that more context is needed.
- Hygiene: Keep temporary text files next to the source book; do not delete user data; surface any extraction failures explicitly.
