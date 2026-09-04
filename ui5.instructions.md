---
applyTo: "webapp/**/*.{js,xml,json,properties}"
---

# UI5 conventions (apply to all files under webapp/)

- Modules use `sap.ui.define` with `"use strict"`; no `jQuery.sap.*`, no `sap.ui.getCore()` in application code, no synchronous loading.
- XML views only; dialogs and reusable blocks are fragments loaded via `sap/ui/core/Fragment` and destroyed in `onExit`.
- All UI text comes from `{i18n>key}`; add new keys to `webapp/i18n/i18n.properties` in the same change.
- Models, routes, targets, and OData data sources are declared in `webapp/manifest.json`, never instantiated ad hoc in controllers.
- Check the model type before writing OData code: `sap.ui.model.odata.v2.ODataModel` → `read/create/update/remove`, deferred groups, `submitChanges`; `sap.ui.model.odata.v4.ODataModel` → contexts, list bindings, `submitBatch`, no `read`.
- Filters and sorters are built with `sap/ui/model/Filter` and `sap/ui/model/Sorter` objects.
- Display logic lives in bindings, expression bindings, or `webapp/model/formatter.js`; controllers hold orchestration only.
- Log with `sap/base/Log`; no `console.log`.
- Navigation goes through the component router (`navTo`); views bind in `patternMatched`.
- New logic gets a QUnit test under `webapp/test/unit`; new user flows get an OPA5 journey under `webapp/test/integration`.
- Run the project's lint (`@ui5/linter`, ESLint) before finishing.
