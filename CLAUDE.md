# Claude Code Assistant Guidelines for PyDataVT2025

## Project Overview
This is a public technical demonstration for a conference focused on geospatial Python tools. The goal is to create Jupyter notebook(s) showcasing various Python workflows for geospatial analysis that attendees can reference and learn from.

## Transparency & Attribution
This project is developed **openly and transparently** with AI assistance from Claude Code. We acknowledge this collaboration publicly because:
- It demonstrates modern development workflows
- It shows how AI tools can enhance learning and documentation
- It models transparent attribution practices for the community

## Core Principles

### 1. Educational Focus
- Write clear, well-commented code suitable for learners
- Include explanations of concepts, not just implementation
- Provide context for why certain approaches are chosen
- Use realistic, practical examples that attendees can adapt

### 2. Geospatial Python Ecosystem
Focus on demonstrating tools such as:
- GeoPandas for vector data manipulation
- Rasterio/GDAL for raster data processing
- Shapely for geometric operations
- Folium/Leaflet for interactive visualization
- PyProj for coordinate system transformations
- Contextily for basemap integration
- Other relevant libraries as needed

### 3. Code Quality Standards
- Follow PEP 8 Python style guidelines
- Use type hints where appropriate for clarity
- Include docstrings for functions and classes
- Write modular, reusable code
- Handle errors gracefully with informative messages
- Include data validation checks

### 4. Notebook Structure
- Start with clear learning objectives
- Include installation/setup instructions
- Use markdown cells to explain concepts between code cells
- Show intermediate outputs to aid understanding
- End sections with key takeaways
- Provide exercises or extensions where appropriate

### 5. Data Considerations
- Use publicly available datasets when possible
- Include data sources and licenses in documentation
- Provide scripts or instructions for data acquisition
- Consider file sizes for GitHub storage
- Document data preprocessing steps clearly

### 6. Reproducibility
- Specify all dependencies with versions (requirements.txt or environment.yml)
- Test notebooks run top-to-bottom without errors
- Document system requirements if applicable
- Use relative paths for portability
- Include random seeds where randomness is involved

### 7. Git Workflow
- Write clear, descriptive commit messages
- Keep commits focused and atomic when possible
- Use .gitignore appropriately for data files, cache, etc.
- Document major changes in commit messages
- **Commit after each prompt**: Create a commit after completing work on each user prompt to show progression and allow easy rollback
- Include reference to prompt number in commit messages for traceability

## Claude Code's Role

### When Assisting:
- Prioritize clarity and educational value over brevity
- Explain geospatial concepts when introducing them
- Suggest best practices for the Python geospatial ecosystem
- Point out potential pitfalls or common errors
- Recommend appropriate libraries and approaches
- Help structure content for progressive learning

### When Writing Code:
- Add comments explaining non-obvious operations
- Include error handling and validation
- Use descriptive variable names
- Show outputs that help learners understand results
- Demonstrate visualization best practices
- Keep code cells focused on single concepts

### When Reviewing:
- Check for technical accuracy
- Verify code follows educational best practices
- Ensure notebooks are beginner-friendly
- Test that examples are clear and complete
- Suggest improvements for clarity or efficiency

## Collaboration Notes
- Ask clarifying questions when requirements are ambiguous
- Suggest alternatives when there are multiple valid approaches
- Flag when additional context or data is needed
- Provide rationale for recommendations
- Be explicit about trade-offs in technical decisions

## Prompt History & Documentation

### Maintaining PROMPT_HISTORY.md
After each prompt, Claude will update `PROMPT_HISTORY.md` with:
- **Prompt Number**: Sequential numbering for reference
- **Date/Time**: When the prompt was received
- **User Request**: Verbatim prompt from the user
- **Actions Taken**: Bulleted list of all actions Claude performed
- **Files Modified/Created**: List of files changed
- **Token Usage**: Input and output tokens for the interaction (if available)
- **Estimated Cost**: Calculated cost based on token usage (if available)
- **Commit SHA**: Git commit hash for this prompt's changes

### End-of-Prompt Workflow
After completing work on each prompt, Claude will:
1. **Summarize actions**: Provide a clear summary of what was accomplished
2. **Update PROMPT_HISTORY.md**: Append a new entry with details above
3. **Commit changes**: Create a git commit with message format:
   ```
   Prompt #N: Brief description of changes

   [More detailed description if needed]

   🤖 Generated with Claude Code
   ```
4. **Report token/cost metrics**: Include token usage and estimated cost in the summary (if available)

### Purpose
This documentation serves multiple purposes:
- Creates a transparent development log
- Allows attendees to see the AI-assisted development process
- Enables easy rollback to any previous state
- Demonstrates cost and efficiency of AI-assisted development
- Provides accountability and traceability

## Success Criteria
A successful demo notebook should:
1. Run completely without errors
2. Teach concepts progressively
3. Include visualizations that enhance understanding
4. Be accessible to Python users new to geospatial analysis
5. Demonstrate practical, real-world workflows
6. Inspire attendees to explore further
7. Serve as a reference for future work

## Attribution
This project is developed by Steve with assistance from Claude Code (Anthropic). AI assistance is used for:
- Code generation and debugging
- Documentation and explanations
- Best practice recommendations
- Workflow suggestions

All content is reviewed, tested, and approved by the human maintainer before inclusion in the repository.

---

*Last Updated: 2025-10-17*
