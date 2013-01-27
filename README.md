## Lua PrettyPrint

  Converts a table to a string with human-readable Lua syntax.

### Usage

	PrettyPrint = require 'PrettyPrint'
	prettyOutput = PrettyPrint( someTable )

### Sorting

Entries in a table are sorted before printing. They are first compared by their values' types, then by their keys. Value type precedence is as follows:

	1 boolean
	2 number
	3 string
	4 function
	5 thread
	6 table
	7 userdata
	8 nil

If the keys are numbers, they are compared as numbers. Otherwise, they are compared as strings.

### Sequences

Entries whose keys are sequential do not have their key portion
printed.

	{
		[1] = "a";
		[2] = true;
		[3] = 4;
	}

becomes:

	{
		"a";
		true;
		4;
	}

Entries whose value is an array that contains only primitive values are collapsed onto one line.

	{"a", true, 4};

### Variable Keys

Entries whose keys are strings that can be a variable name are printed as variables.

	["EntryKey"] = "EntryValue";

becomes:

	EntryKey = "EntryValue";

### Limitations

- Values that are not booleans, numbers, strings, or tables are ignored.
- Keys that are not booleans, numbers, or strings are ignored.
- If a looped reference is found, it is ignored, and not printed.
