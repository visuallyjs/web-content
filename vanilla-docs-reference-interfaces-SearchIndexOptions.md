SearchIndexOptions

Options for the search index.

| Name           | Type           | Description                                                                                                                               |
| -------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| caseSensitive? | boolean        | Whether or not the search index should ignore case. By default this is false.                                                             |
| exclusions?    | Array\<string> | Optional list of field names to omit from the documents stored for each node. This means that any field in this list will not be indexed. |
| fields?        | Array\<string> | Optional list of fields to index. By default this is empty, meaning all fields (minus any `exclusions`) will be indexed.                  |
| limit?         | number         | Optional limit for the number of result a search should return. Defaults to 10.                                                           |
