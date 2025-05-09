# ProcessUserDataTable Module

The **ProcessUserDataTable** module displays a highly configurable table of user-related data in the ProcessWire admin interface. It allows admins to define how fields are displayed, apply formatting, and filter or sort user data.

This document provides a detailed guide to configuring and using the module, ensuring you take full advantage of its features.

---

## 📖 Table of Contents

1. [Overview](#-overview)
2. [Installation](#-installation)
3. [Configuration](#-configuration)
	- [Global Settings](#global-settings)
	- [Field Type Parameters](#field-type-parameters)
	- [Virtual Fields](#virtual-fields)
4. [Rendering and Filtering Options](#-rendering-and-filtering-options)
5. [Examples](#-examples)
6. [FAQ](#-faq)

---

## 🧐 Overview

The **ProcessUserDataTable** module gives you the flexibility to:

- Display fields from the **User** template.
- Define custom virtual fields for calculated or aggregate values.
- Filter users by roles or specific field values.
- Sort and paginate user data.
- Apply custom formatting and tooltips to field values.

---

## 🛠️ Installation

1. **Download the Module**:
   - Clone the repository:  
	 ```bash
	 git clone https://github.com/frameless-at/ProcessUserDataTable.git
	 ```
   - Or download the ZIP file and extract it into your `site/modules/` directory.

2. **Install via Admin**:
   - Go to `Modules > Site > Add New`.
   - Click **"Install"** for the ProcessUserDataTable module.

3. **Verify Installation**:
   - Navigate to the module’s settings under `Setup > User Data Table`.

---

## ⚙️ Configuration

### Global Settings

The module provides global configuration options to define default behavior:

| Setting              | Description                                                                 | Example                                |
|----------------------|-----------------------------------------------------------------------------|----------------------------------------|
| `user_fields_select` | Select fields from the User template to display.                           | `email, first_name, last_name`         |
| `extra_fields`       | Define additional virtual fields (comma-separated).                        | `virtual__sum, virtual__avgScore`      |
| `user_roles`         | Filter users by specific roles.                                            | `editor, admin`                        |
| `roles_mode`         | Define role condition: `or` (at least one) or `and` (all exactly).         | `or`                                   |
| `sort_field`         | Default column to sort by.                                                 | `email` or `virtual__sum`              |
| `sort_dir`           | Default sorting direction (`asc` or `desc`).                               | `asc`                                  |
| `entries_per_page`   | Number of rows per page.                                                   | `25`                                   |

These options are configurable in the module settings under `Setup > User Data Table`.

---

### Field Type Parameters

Each field displayed in the table can be customized using parameters in a key-value format. These parameters can be configured in the **Parameters** textarea for each field.

#### **Primitive Fields** (Text, Integer, DateTime, Checkbox, etc.)

| Parameter         | Required | Description                                                                 | Example                        |
|-------------------|:--------:|-----------------------------------------------------------------------------|--------------------------------|
| `label`           |    No    | Override the column header.                                                 | `label=Full Name`              |
| `edit_link`       |    No    | Make the value a link to the user edit page.                                | `edit_link=1`                  |
| `tooltip_field`   |    No    | Field name for tooltip content.                                             | `tooltip_field=created`        |
| `tooltip_prefix`  |    No    | Text displayed before the tooltip value.                                    | `tooltip_prefix=Joined:`       |
| `tooltip_format`  |    No    | Apply formatting, e.g., `date(d.m.Y)`.                                      | `tooltip_format=date(Y)`       |
| `separator`       |    No    | Separator for multiple values (if the field is an array).                   | `separator=, `                 |
| `format_raw`      |    No    | Custom labels for Checkbox values (`no|yes`).                               | `format_raw=Disabled|Enabled`  |

#### **FieldtypePage**

| Parameter         | Required | Description                                                                 | Example                        |
|-------------------|:--------:|-----------------------------------------------------------------------------|--------------------------------|
| `resolve_page`    |   Yes    | Specify which field of the referenced Page to display.                      | `resolve_page=title`           |
| `as_link`         |    No    | Display the value as a link to the referenced Page.                         | `as_link=1`                    |
| `tooltip_field`   |    No    | Field on the Page to show in a hover tooltip.                               | `tooltip_field=dateEvent`      |
| `tooltip_prefix`  |    No    | Prefix text for the tooltip.                                                | `tooltip_prefix=Date:`         |
| `tooltip_format`  |    No    | Format helper for tooltip content.                                          | `tooltip_format=date(d.m.Y)`   |
| `separator`       |    No    | Separator between multiple pages.                                           | `separator=, `                 |

#### **FieldtypeTable**

| Parameter         | Required | Description                                                                 | Example                        |
|-------------------|:--------:|-----------------------------------------------------------------------------|--------------------------------|
| `table_column`    |   Yes    | Name of the column in the TableField.                                       | `table_column=product_id`      |
| `resolve_page`    |    No    | If the column holds Page IDs, specify which Page field to display.          | `resolve_page=title`           |
| `as_link`         |    No    | Make the resolved Page value a link.                                       | `as_link=1`                    |
| `separator`       |    No    | Separator for multiple resolved values.                                    | `separator= | `                |
| `tooltip_field`   |    No    | Column for tooltip content.                                                | `tooltip_field=product_date`   |
| `tooltip_prefix`  |    No    | Prefix text for the tooltip.                                                | `tooltip_prefix=Purchased:`    |
| `tooltip_format`  |    No    | Format helper for the tooltip value.                                        | `tooltip_format=date(d.m.Y)`   |
| `format_raw`      |    No    | Re-format the raw value (e.g., `d.m.Y`).                                    | `format_raw=d.m.Y`             |

---

### Virtual Fields

Virtual fields are custom columns that display derived or aggregate values. Use the prefix `virtual__` to define these fields.

| Parameter         | Required | Description                                                                 | Example                        |
|-------------------|:--------:|-----------------------------------------------------------------------------|--------------------------------|
| `selector`        |   Yes    | Expression for the virtual field (`sum()`, `avg()`, `min()`, `count()`).    | `selector=sum(products.price)` |
| `label`           |    No    | Override the column header.                                                 | `label=Total Revenue`          |
| `format`          |    No    | Apply formatting (`int`, `number`, `currency`, `percent`, `custom=...`).    | `format=currency`              |
| `tooltip_field`   |    No    | Use another field or expression as a tooltip.                               | `tooltip_field=count(products)`|
| `tooltip_prefix`  |    No    | Prefix text for a tooltip.                                                  | `tooltip_prefix=Count:`        |
| `tooltip_format`  |    No    | Format helper for tooltip value.                                            | `tooltip_format=custom=%d`     |

---

## 🎨 Rendering and Filtering Options

The module supports advanced rendering and filtering features:

1. **Role Filtering**: Show only users with specific roles (`user_roles`).
2. **Sorting**: Sort by any configured field, including virtual fields.
3. **Pagination**: Display a configurable number of rows per page (`entries_per_page`).
4. **Custom Cell Rendering**: Render fields as links, tooltips, or formatted text.

---

## 📝 Examples

## Example 1: Displaying a TableField with Tooltips

This configuration defines a column that displays purchased products with a tooltip showing the purchase date.

```
label=Products Bought 
table_column=product_id 
resolve_page=title 
as_link=1 
tooltip_field=product_date 
tooltip_prefix=Purchased: 
tooltip_format=date(d.m.Y H:i)
```


### Explanation of Parameters

| Parameter        | Description                                                                      | Example                  |
|------------------|----------------------------------------------------------------------------------|--------------------------|
| `label`          | The column header label.                                                        | `Products Bought`        |
| `table_column`   | The name of the column in the **FieldtypeTable** field.                         | `product_id`             |
| `resolve_page`   | Specifies which field from the referenced Page to display.                     | `title`                  |
| `as_link`        | Renders the value as a clickable link to the referenced Page.                  | `1` (enabled)            |
| `tooltip_field`  | Specifies the column to use for the tooltip content.                           | `product_date`           |
| `tooltip_prefix` | Adds a prefix to the tooltip text.                                              | `Purchased:`             |
| `tooltip_format` | Formats the tooltip content using a date helper function.                      | `date(d.m.Y H:i)`        |

### Result in the Admin Interface

When applied, this configuration will:

1. Display a column labeled **"Products Bought"**.
2. Show the product titles (resolved from the Page field `title`).
3. Render the product titles as clickable links leading to the detailed Page.
4. Add a tooltip to each entry that displays the purchase date in the format `day.month.year hour:minute`, prefixed with the text **"Purchased:"**.

### Example Table Output

| Products Bought       |
|------------------------|
| [Product A](#productA) |
| [Product B](#productB) |

Hovering over the entries will display tooltips such as:

- **Purchased: 25.12.2024 14:30**
- **Purchased: 01.01.2025 10:15**


This example demonstrates how to leverage the **ProcessUserDataTable** module to create an intuitive and informative table column in the ProcessWire backend.

---

## Example 2: Virtual Field for Aggregate Value

The **ProcessUserDataTable** module allows you to define virtual fields for calculated or aggregate values using the `virtual__` prefix. This example demonstrates how to configure a virtual field to display the total revenue from products using the `sum()` function.

### Configuration

Add the following configuration in the **Parameters** textarea for the virtual field:
```
selector=sum(products.price) 
label=Total Revenue 
format=currency
```

### Explanation of Parameters

| Parameter   | Required | Description                                                                 | Example                        |
|-------------|:--------:|-----------------------------------------------------------------------------|--------------------------------|
| `selector`  |   Yes    | The expression to calculate the aggregate value. In this case, `sum()` is used to calculate the total of the `products.price` field. | `sum(products.price)`          |
| `label`     |    No    | The column header label to display in the table.                            | `Total Revenue`                |
| `format`    |    No    | Defines how the value is formatted. Supports `int`, `number`, `currency`, `percent`, or a custom format. | `currency`                     |

### Supported `selector` Functions
- **`sum()`**: Calculates the total sum of the specified field.
- **`avg()`**: Calculates the average value of the specified field.
- **`min()`**: Finds the minimum value in the field.
- **`max()`**: Finds the maximum value in the field.
- **`count()`**: Counts the number of entries in the field.
- **`join(..., ', ')`**: Joins multiple values together with a specified separator.

### Supported `format` Options
- **`int`**: Rounds the value to the nearest integer.
- **`number`**: Formats the value as a number with two decimal places.
- **`currency`**: Formats the value as a currency (e.g., `€ 1,234.56`).
- **`percent`**: Formats the value as a percentage.
- **`custom=...`**: Apply a custom format string using `sprintf()` syntax.

### Result in the Admin Interface

When applied, this configuration will:

1. Add a column labeled **"Total Revenue"** to the table.
2. Calculate the total sum of all `price` values in the `products` field.
3. Format the value as currency (e.g., `€ 1,234.56`).

### Example Table Output

| User          | Total Revenue |
|---------------|---------------|
| John Doe      | € 1,234.56    |
| Jane Smith    | € 2,345.67    |

This configuration allows you to create insightful aggregate columns in your table, enhancing the usefulness of the **ProcessUserDataTable** module.

---

## Example 3: Checkbox with Custom Labels

The **ProcessUserDataTable** module allows you to customize how checkbox fields are displayed in the table. You can define specific labels for the `true` (checked) and `false` (unchecked) states using the `format_raw` parameter.

### Configuration

To customize the labels for a checkbox field, use the following configuration in the **Parameters** textarea:
```
label=Status 
format_raw=Inactive|Active
```

### Explanation of Parameters

| Parameter   | Required | Description                                                                 | Example                  |
|-------------|:--------:|-----------------------------------------------------------------------------|--------------------------|
| `label`     |    No    | The column header label to display in the table.                            | `Status`                |
| `format_raw`|    No    | Defines custom labels for the unchecked (`false`) and checked (`true`) states. Use a pipe (`|`) to separate the two labels. | `Inactive|Active`        |

### How `format_raw` Works
- The first value (before the pipe `|`) is displayed when the checkbox is **unchecked** (`false`).
- The second value (after the pipe `|`) is displayed when the checkbox is **checked** (`true`).

If `format_raw` is not specified, the module will use default labels:
- **Unchecked**: Displays as `Disabled`.
- **Checked**: Displays as `Enabled`.

### Result in the Admin Interface

When applied, this configuration will:

1. Add a column labeled **"Status"** to the table.
2. Display the label **"Inactive"** for unchecked checkboxes.
3. Display the label **"Active"** for checked checkboxes.

### Example Table Output

| User          | Status       |
|---------------|--------------|
| John Doe      | Active       |
| Jane Smith    | Inactive     |

This configuration allows you to provide user-friendly, meaningful labels for checkbox fields in your table, enhancing clarity and usability.


---

## ❓ FAQ

### Q: Can I display fields from other templates?
A: The module currently supports only fields directly defined in the **User template**.

### Q: How do I add a virtual field?
A: Add the field name with the prefix `virtual__` (e.g., `virtual__sum`) in the **Additional fields** setting.

### Q: Can I sort by virtual fields?
A: Yes, sorting by virtual fields is supported using the `selector` parameter.

### Q: Can I use fields from related templates (e.g., Pages referenced in a User field)?
**A:** Yes, you can use `resolve_page` to display fields from related Pages (e.g., `resolve_page=title` for a Page reference in a user field). For nested structures, you can also use virtual fields and selector expressions.

### Q: What happens if I configure a field that doesn't exist in the User template?
**A:** The module will skip over fields that do not exist in the User template or are incorrectly configured. No errors will be displayed, but the column will be empty in the output.

### Q: How can I customize the tooltip text for a field?
**A:** You can specify a `tooltip_field` (the field to use for tooltip content) and optionally add `tooltip_prefix` or format it using `tooltip_format`. For example: 
```
tooltip_field=created 
tooltip_prefix=Joined: 
tooltip_format=date(d.m.Y)
```

### Q: Can I configure multiple roles for filtering?
**A:** Yes, you can specify multiple roles using `user_roles` and define whether users need **at least one role** (`or`) or **all roles exactly** (`and`) using `roles_mode`.

### Q: Can I display fields that reference multiple Pages (PageArrays)?
**A:** Yes, the module supports PageArray fields. You can use `resolve_page` to display a specific subfield (e.g., `title`) and separate multiple values using `separator`.

### Q: How do I create a calculated field using multiple fields?
**A:** Use the virtual field feature with a `selector` expression. For example, to calculate the total price of products:
```
selector=sum(products.price)
```
### Q: What happens if I try to sort by a virtual field?
**A:** Sorting by virtual fields is supported. Ensure you configure the virtual field with a valid `selector` and specify it in the `sort_field` setting.

### Q: Can I display a checkbox field as custom labels like "Active" or "Inactive"?
**A:** Yes, by using `format_raw`. For example:
```
format_raw=Pending|Cleared
```

### Q: Is it possible to export the table data?
**A:** The module does not natively support exporting data. However, you can use ProcessWire's API or other tools to generate CSV or JSON exports.

### Q: How do I handle fields with large amounts of text (e.g., multi-line text fields)?
**A:** For large text fields, you can truncate the content using custom formatting or use tooltips to display the full content on hover.

### Q: Can I hide the table for specific user roles?
**A:** Yes, you can control access to the module via ProcessWire's permissions system. Ensure the appropriate roles have or lack the `user-admin` permission.

### Q: What should I do if I encounter performance issues with large datasets?
**A:** Reduce the number of rows displayed per page (`entries_per_page`) and optimize the fields being queried (e.g., avoid complex calculations in virtual fields).

---

This README provides a comprehensive guide to configuring and using the **ProcessUserDataTable** module. If you have further questions or need assistance, feel free to contact the author or check the [repository documentation](https://github.com/frameless-at/ProcessUserDataTable).