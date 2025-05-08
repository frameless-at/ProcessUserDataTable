# User Data Table Module

Displays a configurable table of User template fields in the ProcessWire admin.

Licensed under GNU/GPL v2, see LICENSE.TXT  
Author: frameless Media · https://frameless.at  

---

## 📊 Configuration Parameters

Specify one `key=value` pair per line in each column’s **Parameter** textarea.

### 🔤 General (all field types)

| Parameter          | Required | Description                                | Example           |
|--------------------|:--------:|--------------------------------------------|-------------------|
| `label`            |    No    | Override the column header                 | `label=Full Name` |

---

### 👤 Primitive Fields (Text, Integer, DateTime on User)

| Parameter          | Required | Description                                          | Values                      |
|--------------------|:--------:|------------------------------------------------------|-----------------------------|
| `edit_link`        |    No    | Link value to user edit page                         | `edit_link=1`               |
| `tooltip_field`    |    No    | Field name for tooltip content                       | `tooltip_field=created`     |
| `tooltip_prefix`   |    No    | Text displayed before tooltip value                  | `tooltip_prefix=Joined:`    |
| `tooltip_format`   |    No    | Format helper, e.g. `date(d.m.Y)`                    | `tooltip_format=date(Y)`    |
| `separator`        |    No    | Separator for multiple values (if field is array)    | `separator= — `             |

---

### 🔗 FieldtypePage

| Parameter          | Required | Description                                          | Values                      |
|--------------------|:--------:|------------------------------------------------------|-----------------------------|
| `resolve_page`     |   Yes    | Which field of the referenced Page to display        | `resolve_page=title`        |
| `as_link`          |    No    | Render value as link to that Page                    | `as_link=1`                 |
| `tooltip_field`    |    No    | Field on the Page to show in a hover tooltip         | `tooltip_field=dateEvent`   |
| `tooltip_prefix`   |    No    | Prefix text for the tooltip                          | `tooltip_prefix=Date:`      |
| `tooltip_format`   |    No    | Format helper for tooltip value                      | `tooltip_format=date(d.m.Y)`|
| `separator`        |    No    | For PageArray, separator between multiple pages       | `separator=, `              |

---

### 🧮 FieldtypeTable

| Parameter          | Required | Description                                                             | Example                          |
|--------------------|:--------:|-------------------------------------------------------------------------|----------------------------------|
| `table_column`     |   Yes    | Name of the column in the TableField                                    | `table_column=product_id`        |
| `resolve_page`     |    No    | If that column holds Page IDs, which Page field to display              | `resolve_page=title`             |
| `as_link`          |    No    | Make resolved Page value a link                                         | `as_link=1`                      |
| `separator`        |    No    | Separator for multiple resolved values                                  | `separator= | `                  |
| `tooltip_field`    |    No    | Name of another Table column to use as tooltip                           | `tooltip_field=product_date`     |
| `tooltip_prefix`   |    No    | Prefix text for the tooltip                                              | `tooltip_prefix=Purchased:`      |
| `tooltip_format`   |    No    | Format helper for the tooltip value                                       | `tooltip_format=date(d.m.Y H:i)` |
| `format_raw`       |    No    | If you want to re-format the “raw” (unformatted) Page field value         | `format_raw=Y-m-d`               |

---

### 🧠 Virtual Fields (`virtual__...`)

Define one or more in **Additional fields** (comma-separated).

| Parameter          | Required | Description                                                      | Example                                    |
|--------------------|:--------:|------------------------------------------------------------------|--------------------------------------------|
| `selector`         |   Yes    | Expression: `sum(...)`, `avg(...)`, `min(...)`, `max(...)`, `count(...)`, `join(..., ', ')` | `selector=sum(products.product_id.price)` |
| `label`            |    No    | Override column header                                           | `label=Total Revenue`                     |
| `format`           |    No    | Quick numeric formats: `int`, `number`, `currency`, `percent`, `custom=…` | `format=currency`                        |
| `separator`        |    No    | For `join()`, specify the separator                              | `separator=; `                            |
| `tooltip_field`    |    No    | Use another field or expression as tooltip                       | `tooltip_field=count(products)`           |
| `tooltip_prefix`   |    No    | Prefix text for tooltip                                          | `tooltip_prefix=Count:`                   |
| `tooltip_format`   |    No    | Format helper for tooltip value                                  | `tooltip_format=custom=%d items`          |

---

### 🧭 Module-wide Options

| Field                  | Required | Description                                                    | Values                     |
|------------------------|:--------:|----------------------------------------------------------------|----------------------------|
| `user_roles`           |    No    | Show only users with these roles                               | Array of role names        |
| `roles_mode`           |    No    | `or` = any role, `and` = exactly all selected                  | `or`, `and`                |
| `sort_field`           |    No    | Default sort column                                            | Field name                 |
| `sort_dir`             |    No    | Default sort direction                                         | `asc`, `desc`              |
| `entries_per_page`     |    No    | Number of rows per page                                        | Integer (default `25`)     |

---

## 📝 Examples

#### TableField with Page lookup and tooltip
```
label=Products Bought
table_column=product_id
resolve_page=title
as_link=1
tooltip_field=product_date
tooltip_prefix=Purchased:
tooltip_format=date(d.m.Y H:i)
```
#### Param for `virtual__countItems`:
```
selector=count(products.product_id)
label=Item Count
```

---
