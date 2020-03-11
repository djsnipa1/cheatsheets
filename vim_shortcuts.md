# Vim Shortcut Keys 

| Shortcut Keys | Function      |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

### Main

|
| Escape key | Gets out of the current mode into the “command mode”. All keys are bound of commands. |
| i | “Insert mode” for inserting text. Keys behave as expected. |
| : | “Last\-line mode” where Vim expects you to enter a command such as to save the document. |

|

### Navigation keys

|
| h | moves the cursor one character to the left. |
| j or Ctrl + J | moves the cursor down one line. |
| k or Ctrl + P | moves the cursor up one line. |
| l | moves the cursor one character to the right. |
| 0 | moves the cursor to the beginning of the line. |
| \$ | moves the cursor to the end of the line. |
| ^ | moves the cursor to the first non\-empty character of the line |
| w | move forward one word (next alphanumeric word) |
| W | move forward one word (delimited by a white space) |
| 5w | move forward five words |
| b | move backward one word (previous alphanumeric word) |
| B | move backward one word (delimited by a white space) |
| 5b | move backward five words |
| G | move to the end of the file |
| gg | move to the beginning of the file. |

|

### Navigate around the document

|
| ( | jumps to the previous sentence |
| ) | jumps to the next sentence |
| { | jumps to the previous paragraph |
| } | jumps to the next paragraph |
| \[\[ | jumps to the previous section |
| \]\] | jumps to the next section |
| \[\] | jump to the end of the previous section |
| \]\[ | jump to the end of the next section |

|

### Insert text

|
| a | Insert text after the cursor |
| A | Insert text at the end of the line |
| i | Insert text before the cursor |
| o | Begin a new line below the cursor |
| O | Begin a new line above the cursor |

|

### Special inserts

|
| :r \[filename\] | Insert the file \[filename\] below the cursor |
| :r !\[command\] | Execute \[command\] and insert its output below the cursor |

|

### Delete text

|
| x | delete character at cursor |
| dw | delete a word. |
| d0 | delete to the beginning of a line. |
| d\$ | delete to the end of a line. |
| d) | delete to the end of sentence. |
| dgg | delete to the beginning of the file. |
| dG | delete to the end of the file. |
| dd | delete line |
| 3dd | delete three lines |

|

### Simple replace text

|
| r{text} | Replace the character under the cursor with {text} |
| R | Replace characters instead of inserting them |

|

### Copy/Paste text

|
| yy | copy current line into storage buffer |
| \["x\]yy | Copy the current lines into register x |
| p | paste storage buffer after current line |
| P | paste storage buffer before current line |
| \["x\]p | paste from register x after current line |
| \["x\]P | paste from register x before current line |

|

### Undo/Redo operation

|
| u | undo the last operation. |
| Ctrl+r | redo the last undo. |

|

### Search and Replace keys

|
| /search_text | search document for search_text going forward |
| ?search_text | search document for search_text going backward |
| n | move to the next instance of the result from the search |
| N | move to the previous instance of the result |
| :%s/original/replacement | Search for the first occurrence of the string “original” and replace it with “replacement” |
| :%s/original/replacement/g | Search and replace all occurrences of the string “original” with “replacement” |
| :%s/original/replacement/gc | Search for all occurrences of the string “original” but ask for confirmation before replacing them with “replacement” |

|

### Bookmarks

|
| m {a\-z A\-Z} | Set bookmark {a\-z A\-Z} at the current cursor position |
| :marks | List all bookmarks |
| \`{a\-z A\-Z} | Jumps to the bookmark {a\-z A\-Z} |

|

### Select text

|
| v | Enter visual mode per character |
| V | Enter visual mode per line |
| Esc | Exit visual mode |

|

### Modify selected text

|
| ~ | Switch case |
| d | delete a word. |
| c | change |
| y | yank |
| \> | shift right |
| < | shift left |
| ! | filter through an external command |

|

### Save and quit

|
| :q | Quits Vim but fails when file has been changed |
| :w | Save the file |
| :w new_name | Save the file with the new_name filename |
| :wq | Save the file and quit Vim. |
| :q! | Quit Vim without saving the changes to the file. |
| ZZ | Write file, if modified, and quit Vim |
| ZQ | Same as :q! Quits Vim without writing changes |
