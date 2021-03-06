=============================
共通情報
=============================

トレードAPIに共通する情報です。
パラメータなど、API個別の情報はそれぞれのページを参照してください。

事前準備
==============
取引APIを利用するには、`アカウント情報のページ <https://zaif.jp/api_keys>`_ のページからAPI Keyの発行をおこなってください。


リクエスト方法
==============

エンドポイント
--------------

https://api.zaif.jp/tlapi

リクエスト種別
--------------

POST

認証
--------------
取得したAPI Keysを利用して、下記のようにHTTPヘッダを設定し、認証情報を送信します。

.. csv-table::
   :header: "キー", "詳細", "具体例"

   "key", "APIキー", "490f983a-5fab-49b2-b789-9d1f130874d3"
   "sign", "署名", "詳細は下記"

.. note::

    signはPOSTする全てのパラメータ（nonceとmethodおよびメソッド毎のパラメータ）を
    URLエンコードしたクエリ形式(param1=val1&param2=val2)のメッセージとして、Secret Keyを用いてHMAC-SHA512で署名します。

パラメータ
--------------

.. csv-table::
   :header: "キー", "詳細", "具体例"

   "nonce", "1以上の数を実行都度増分して送信します", 23123
   "method", "APIメソッド名", "get_positions"
   "type", "取引タイプ(margin or futures)", "margin"
   "group_id", "グループID（AirFX・先物のみ）", 1

| **注意**
| 信用取引を行う場合はtype='margin'を　AirFX,先物取引を行う場合はtype='futures'を指定してください。
| type='futures'を指定した場合は必ずgroup_idも指定してください。
| その他のメソッド毎の固有のパラメータも全てPOSTパラメータにて送信してください。
| nonceパラメータの値は実効毎に増分されていないとエラーが発生します。また増分量は少数点以下の値にも対応しております。

戻り値
==============
.. code-block:: python

    {
        "success": 1,
        "return": {
            ...
        }
    }

.. csv-table::
   :header: "キー", "詳細", "型"

   "success", "成功フラグ", "int"
   "return", "実行結果", "dict or string"

補足
==============


戻り値
--------------

| 処理に成功した場合、successには1が、returnには実行結果が設定されます。
| 処理に失敗した場合、successには0が、returnにはエラーメッセージが設定されます。
| 戻り値の各項目は値が入っている場合のみ出力されます。
