# kv3parser

A Python parser for converting KV3 (KeyValues3) data format to JSON, built for data analysis in the game Deadlock.

## Installation

You can install kv3parser using pip:

```
pip install kv3parser
```

## Overview

This project provides a robust parser that can read KV3 formatted data from .vdata files and convert it to JSON. KV3 is a data format used in some Valve games and tools, including Deadlock. By converting KV3 to JSON, this parser facilitates easier analysis and manipulation of game data using standard JSON tools and libraries.

## Features

- Parses KV3 formatted data from .vdata files and converts it to JSON
- Handles complex KV3 structures including nested objects and arrays
- Supports various data types: strings, numbers, booleans, null values
- Recognizes and preserves KV3-specific flags (resource, resourcename, panorama, soundevent, subclass)
- Provides detailed error messages with line and column information for parsing errors
- Supports multi-line strings
- Handles comments (both single-line and multi-line)
- Allows for flexible syntax, such as omitting commas between key-value pairs

## Usage

```python
import json
from kv3parser import kv3_to_json

# Path to your .vdata file
vdata_file_path = 'path/to/your/file.vdata'

# Read the content of the .vdata file
with open(vdata_file_path, 'r', encoding='utf-8') as file:
    vdata_content = file.read()

try:
    # Parse the KV3 content
    json_output = kv3_to_json(vdata_content)
    
    # Print or save the JSON output
    print(json_output)
    
    # Optionally, save to a file
    with open('output.json', 'w', encoding='utf-8') as json_file:
        json_file.write(json_output)

except Exception as e:
    print(f"Error parsing KV3: {e}")
```

This script does the following:

1. Reads a .vdata file (which uses the KV3 format).
2. Parses the content using `kv3_to_json()`.
3. Saves the resulting JSON to a file.
4. Provides an example of how to load the JSON back into a Python dictionary for further processing.

You can easily modify this script to suit your specific needs, such as processing multiple files, extracting specific data, or integrating it into a larger application.

## Error Handling

The parser provides detailed error messages when it encounters issues in the KV3 content. The `KV3ParseError` class is used to generate these messages, which include:

- The type of error
- The line and column where the error occurred
- A snippet of the content around the error location
- A pointer to the exact position of the error

## Implementation Details

The parser is implemented as a `KV3Parser` class with the following key methods:

- `parse()`: The main parsing method
- `parse_value()`: Parses different types of values (objects, arrays, strings, numbers, keywords)
- `parse_object()`: Handles parsing of KV3 objects
- `parse_array()`: Handles parsing of arrays
- `parse_string()`: Parses both single-line and multi-line strings
- `parse_number()`: Handles integer and float parsing
- `parse_keyword_or_resource()`: Handles keywords (true, false, null) and resource strings

The parser also includes methods for skipping whitespace and comments, and for parsing keys with potential flags.

The `kv3_to_json()` function provides a convenient wrapper around the `KV3Parser` class, making it easy to convert KV3 content to JSON with a single function call.

## Dependencies

This project requires Python 3.6 or later. It uses only built-in Python libraries (`re` and `json`) and has no external dependencies.

## Contributing

Contributions to improve the parser or extend its functionality are welcome. Please feel free to submit issues or pull requests on the GitHub repository.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

This parser was created to facilitate data analysis for the game Deadlock. Special thanks to the Deadlock community for their support and feedback.
