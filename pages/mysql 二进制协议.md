- #mysql
- ColumnDefinition41
	- ```
	  lenenc_str     catalog
	  lenenc_str     schema
	  lenenc_str     table
	  lenenc_str     org_table
	  lenenc_str     name
	  lenenc_str     org_name
	  lenenc_int     length of fixed-length fields [0c]
	  2              character set
	  4              column length
	  1              type
	  2              flags
	  1              decimals
	  2              filler [00] [00]
	    if command was COM_FIELD_LIST {
	  lenenc_int     length of default-values
	  string[$len]   default values
	    }
	  ```
	- 解释
	  ```
	  catalog (lenenc_str) -- catalog (always "def")
	  schema (lenenc_str) -- schema-name
	  table (lenenc_str) -- virtual table-name
	  org_table (lenenc_str) -- physical table-name
	  name (lenenc_str) -- virtual column name
	  org_name (lenenc_str) -- physical column name
	  next_length (lenenc_int) -- length of the following fields (always 0x0c)
	  character_set (2) -- is the column character set and is defined in Protocol::CharacterSet.
	  column_length (4) -- maximum length of the field
	  column_type (1) -- type of the column as defined in Column Type
	  flags (2) -- flags
	  decimals (1) -- max shown decimal digits
	    0x00 for integers and static strings
	    0x1f for dynamic strings, double, float
	    0x00 to 0x51 for decimals
	  ```