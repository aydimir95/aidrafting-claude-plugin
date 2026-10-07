---
name: revit-browser-assistant
description: Inspect Autodesk Revit and perform requested model or annotation operations through the AIDrafting browser connector. Use when a user asks to connect to their Revit computer, check a project or view, or work on a Revit model through AIDrafting.
---

# AIDrafting in a browser

Use the AIDrafting connector already installed with this plugin. Authentication happens in its account connection flow. Never ask the user to copy an MCP URL, credentials, pairing secrets or a local file path. A running Revit computer with activated AIDrafting and browser access enabled is required. The account connection selects a computer, not a Revit project.

## Establish the exact project

1. Discover live hosts with `list_revit_instances`, then inspect open documents with `list_revit_documents` for the returned `instanceId`. Use the returned `instanceId` and `documentId`; do not invent IDs or silently choose a different computer, instance or project. Ask which project if the user's request and discovered context do not identify one.
2. Respect the user's chosen connection mode. For ordinary access, use `connection: "ordinary"` and the explicit discovered `target` on subsequent model tools. Do not enable protected mode merely to test the connector.
3. If the user uses separate project assignment, call `request_revit_project_connection` for the chosen discovered project. Show only the request label and short context code. The human approves it in that Revit window's AI Connection dialog. Keep the returned secret connection token only in this conversation, never display it or write it to files. Poll `get_revit_project_connection` with the same token while pending. The assistant cannot approve, revoke or reassign itself. A browser transport session is not proof of an individual chat's identity.
4. Once the chosen mode is ready and the AI Connection dialog is closed, call `get_current_view_info` using that connection and exact target. Report the confirmed project, view, actual Revit version and supported capabilities. The initial connection check is read-only: do not create elements, change parameters, run C# or use transactional previews to prove connectivity.

Never switch to ordinary access after an invalid, expired or unavailable protected connection. Only use ordinary access when the user selected it. Preserve the target when a user explicitly turns off separate project assignment. An unavailable host or closed document requires reconnecting the intended project; it does not authorize selecting another one.

## Work on the model

Inspect relevant context before a requested change. Use exact element IDs from the current model, preserving decimal strings when numeric precision would be lost. Follow each tool's units, capabilities and transaction behavior. Preview tools may create and roll back Revit elements, so a preview is still a model operation and is excluded from the initial connection test.

Perform only changes authorized by the user. Report confirmed results and failures. A timeout, closed connection or lost response does not prove rollback. Inspect the same model before deciding whether to retry a change; never automatically repeat a possibly completed write.

Developer C# execution follows the user's AIDrafting setting on the Revit PC. Do not enable it or bypass a disabled setting. C# has full trust when enabled; project assignment is not a C# sandbox.

If access fails, direct the user to the plugin's Connect action and AIDrafting browser-connection page to sign in or select the intended computer. On the PC, verify Revit is open, AIDrafting is activated, browser access is enabled and modal Revit windows are closed. Respect offline, revoked and expired access results instead of trying another account or computer.
