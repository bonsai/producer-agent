# producer-agent

マーケティングエージェントの調査結果を受け取り、**企画（project concept）・計画（execution plan）・実行単位（workflow task set）**へ変換するプロデューサーエージェントです。

> マーケティングエージェントは「何が起きているか、誰に何の機会があるかを調べる」。
> producer-agentは「何をやるかを決め、プロジェクトとして成立させ、実行可能な仕事へ分解する」。

## パイプライン

```text
marketing.research-packet.v1
        ↓ trace / frame
producer.project-concept.v1
        ↓ scope / sequence / resource
producer.execution-plan.v1
        ↓ decompose
workflow.task-set.v1
        ↓ execute
skills + tools + owners + done conditions
```

## 責務境界

producer-agentは、市場データを勝手に作ったり、マーケティング調査を置き換えたりしません。入力された調査パケットの根拠・信頼度・欠測・リスクを保持し、企画判断と計画判断を明示します。企画の採用・保留・却下を記録し、採用された企画だけをWorkflow Taskへ分解します。

## 入力

`marketing.research-packet.v1` は、少なくとも市場シグナル、対象／オーディエンス、ニーズ、機会、リスク、信頼度、出典を含みます。加えて、予算・期間・能力・除外条件・成功指標を `producer.constraints.v1` として受け取ります。

## 出力

| 出力型 | 内容 |
|---|---|
| `producer.project-concept.v1` | 問題、対象、価値提案、企画、スコープ、非目標、リスク |
| `producer.execution-plan.v1` | 成果、マイルストーン、依存関係、資源、指標、リスク、判断履歴 |
| `workflow.task-set.v1` | skill、tool、input、output、owner、done condition付きの実行タスク |

## 変換の仕事

`research-to-concept` は調査を企画へ変換し、`concept-to-plan` は企画を実行可能な計画へ変換し、`plan-to-tasks` は計画をWorkflow Taskへ変換します。各変換は入力・出力・検証条件を保持します。

## 原則

根拠のない市場判断を作らないこと、仮説と事実を分離すること、スコープと非目標を同時に決めること、タスクに完了条件を持たせること、そして未承認の外部公開・破壊的変更・費用発生を実行しないことを基本とします。
