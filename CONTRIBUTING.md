# Contributing to README Roast

Thanks for your interest in contributing. Here's how to help.

## Ways to Contribute

### Add repos to benchmark categories
The benchmark data in `benchmarks/*.json` is the core differentiator. Adding more repos or refining scores makes the tool better for everyone.

1. Pick a category (`cli-tools`, `ai-ml`, `web-frameworks`, `testing`, `devops`, `library`)
2. Find a top-starred repo that's missing
3. Analyze its README against the scoring rubric in `.claude/skills/readme-hero/SKILL.md` and siblings
4. Add it to the appropriate JSON file with scores and patterns
5. Update `repos_analyzed` count and recalculate `category_averages` and `patterns_summary`

### Add a new benchmark category
If you work in a domain not covered (mobile, gamedev, data engineering, etc.):

1. Create `benchmarks/{category}.json` following the existing schema
2. Analyze 15 top-starred repos in that category
3. Update the master skill in `.claude/skills/readme-roast/SKILL.md` to list the new category
4. Add detection signals to `.claude/skills/readme-audit/SKILL.md`

### Refine scoring rubrics
The scoring rubrics in each skill file are opinionated. If you have data or experience that suggests a different weighting or criteria, open an issue first to discuss.

### Improve PDF reports
The PDF generator at `scripts/generate_pdf_report.py` uses ReportLab. PRs for better charts, layout, or new sections are welcome.

## Development Setup

```bash
git clone https://github.com/hidai25/readme-roast
cd readme-roast

# Optional: install PDF dependencies
pip install reportlab
```

The tool runs as Claude Code skills. To test:
```bash
cd readme-roast
claude
# Then: /readme-audit https://github.com/some/repo
```

## Pull Request Process

1. Fork the repo and create a branch from `main`
2. Make your changes
3. Test by running an audit on at least one repo
4. Ensure benchmark JSON files are valid: `python3 -c "import json; [json.load(open(f'benchmarks/{f}')) for f in ['cli-tools.json','ai-ml.json','testing.json','web-frameworks.json','devops.json','library.json']]"`
5. Open a PR with a clear description of what changed and why

## Code Style

- Skill files (`.md`): Follow the existing structure — frontmatter, purpose, rubric, procedure, output format
- Python: Standard Python style, no external linters required
- JSON: 2-space indent, consistent field ordering

## Issues

- **Bug reports**: Include the command you ran, the repo you audited, and what went wrong
- **Feature requests**: Describe the use case, not just the feature
- **Benchmark corrections**: If a repo's score seems off, explain your reasoning

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
