# Hydro SAP 应用启动器

This repository contains the static homepage for `https://www.zaza.de5.net`.

## Applications

| Name | URL |
| --- | --- |
| 分数计算工具 | https://fraction.zaza.de5.net |
| 销售报表工具 | https://report.zaza.de5.net |
| Delivery Note 工具 | https://dn.zaza.de5.net |

## Deployment

Deploy `index.html` and `styles.css` to the web root for `www.zaza.de5.net`.

The application launcher only links to the deployed systems. It does not start, proxy, embed, or merge them.

## Domain Mapping

- `www.zaza.de5.net`: unified application launcher
- `fraction.zaza.de5.net`: fraction calculator tool
- `report.zaza.de5.net`: sales report tool
- `dn.zaza.de5.net`: Delivery Note tool

## Quick Deploy

To publish the launcher, point `www.zaza.de5.net` to the static files in this repository.

Recommended layout on the server:

```text
/var/www/zaza/
  index.html
  styles.css
```

Minimal Nginx example:

```nginx
server {
    listen 80;
    server_name www.zaza.de5.net;

    root /var/www/zaza;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

The launcher itself does not proxy the three tools. Each subdomain continues to serve its own application.
