# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：glossary_search_glossary
- STEP 2 の [tool call]：glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]：fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
- STEP 4 の [tool call]：aws_aws___search_documentation({'search_phrase': 'Amazon S3 バージョニング 概要', 'topics': ['general']})
- 気づき・疑問：設定ファイルに command を書くと自分の環境で起動し、url を書くと外部のサーバーに
  接続する違いを、実際に確かめられた。ツールは glossary の1個から、fetch、aws を足して7個に
  増えたが、エージェントのコードは変えていない。aws は質問の内容が外部に送られる点に注意が必要だと感じた。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：app/mcp_server.py に server.tool()(tools.get_lecture_summary) を1行足した。
  エージェント側（mcp_agent.py）は変更していない
- 結果：ツール一覧が7個から8個に増え、glossary_get_lecture_summary が表示された。
  「第2回では何を学びますか？」の質問で
  glossary_get_lecture_summary({'lecture': 2}) が呼ばれ、第2回（ファインチューニングとLoRA）の
  要点で回答できた。pytest は21件すべて通った
- 気づき・疑問：エージェントは起動のたびにサーバーへツール一覧を問い合わせるため、サーバー側に
  1行足すだけで、エージェント側を変えずに新しいツールが使えた。モデルは質問の内容から、
  2つのツールのうち適切なほう（回の要点を返すツール）を選び、引数 lecture に 2 を渡していた。
