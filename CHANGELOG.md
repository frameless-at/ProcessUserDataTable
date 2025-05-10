# Changelog

All changes follow [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

---

## [2.3.3] – 2025-05-10

### Changed
- Removed the obsolete `format_raw` parameter from both field configuration and documentation.
- Updated notes for **Primitive Fields** and **Virtual Fields**:
  - Added support for the `format` parameter, allowing formatting options such as `int`, `number`, `currency`, `percent`, and custom patterns.
  - Documented the new `locale` parameter for currency formatting, enabling localized output (e.g., `locale=en_US`).
- Updated notes for **TableField**:
  - Confirmed that the `format` parameter is not supported for TableFields and adjusted the field notes accordingly.
- Ensured field documentation aligns with the current functionality for all field types.

### Links
- [Commit dcaade87a05814f5ec305c243803094bcedd9c15](https://github.com/frameless-at/ProcessUserDataTable/commit/dcaade87a05814f5ec305c243803094bcedd9c15)

---

## [2.3.2] – 2025-05-10

### Added
- Introduced a centralized `formatValue()` method for standardized value formatting:
  - Supports formats such as `int`, `number`, `currency`, `percent`, and custom patterns.
  - Added localization support for currency formatting using `NumberFormatter`.
  - Introduced a new CONFIG parameter `locale` to specify localization options for currency.
  - Handles custom mappings like `format=0:No,1:Yes`.
  - Improved handling of null or empty values with placeholders (`–`).
- Improved support for rendering table columns with dynamic content in both headers and data cells.
  - Added `textAlign` parameter to control text alignment (`left`, `center`, `right`).

### Changed
- Refactored column formatting logic in the `renderColumn()` method for consistency and flexibility.
- Enhanced tooltip generation with support for `tooltip_field`, `tooltip_prefix`, and `tooltip_format` parameters.
- Improved handling of `FieldtypeCheckbox` and `FieldtypeToggle` fields to normalize values and apply dynamic labels.
- Updated the `renderSelectorExpression()` method to handle aggregate functions (`sum`, `avg`, etc.) and nested field paths (e.g., `products.price`) with better error handling.

### Fixed
- Addressed minor bugs and inconsistencies in table column rendering.
- Resolved edge cases in sorting and pagination logic for user data tables.

### Links
- [Commit fcb63f2](https://github.com/frameless-at/ProcessUserDataTable/commit/fcb63f2d7036bdb7b0d0f08b71916b84b14436a3)

---

## [2.3.1] – 2025-05-08
### Added
- Support for `FieldtypeCheckbox` and `FieldtypeToggle` fields in the `renderPrimitiveField` method.
- Custom formatting for checkbox and toggle fields through the `format_raw` configuration option, enabling dynamic labels for `0` and `1` values.

### Improved
- Enhanced rendering logic for boolean fields with fallback to default labels ("Enabled"/"Disabled") if no custom format is defined.
- Compatibility with existing tooltip and edit-link configurations for boolean fields.

### Links
- [Commit 1f524872024624efb696059bacc35e98b66e8f8e](https://github.com/frameless-at/ProcessUserDataTable/commit/1f524872024624efb696059bacc35e98b66e8f8e)

---

## [2.3.0] – 2025-05-08
### Changed
- Revised the renderCell() method to improve the detection of Page and PageArray fields.

---

## [2.2.2] – 2025-05-08
### Changed
- **`renderResolvedPageColumn()`** now recognizes and handles `PageArray` values (e.g. the built-in `roles` field) by using:
  - `$value->each('<a href="{url}">{title}</a>')` for linked output, or
  - `$value->implode('title', ', ')` for plain text
- Introduced a **fallback** for `resolve_page`, accepting `"title|name"` so the first available of those fields is used
- Removed strict `hasField()` gating — all configured fields are now retrieved via `$page->get($field)` or `$page->{$field}` with safe fallback
- Consolidated the multi-page vs. single-page rendering paths into a single method, ensuring consistent output for both simple Page fields and PageArray fields

---

## [2.2.1] – 2025-05-07
### Added
- Support for **multiple** virtual fields via comma-separated list.  
- New `tooltip_format` parameter (e.g. `tooltip_format=date(d.m.Y)`, `tooltip_format=custom=%.2f`).  
- Centralized tooltip formatting helper `applyTooltipFormat()`.  
- TableField date columns now use `getFormatted()` to respect the PW field’s native output format.  
- Example configs demonstrating combined table- and page-date rendering.

---

## [2.2.0] – 2025-05-07
### Added
- `format_raw` parameter for TableField date re-formatting.  
- Quick-format options for virtual fields: `format=int|number|currency|percent|custom=…`.  
- Enhanced `renderTooltip()` to accept raw strings, Page objects, and TableRow arrays.  
- Tooltip rendering consolidated in the `renderTooltip()` helper.  
- Field-config **notes** always display all available options in the admin UI.

---

## [2.1.0] – 2025-05-06
### Added
- New `tooltip_prefix` and `tooltip_field` parameters for all field types.  
- `tooltip_format` for basic date formatting.  
- Modularized helpers: `renderCell()`, `renderResolvedPageColumn()`, `renderResolvedPageTableColumn()`.

---

## [2.0.0] – 2025-05-06
### Added
- Complete refactor: per-cell logic in `renderCell()`.  
- Virtual fields (`selector=…`) with sorting via GET parameters.  
- Pagination and clickable, sortable column headers.  
- Configurable settings UI via `getModuleConfigInputfields()`.

---

## [1.10.0] – 2025-05-05
### Restored
- Tooltip support for Page and Table fields (`tooltip_field`, `tooltip_prefix`).  
- Virtual field tooltips re-enabled.  
- Auto-suggested tooltip parameters in config, per field type.  
- Correct `d.m.Y H:i` date formatting in tooltips.  
- Restored `label=… (optional)` parameter.

### Changed
- Moved TableField tooltip logic into `renderResolvedPageTableColumn()`.  
- Unified tooltip output to `data-uk-tooltip`.  
- Ensured a space after the tooltip prefix for readability.

### Fixed
- Tooltips were not appearing despite correct configuration.  
- Virtual fields never generated tooltips even when configured.

---

## [1.9.2] – 2025-05-04
### Added
- Virtual columns defined via the “Additional fields” text input.  
- Combined field list from AsmSelect + manual extras.  
- Internally store `user_fields` as JSON.  
- Parameter textareas generated for every real + virtual field.

### Fixed
- Resolved `InputfieldTextTags` issue that prevented parameter fields from appearing.  
- Re-delegated to AsmSelect logic with stable manual-extras support.

---

## [1.9.1] – 2025-05-04
### Added
- New config parameters: `sort_field`, `sort_dir`, `entries_per_page`.  
- `edit_link=1` for linking primitive values to the user edit page.  
- `tooltip_field` and `tooltip_prefix` for all field types.  
- New helper `formatDateValue()` for timestamp formatting.  
- UIKit-conformant tooltips via `title` attribute.

### Changed
- Switched sorting from `PageArray->sort()` to native PHP `usort()`.  
- Pagination now uses `?start=` instead of `?pageNum=`.  
- Column headers show `uk-icon` arrows and toggle direction on click.

### Fixed
- Sorting failure due to invalid `Closure` in `PageArray->sort()`.  
- Duplicate or missing tooltip issues.  
- TableField missing-column error.  
- Missing non-breaking space (`&nbsp;`) between header text and icon.

---

## [1.9.0] – 2025-05-04
### Added
- Modular cell rendering via `renderCell()`.  
- TableField parameters: `table_column=…`, `resolve_page=…`, `as_link=…`, `separator=…`.

---

## [1.8.3] – 2025-05-04
### Fixed
- Fatal error from `PageArray->filter(Closure)` use.  
- Now uses `array_filter()` + `new PageArray()`.

### Changed
- Split `roles` vs. `roleNames` to avoid type mixing.  
- Eliminated inadvertent array/closure overwrites.

---

## [1.8.2] – 2025-05-04
### Changed
- `and` role mode now shows only users with exactly the selected roles.

---

## [1.8.1] – 2025-05-04
### Changed
- Removed title configuration fields.  
- Added `roles_mode` radio for AND/OR.

---

## [1.8.0] – 2025-05-04
### Added
- Role-based user filtering via InputfieldAsmSelect.

---

## [1.7.5] – 2025-05-04
### Fixed
- Removed stray backslashes in `init()`.  
- Title update via `Modules::saveConfig()` now works.

---

## [1.7.4] – 2025-05-04
### Fixed
- Hook switched to `Modules::saveConfig()` (instead of `___saveConfig()`).

---

## [1.7.3] – 2025-05-04
### Changed
- Admin page title now updates automatically on config save.

---

## [1.7.2] – 2025-05-04
### Fixed
- Backslashes removed from `init()`.  
- Config now correctly loaded in `___execute()`.  
- Outputs table or “no fields” notice.

---

## [1.6.9] – 2025-05-04
### Changed
- Removed `page` entry from `getModuleInfo()`.  
- Admin page auto-created in `ready()`.

---

## [1.6.8] – 2025-05-04
### Changed
- Moved config init from `init()` to `ready()` to avoid install-time conflicts.

---

## [1.6.7] – 2025-05-04
### Fixed
- Guarded `init()` against empty config to prevent `[empty]` selector errors.  
- Removed erroneous backslashes.

---

## [1.6.6] – 2025-05-04
### Changed
- Renamed class to `ProcessUserDataTable` for auto page creation.  
- Ensured `getModuleInfo()['page']` is honored.

---

## [1.6.5] – 2025-05-04
### Changed
- Reverted to pure `getModuleInfo()['page']` handling.  
- Removed manual page creation in `___install()`.

---

## [1.6.3] – 2025-05-04
### Fixed
- Added `implements Module` so the `page` definition takes effect.

---

## [1.6.2] – 2025-05-04
### Fixed
- Moved admin-page title change into `___install()`.

---

## [1.6.1] – 2025-05-04
### Fixed
- Handled missing admin page gracefully during installation.

---

## [1.6.0] – 2025-05-04
### Added
- Auto-create menu entry under **Access > user-data-table**.  
- Admin page title editable via module config.

---

## [1.5.0] – 2025-05-04
### Changed
- Replaced repeater UI with AsmSelect + per-field textareas.

---

## [1.4.0] – 2025-05-04
### Added
- Configurable field groups with “Add” button (later deprecated).

---

## [1.3.0] – 2025-05-04
### Fixed
- Replaced broken repeater with working Inputfield wrappers.

---

## [1.2.0] – 2025-05-04
### Fixed
- Removed invalid `setFieldDefaults()` usage for repeater config.

---

## [1.1.0] – 2025-05-04
### Changed
- Full `ConfigurableModule` integration.  
- Column config loaded on `___execute()`.

---

## [1.0.0] – 2025-05-04
### Added
- Initial release with configurable User table.  
- Repeater-style column config.  
- Basic `as_link=1` support for Page fields.  
- Role-based user listing.