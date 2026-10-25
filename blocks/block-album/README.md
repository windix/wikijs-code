# block-album

`block-gallery` 的改版，作为自定义块装在 https://home.windix.au 上。唯一的区别是共享 lightbox：页面上所有 `pool` 相同的 album 在 lightbox 里按页面顺序连成一组，左右键可以跨块切换。不写 `pool` 时整页共用一个池。

文档和跟踪记录：[Wiki.js 3 使用技巧与定制](https://home.windix.au/pve/lxc/120-wikijs/customization)

## 打包

```bash
cd blocks
npm ci
npm run package -- block-album   # 输出 packages/block-album.wkblock
```

然后在 **管理后台 → Content Blocks → Install Block...** 上传。同一个 key 再次上传就是升级，启用状态和配置会保留。

## 升级 Wiki.js 之后

1. 对比新旧版本：`gh api repos/requarks/wiki/compare/<旧版本>...<新版本>`，看 `blocks/block-gallery`、`blocks/shared`、`backend/helpers/wkblock.ts`、`dev/specs/wkblock.md` 有没有改动
2. 如果 gallery 改了，把这个分支 rebase 到新版本的 tag 上，把改动同步到 `component.js`，然后重新打包上传
3. 如果 `.wkblock` 格式版本（目前是 1）变了，必须重新打包

## 和上游的关系

同样的功能已经以 `group` 参数的形式做进 `block-gallery`，在 `feat/gallery-group` 分支，准备提 PR 给 `requarks/wiki`。上游的版本默认不分组。
