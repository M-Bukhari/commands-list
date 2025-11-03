# Claude Tips and Tricks

## Command list

{:: VIP How to use Claude ::}

<!-- Claude Prompt Examples -->

Tip: Use /agents to create context-efficient experts for specific tasks. Eg. Code Reviewer, Software Architect, Data Scientist

Tip: Want Claude to remember something? Hit # to add preferences, tools, and instructions to Claude's memory

Tip: Did you know you can drag and drop image files into your terminal?

Tip: Press Esc twice to rewind the conversation to a previous point in time

Tip: Run claude --continue or claude --resume to resume a conversation

Tip: Use /agents to create context-efficient experts for specific tasks. Eg. Code Reviewer, Software Architect, Data Scientist

Tip: Press Shift+Enter to send a multi-line message

Tip: Use /permissions to pre-approve and pre-deny bash, edit, and MCP tools

Tip: Want Claude to remember something? Hit # to add preferences, tools, and instructions to Claude's memory

Tip: Ctrl+Escape to launch Claude in your IDE

Tip: Use Plan Mode to prepare for a complex request before making changes. Press shift+tab twice to enable.

```bash
  ! for bash mode       double tap esc to clear input
  / for commands        alt + m to auto-accept edits
  @ for file paths      ctrl + r for verbose output
  # to memorize         shift + ⏎ for newline
  ctrl + _ to undo           alt + v to paste images
```

TIP:
● Hello! I'm ready to continue working on the ABAM Investment Hub project.

Based on our previous work, we successfully:

-   Fixed investor qualification form redirection and alert positioning issues
-   Removed all SCSS helper links from 13 files across the project
-   Catalogued all custom CSS files and external dependencies

What would you like to work on next? I can help with:

-   Bug fixes and troubleshooting
-   Feature development
-   Code optimization
-   Database management
-   UI/UX improvements
-   Documentation updates

What task should we tackle?

What's new:
• Enable /context command for Bedrock and Vertex
• Add mTLS support for HTTP-based OpenTelemetry exporters

```bash

    #  To get current time
    Tip: Use /agents to create context-efficient experts for specific tasks. Eg. Code Reviewer, Software Architect, Data Scientist

```

## General Best Practices

1. **Be Specific** - Instead of "fix the bug", provide detailed context and reproducible error messages

2. **Break Down Large Tasks** - Split complex work into smaller, manageable steps

3. **Let Claude Explore First** - Before making changes, allow Claude to understand your codebase

## Workflow Tips

4. **Start Broad, Then Narrow** - Ask general questions about the codebase first, then get specific

5. **Use Domain-Specific Language** - Reference actual class names, function names, and patterns

6. **Request Multiple Approaches** - Ask for different solution options when debugging

## Efficiency Tips

7. **Use Plan Mode** - For safe, read-only code exploration before making changes

8. **Leverage Specialized Subagents** - Use task-specific agents for targeted work

9. **Run Tests After Changes** - Always validate modifications

10. **Maintain Backward Compatibility** - Especially important during refactoring

## Prompt Engineering

11. **Use "Think Hard" Phrases** - Trigger deeper reasoning for complex problems

12. **Use `@` References** - Quickly reference files and directories

13. **Create Custom Slash Commands** - For repetitive project-specific tasks

## Essential Shortcuts

- **Tab**: Command completion
- **↑**: Command history
- **/**: Show all slash commands
- **/help**: Get help anytime
- **/clear**: Clear conversation history
