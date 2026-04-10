# grandma3

A powerful macro and Lua scripting tool for GrandMA3 lighting consoles.

## Description

grandma3 provides enhanced macro functionality and Lua scripting capabilities for GrandMA3 lighting control systems. This tool helps lighting programmers and operators automate tasks, create custom workflows, and extend the functionality of their GrandMA3 consoles.

## Features

- **Macro Management**: Create, edit, and organize macros efficiently
- **Lua Scripting**: Write custom Lua scripts to automate complex tasks
- **Extended Functionality**: Access features beyond the standard console interface
- **Workflow Automation**: Streamline repetitive programming tasks

## Requirements

- GrandMA3 software or hardware console
- Lua 5.x support (built into GrandMA3)

## Installation

1. Clone this repository:
   ```bash
   git clone <repository-url>
   ```

2. Copy the macro and Lua files to your GrandMA3 user data folder

3. Import macros through the GrandMA3 interface

## Usage

### Macros
Load and execute macros directly from the GrandMA3 command line or assign them to executor buttons for quick access.

### Lua Scripts
Access Lua scripting through the GrandMA3 command shell. Example:
```lua
-- Example Lua script
Cmd("Select All")
Cmd("Clear")
```

## Project Structure

```
grandma3/
├── README.md          # Project documentation
├── macros/            # Macro files (to be added)
└── lua/               # Lua scripts (to be added)
```

## Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

## License

This project is provided as-is for the GrandMA3 community.

## Resources

- [GrandMA3 Official Documentation](https://www.malighting.com/)
- [Lua Programming Language](https://www.lua.org/)
- [GrandMA3 Command Reference](https://wiki.malighting.com/)

## Support

For questions and support, please open an issue in this repository or consult the GrandMA3 community forums.
