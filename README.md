# AssetDB

AssetDB is a Splunk application that allows merging distinct data sources into an asset data base, without the need for Splunk Enterprise Security. The app is currently in development, and its README will be updated once it is stable with base functionality.

## Usage

Navigate to the "Configure" tab to configure AssetDB

### Lookups

Create lookup files and corresponding lookup generation searches for each unqiue data source that provides asset information. 

 - **Add lookup file**: Click the *Add Lookup* button to add a lookup file to be used to populate the merged *Asset Database*. A demo lookup file, *assetdb_demo_assets.csv* is provided by default. 

 - **Delete lookup file**: Click the *Delete* link next to an existing lookup file in the *Lookups Table* to remove the lookup and prevent its contents from being merged into the *Asset Database*.

### Fields

Create fields to be stored within the *Asset Database* and merged between all input lookup files. 

- **Add field**: Click the *Add Field* button to add a new field into the *Asset Database*. See the **Field Properties** section below for more information on field properties. 

- **Edit field**: Click the *Edit Field* button to edit an existing field into the *Asset Database*. See the **Field Properties** section below for more information on field properties. 

- **Delete field**: Click the *Delete Field* button to delete an existing field from the *Asset Database*. Deleting a field, does not remove that field from any underlying lookup files. 

### Field Properties

The following field properties can be set when adding a new field or editing an existing field. 

| Property | Type | Description |
| ----------- | ----------- | ----------- |
| Field Name | String | The name of the field. Must consist of alphanumeric characters or underscores. Field names *_key* and *asset* are automatically created during the asset merge process and cannot be overwritten. |
| Key Field | Boolean | Whether the field is a key field or not. Key fields are fields that define a unqiue asset and are used during the asset merge process. See **How AssetDB Merges Assets** for more information on.
| Case Sensitive | Boolean | Wether the field is case sensitive or not. A value of *No* will set all field values to lower case. 
| Ignore Values | String | (Optional) A comma seperated list of field values to ignore (e.g. null,none,unknown). 
| Fill Null | String | (Optional) A static value to fill null entries of a field with (e.g. a default asset priority). 
| Field Type | Single|Multivalue|Eval | Defines the type of field. Use a single value, keep all unique entries as a multivalue, or use an eval expression to define this field.

#### Field Type Specific Options

**Single**
| Property | Type | Description |
| ----------- | ----------- | ----------- |
| Merge Method | Latest|Min|Max|Avg|Coalesce | Defines how a single value is derived across the input lookup table files.
- **Latest**: the most recent value
- **Min**: minimum value, only applicable to numeric field values
- **Max**: maximum value, 
- **Avg**: average value
- **Coalesce**: define a precedence by ranking the source data with the *Coalesce* property |

| Property | Type | Description |
| ----------- | ----------- | ----------- |
| Coalesce | Multiselect | Defines the precedence of source data to be used for this field. |

### How AssetDB Merges Assets