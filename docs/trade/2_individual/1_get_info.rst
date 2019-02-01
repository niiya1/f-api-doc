=============================
get_info
=============================


現在の残高（余力および残高・トークン）、APIキーの権限、過去のトレード数、アクティブな注文数、サーバーのタイムスタンプを取得します。

パラメータ
==============
なし

戻り値
==============
.. code-block:: python

    {
        "success":1,
        "return":{
            "funds":{
                "jpy":15320,
                "btc":1.389,
                "xem":100.2,
                "mona":2600,
                "pepecash":0.1
            },
            "deposit":{
                "jpy":20440,
                "btc":1.479,
                "xem":100.2,
                "mona":3200,
                "pepecash":0.1
            },
            "rights":{
                "info":1,
                "trade":1,
                "withdraw":0,
                "personal_info":0,
                "id_info":0,
            },
            "trade_count":18,
            "open_orders":3,
            "server_time":1401950833
        }
    }

.. csv-table::
   :header: "キー", "詳細", "型"

   "funds", "資産の残高", "dict"
   "deposit", "資産の残高に注文情報を加味したもの", "dict"
   "rights", "キーが保持している権限", "dict"
   "trade_count", "実行したトレード数", "int"
   "open_orders", "アクティブな注文数", "int"
   "server_time", "UNIX時間で換算された日本時間", "int"


deposit計算式
==============
| depositは現在の資産の残高に注文情報を加味したものになります。
| 買い注文が存在する場合、その注文の値段と量をかけ合わせたもので、
| 売り注文が存在する場合は、その注文の量のみが加味されます。


補足
==============
取得できる情報は、APIを実行した時点のものになります。

