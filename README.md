# Claude File Organizer

A Python utility for copying relevant project files to a directory to be easily uploaded to Claude, Anthropic's AI assistant. It selectively copies files based on extensions and .gitignore rules, organizing them into a target folder for easy uploading.  It commits all the files in that folder to a git repository so they're not lost, deletes them, and then copies the updated files to that folder.  This allows you to upload your latest file states to a Claude project without having to manually click through all your folders to select and upload specific files.

This tool is particularly useful when you need to share specific files/file types in your project with claude without wanting to iterate through each subdirectory each time.

## Prerequisites

- Python 3.6 or higher
- Git installed and accessible from command line
- Write permissions for target directory

## How it works

Edit the script copy_files.py to specify:
1. The directory you are copying files from
2. The directory you are copying files to
3. (Optional) File types to include
4. (Optional) .gitignore file to determine which files to exclude

Example configuration:
```python
# CONFIGURATION
SOURCE_DIRECTORY = Path('/Users/username/projects/myproject')  
TARGET_DIRECTORY = Path('/Users/username/claude-files')  
GITIGNORE_FILE = Path('/Users/username/projects/myproject/.gitignore')  

# File extensions to copy (optional)
EXTENSIONS = {'.py', '.yaml', '.toml', '.txt', '.md', '.gitignore', '.gitattributes'}
```

When you run ```python3 copy_files.py``` the following occurs:

1. It initializes a git repository in the target folder if not already initialized. Note that the folder must not be part of an existing repository.
2. It adds and commits the existing files in that folder to that repository.
3. It deletes those existing files.
4. It copies the files from the source directory into that target directory as specified in the optional gitignore file and optional provided extensions. It also includes a file_map.txt file so you (and Claude) can tell where the files came from.

Once this is done you can go into claude project, delete your existing files, go to the target folder you specified, and upload all files there.

## Security Features

The script includes several safety measures:
- Protection against accessing system directories on Windows, Mac, Linux, and Unix
- Permission checks for target directories
- Root directory protection
- System user/ownership checks on Unix systems
- Comprehensive error handling for permission and access issues

## Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/claude-file-copier.git
cd claude-file-copier
```

2. No additional dependencies required - uses Python standard library only.

[Rest of the README remains the same...]

## Limitations

- The target folder must not be within an existing git repository
- The script includes protection against accessing system directories (e.g., /bin, /etc, C:\Windows, etc.)
- Write permissions are required for both source and target directories
- Target directory cannot be owned by root/system user

[Rest of the README remains the same...]

## Contributing

Contributions welcome! Please feel free to submit pull requests.

## License

MIT License - See LICENSE file for details.

## Note

This tool was created specifically for preparing files to share with Claude. It's being shared on GitHub and Hacker News to help others who frequently interact with Claude and need to organize their file sharing.