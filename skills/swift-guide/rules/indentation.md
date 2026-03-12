# Indentation

Although the Swift Style Guide does not have a single "Indentation" section, the following rules govern how code is indented:

*   **No Tabs:** Tab characters are not used for indentation. (See [Source File Basics](source-file-basics.md))
*   **Space Character:** The Unicode horizontal space character (`U+0020`) is used for indentation.
*   **Line-Wrapping Indentation:** A continuation line that is part of a vertically-oriented comma-delimited list is indented exactly +2 from the original line. (See [Line-Wrapping](line-wrapping.md))
*   **Brace Style:** In general, braces follow Kernighan and Ritchie (K&R) style for non-empty blocks. (See [Braces](braces.md))
*   **Switch Statements:** Case statements are indented at the *same* level as the switch statement to which they belong; the statements inside the case blocks are then indented +2 spaces from that level. (See [Switch Statements](switch-statements.md))
*   **Control Flow Wrapping:** When a control flow statement (such as `if`, `guard`, `while`, or `for`) is wrapped, the first continuation line is indented to the same position as the token following the control flow keyword. Additional continuation lines are indented at that same position if they are syntactically parallel elements, or in +2 increments from that position if they are syntactically nested. (See [Line-Wrapping](line-wrapping.md))
