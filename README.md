# Charles's Blog

由 [Hexo](https://hexo.io/) 建置，主題為 [Wikitten](https://github.com/zthxxx/hexo-theme-Wikitten)。

## 本機開發

```bash
npm install
npx hexo server   # http://localhost:4000
```

## 寫新文章

```bash
npx hexo new "文章標題"
```

會在 `source/_posts/` 產生一個新的 Markdown 檔案，寫完後 commit + push 到 `master` 即可（見下方部署流程）。

## 部署

`.github/workflows/deploy.yml` 會在每次 push 到 `master` 時自動執行 `hexo generate`，並把產生的 `public/` 內容推到 `gh-pages` 分支。

**一次性設定（初次啟用需要手動做）：**在 repo 的 Settings → Pages，將 Source 設定為 `gh-pages` 分支（root）。之後就完全自動化，不用再手動 `hexo generate` 或複製檔案。
