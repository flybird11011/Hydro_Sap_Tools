# Unified App Launcher Design

## Goal

Create a clean unified homepage for Hydro SAP at `https://www.zaza.de5.net`.
The homepage is an application launcher, not a backend merge or shared business system.
It gives users one entry point for the three existing deployed tools.

## Confirmed URLs

| Application | URL |
| --- | --- |
| 分数计算工具 | `https://fraction.zaza.de5.net` |
| 销售报表工具 | `https://report.zaza.de5.net` |
| Delivery Note 工具 | `https://dn.zaza.de5.net` |

`https://www.zaza.de5.net` will become the unified main entry.
The current tool previously hosted at `www.zaza.de5.net` should move to `fraction.zaza.de5.net`.

## Scope

The first version is a static launcher page with three application cards.
Each card shows:

- Application name
- Short purpose description
- Destination URL
- Primary "打开应用" action

The page does not include login, database storage, server status checks, embedded iframes, or one-click service startup.
Each application remains independently deployed and maintained.

## User Experience

The page should feel like a practical internal application launcher.
It should be fast to scan, calm, and work-focused.
The primary screen should make the three available tools obvious without extra explanation.

Recommended card descriptions:

- 分数计算工具: 用于录取分数、分数线或相关历史工具查询与计算。
- 销售报表工具: 上传 Excel 文件，完成字段映射、预览和销售报表导出。
- Delivery Note 工具: 处理 Delivery Note PDF 和客户资料，生成更新后的 PDF 文件。

## Architecture

Build the launcher as a small static site in the `Hydro_sap` workspace.
The site can be deployed to the web root for `www.zaza.de5.net`.

Suggested initial files:

- `index.html`
- `styles.css`
- optional `README.md` with deployment notes

The static site links directly to the deployed application URLs.
No local integration with the three source project directories is required for the first version.

## Deployment Notes

DNS and hosting should map:

- `www.zaza.de5.net` to the new launcher
- `fraction.zaza.de5.net` to the existing fraction tool
- `report.zaza.de5.net` to the sales report tool
- `dn.zaza.de5.net` to the Delivery Note tool

The launcher implementation should not assume control of the other three deployments.

## Testing

Before completion:

- Open the launcher locally and verify layout on desktop and mobile widths.
- Confirm all three links target the correct HTTPS URLs.
- Check that Chinese text renders correctly.
- Confirm the page works as a static site without a backend.
