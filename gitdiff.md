## PRのみで見せかけの差分が発生するケース

### テスト１

### テスト2

### 順序（fix2）

- main -> releaseブランチにマージ
- mainブランチからfix1ブランチを切って修正

### 順序（fix2）

- main -> releaseブランチにマージ
- mainからfix1を切る
- mainからfix2を切る
- fix1/fix2をmainにPRでマージ
- fix1/fix2をreleaseにPRでマージ
- main->releaseのPRを作ると、github上で、fix2の差分だけ、見せかけの差分が表示される

- fix1/2が入った後の時点からfix3などで、main/releaseにマージすることで、merge-baseが共通化されるので、解消する

### 詳細

GitHubのPRは共通祖先（merge-base）を基準に差分を表示する。
fix1/fix2をそれぞれmainとreleaseへ独立してマージしたことで、fix1とfix2の両方が共通祖先候補になるコミットグラフになった。
その結果、たとえばfix1側を基準に比較すると、fix2が「merge-base以降の変更」としてPR上に表示される。
ただし実際にはreleaseにもfix2は入っているため、見かけ上の差分
