# humanizer

<p>
  <a href="README.md">English</a> |
  <a href="README.zh.md"><b>繁體中文</b></a>
</p>

蠶食自 [blader/humanizer](https://github.com/blader/humanizer) v2.11.1（MIT），2026-08-18。

移除英文散文裡的 AI 寫作痕跡，依據 Wikipedia WikiProject AI Cleanup 的「Signs of AI writing」35 條 pattern。

## 為什麼引入這個

繁中那側已有既有的句構規則加上寫作 skill 的嚴格自檢；英文那側原本完全沒有語氣品管——翻譯服務跑的是 flash 級模型，AI 痕跡比 Sonnet 改寫重得多。

射程：英文散文。與繁中規則不重疊。

## 本地調整（2026-08-19）

上游原樣是單一 456 行的 SKILL.md。**35 條 pattern 的文字一字未改**，調整全在結構與包裝：

| 調整 | 為什麼 |
|---|---|
| 35 條 pattern 移到 `references/PATTERNS.md` | body 從 6608 tok 降到 2194 tok。原本超過 5000 token 的 compaction 截斷線，壓縮後尾端會靜默消失——掉的正好是「Check for false positives」「What not to flag」「How to return the result」「Rewrite process」，留下的是 35 條「要抓什麼」。那會讓它變成只會抓、不會放、也不知道怎麼交付的工具 |
| body 保留 35 條的編號索引 | `§7`、`§14` 這類交叉引用要能解析，而且 agent 要知道射程有多大才知道該不該去讀 |
| description 改成關鍵字列表 + 中文觸發語 | 所有 skill 的 description 常駐在 system prompt，共用同一份 listing budget |
| 補 `LICENSE` | 上游是 MIT，而原本的出處署名寫在 SKILL.md 第 452 行——正好在截斷線之後。授權聲明不該只活在會被截斷的位置 |
| 補 `.gitignore` | 比照其他 skill，排除 `__pycache__` 與 `lessons.md` 這類本地軌跡 |

**沒改的**：35 條的內容與措辭、寫作語氣、判斷標準、`How to return the result` 的三種模式、`Rewrite process` 的四步。上游的風格是它被社群採用的原因，不動。

**沒設 `disable-model-invocation`**：這是「檢查我剛寫的東西」型工具，讓 model 自己在適當時機叫它才有價值。

## 上游

- 來源：https://github.com/blader/humanizer （MIT）
- 版本：2.11.1
- 上游另有給 Codex 用的 `agents/openai.yaml`，未取用（主 harness 是 Claude Code）
- pattern 目錄源自 Wikipedia「Signs of AI writing」，CC BY-SA 4.0
