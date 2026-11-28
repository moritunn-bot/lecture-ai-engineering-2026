# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：glossary_search_glossary、glossary_get_lecture_summary
- STEP 2 の [tool call]：glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]：
- STEP 4 の [tool call]：
- 気づき・疑問：MCPサーバーとしてツールを公開すると、エージェント側を変えなくても起動時に一覧が取得され、第3回と同じ関数がMCP経由で呼び出されることが確認できた。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：`app/mcp_server.py` に `server.tool()(tools.get_lecture_summary)` を1行追加して保存し、エージェント側のコード（`app/mcp_agent.py`）や設定（`app/mcp_servers.json`）は変更せずに、`--list-tools`、`--trace` 付きの質問実行、`uv run pytest -q` を行った
- 結果：`--list-tools` で `glossary_get_lecture_summary` が追加されツール数が1個から2個になったことを確認した。また、「第2回では何を学びますか?」の `--trace` 実行で `glossary_get_lecture_summary({'lecture': 2})` が呼ばれ、第2回の要点が回答に反映された。`uv run pytest -q` は21件すべて合格（passed）した。
- 気づき・疑問：エージェント側のコードや設定を変更しなくても、起動時にMCPサーバーからツール一覧を動的に取得するため、サーバー側で公開するだけでエージェントから利用できる仕組みが分かりやすかった。第5回までの直接関数登録と比べ、ツール管理をサーバー側に分離できる点にメリットを感じた。
