# 公开更新源（私有主仓库配套）

主仓库 `TEH-TheEmptyHouse` 保持私有时，客户端**不能**调用 GitHub API 读 Release。  
请维护一个**公开**仓库（默认名 `TEH-Public-Updates`），只放：

1. 根目录 **`manifest.json`**（本目录里的模板，发版时改版本与链接）
2. **Releases** 附件：`TEH-TheEmptyHouse-windows.zip`（与 `tools/export_windows.ps1` 产出一致）

## 发版步骤

1. 在私有仓库导出：`powershell -ExecutionPolicy Bypass -File tools\export_windows.ps1`
2. 在公开仓库创建 Release，tag 与 manifest 里 `tag` 一致（如 `v0.3.12`），上传 `build\TEH-TheEmptyHouse-windows.zip`
3. 把 `build\update_manifest.json`（导出脚本已生成）或本目录 `manifest.json` 里的 `zip_url` / `page_url` 改成该 Release 的真实地址
4. 将 `manifest.json` 推到公开仓库 **`main` 分支根目录**（客户端固定读 raw 地址）

客户端读取：

`https://raw.githubusercontent.com/Evertworth/TEH-Public-Updates/main/manifest.json`

更换公开仓库名时，改 `scripts/update/github_updater.gd` 里的 `PUBLIC_MANIFEST_URL` 与 `PUBLIC_RELEASES_PAGE`。
