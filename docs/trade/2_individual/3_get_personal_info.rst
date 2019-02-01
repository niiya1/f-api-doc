=============================
get_personal_info
=============================


チャットに使用されるニックネームと画像のパスを返します。

パラメータ
==============
なし

戻り値
==============
.. code-block:: python

    {
        "success": 1,
        "return": {
            "ranking_nickname": "ニックネーム",
            "icon_path": "https://abs.twimg.com/sticky/default_profile_images/default_profile_0_normal.png"
        }
    }

.. csv-table::
   :header: "キー", "詳細", "型"

   "ranking_nickname", "ニックネーム", "str"
   "icon_path", "画像のパス", "str"
