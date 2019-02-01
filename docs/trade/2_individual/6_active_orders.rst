=============================
active_orders
=============================


現在有効な注文一覧を取得します（未約定注文一覧）。

パラメータ
==============
.. csv-table::
   :header: "パラメータ", "必須", "詳細", "型", "デフォルト"
   :widths: 5, 5, 20, 10, 5

   "currency_pair", "No", "取得する通貨ペア。公開情報APIのcurrency_pairsで取得できるものが指定できます。指定なしで全ての通貨ペアの情報を取得します。", "str(例 btc_jpy)", "全てのペア"
   "is_token", "No", "【非推奨、削除予定】true：カウンターパーティトークンの情報を取得 false：カウンターパーティトークン以外の情報を取得", "bool", "false"
   "is_token_both", "No", "【非推奨、削除予定】true：全てのアクティブなオーダー情報を取得 false：currency_pairやis_tokenに従ったオーダー情報を取得", "bool", "false"

戻り値
==============
.. code-block:: python

    {
        "success": 1,
        "return": {
            "184": {
                "currency_pair": "btc_jpy",
                "action": "ask",
                "amount": 0.03,
                "price": 56000,
                "timestamp": 1402021125,
                "comment" : "demo"
            }
        }
    }

      is_token_bothがtrueの時は下記

    {
       "success": 1,
       "return": {
           "active_orders": {
               "184": {
                   "currency_pair": "btc_jpy",
                   "action": "ask",
                   "amount": 0.03,
                   "price": 56000,
                   "timestamp": 1402021125,
                   "comment" : "demo"
               },
               "token_active_orders": {
                   "235": {
                       "currency_pair": "kaori_jpy",
                       "action": "ask",
                       "amount": 0.3,
                       "price": 10,
                       "timestamp": 1402064525,
                       "comment" : "demo"
                   }
               }
           }
       }
    }


.. csv-table::
   :header: "キー", "詳細", "型"

   "184(一例であり、注文idによって変わります)", "order_id(注文id)", "int"
   "currency_pair", "通貨ペア", "str"
   "action", "bid(買い) or ask(売り)", "str"
   "amount", "数量", "int"
   "price", "価格", "int"
   "timestamp", "発注日時", "UNIX_TIMESTAMP"
   "comment", "注文のコメント", "str"
