# AIDrafting for Revit — Browser

Install this plugin in Claude to inspect your Revit project and perform model operations you request. It includes the AIDrafting connector address and the Revit workflow skill. An activated AIDrafting installation, enabled browser access, an open Revit project and a running connected computer are required.

In claude.ai, open **Customize → Plugins → Add → Upload plugin** and select this ZIP. Open the plugin's **Connectors** tab, add/connect AIDrafting, sign in to your AIDrafting account and choose the exact Revit computer. Your organization may require its owner to add the connector first. No endpoint or secret needs to be copied.

For the first check ask: **“Check my current Revit project and view without changing the model.”** If project assignment is enabled, approve the displayed connection request in Revit and close the AI Connection dialog. Keep Revit and the computer running while using the connector.

## Install in Claude Code

From the community marketplace (once listed):

```
/plugin marketplace add anthropics/claude-plugins-community
/plugin install aidrafting-browser@claude-community
```

Then run `/mcp`, select **aidrafting**, and sign in to your AIDrafting account to choose your Revit computer.

## What the connector can do

- **Read:** list running Revit instances and open projects on your linked computer, and report the current project, view, Revit version and supported capabilities.
- **Write (only when you ask):** create or change elements, parameters and annotations. Preview tools create elements temporarily and roll them back.
- **C# (optional):** runs only if developer C# execution is enabled in AIDrafting on your Revit PC. It runs with full trust; Claude cannot turn it on.

Access is per computer and tied to your AIDrafting account. With separate project assignment, each project connection must be approved in that Revit window's AI Connection dialog.

## Requirements

- Autodesk Revit open on a Windows PC with AIDrafting installed and activated
- Browser access enabled in AIDrafting
- No modal Revit dialogs open while Claude is working

Для первого подключения загрузите этот ZIP в **Customize → Plugins → Add → Upload plugin**. На вкладке **Connectors** подключите AIDrafting, войдите в аккаунт и выберите компьютер с Revit. Адрес сервера уже настроен. Для проверки попросите: **«Проверь текущий проект и вид Revit, ничего не меняя в модели»**.

[Connection help](https://customers.aydrafting.com/browser-connections?setup=claude) · [Access terms](https://customers.aydrafting.com/terms) · [Privacy](https://customers.aydrafting.com/privacy)
