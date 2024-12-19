# update Notion database

To use it:

Set up the secrets in your GitHub repository:

* NOTION_TOKEN
* NOTION_DATABASE_ID


Trigger the workflow manually and provide the fields as a JSON string. Examples:

``` json
// Example 1 - Version update
{
  "Date": "today",
  "Component": "MyApp",
  "Old Version": "1.0.0",
  "New Version": "1.1.0"
}

// Example 2 - Task tracking
{
  "Title": "New Feature",
  "Status": "In Progress",
  "Priority": "High",
  "Due Date": "2024-12-31"
}
```

The script will:

Parse the JSON input
Convert values to appropriate types
Add a new row to your Notion database, if row with the same values already exists, it will not be added - the check is based on the unique_fields comma seprated list

# Example workflow using the composite action
```yaml
name: Update Notion
on:
  workflow_dispatch:
    inputs:
      fields_json:
        description: 'Fields to update'
        required: true
        type: string
      unique_fields:
        description: 'Unique fields to cjeck for duplicates'
        required: true
        type: string

jobs:
  update-notion:
    runs-on: ubuntu-latest
    steps:
      - uses: comet-ml/gha-tools/notion-update@main  # If publishing as a separate repo
        with:
          notion_token: ${{ secrets.NOTION_TOKEN }}
          database_id: ${{ secrets.NOTION_DATABASE_ID }}
          fields_json: ${{ inputs.unique_fields }}

```

For your Notion page you want to update - https://developers.notion.com/docs/create-a-notion-integration#give-your-integration-page-permissions

