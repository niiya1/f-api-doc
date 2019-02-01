=============================
共通情報
=============================

.. warning::
    決済APIは、Zaif上で決済を行うためのAPIです。決済APIの利用には事業者用アカウントおよびAPI Keyが必要になります。


認証
==============
    決済APIを利用するには、アカウント情報のページからAPI Keyの発行をおこなってください。 取得したAPI Keyを利用して、下記のパラメータを認証情報として、POSTパラメータに付加して送信してください。

    *md5を利用したパターン*
      * key – APIキー。 例: 490f983a-5fab-49b2-b789-9d1f130874d3
      * md5secret – Secret Keyをmd5ハッシュ化した文字列
    *sha1を利用したパターン*
      * key – APIキー。 例: 490f983a-5fab-49b2-b789-9d1f130874d3
      * sha1secret – Secret Keyをsha1ハッシュ化した文字列

    認証方法についてはセキュリティ上の理由により、将来変更される可能性があります。


使用方法
==============

    * https://api.zaif.jp/ecapi にPOSTします。
    * APIのメソッドを "method" というPOSTパラメータで送信します。
    * 全てのAPIメソッドにおいて"nonce"パラメータを1以上の整数にて都度増分して送信します。
    * メソッド毎に必要なPOSTパラメータおよび上記の認証用のパラメータも合わせて送信します。
    * 結果はjsonフォーマットにて返されます。
    * 成功時の結果JSONフォーマットは以下のようになります。

      .. code-block:: python

          {"success":1,"return":{<return>}}

    * 失敗時の結果JSONフォーマットは以下のようになります。

      .. code-block:: python

          {"success":0,"error":"<some error message>"}


nonceパラメータについて
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    nonceパラメータはAPIコールの重複を防く効力を持ち、また、呼び出し側での濫用を抑制することに役立ちます。 APIキー毎のnonceの値については、呼び出し側で管理して下さいますようお願いします。 unixtimeをnonceに利用すると簡単に管理できますが、１秒に１度以上のAPIコールができなくなる可能性があることに注意してください。 2016年2月以降、小数点以下の値も受け付けるようになりましたので、マイクロ秒まで含むunixtimeを利用して管理することが可能になっています。


メソッド
==============

    * `インボイスの作成 createInvoice <http://techbureau-api-document.readthedocs.io/ja/latest/payment/2_individual/1_createInvoice.html>`_
        Bitcoin/Monacoinによる決済の開始時に、インボイスの作成を行います。 決済金額・商品名・通貨などの情報を送信してインボイスを作成し、暗号通貨による決済を開始します。

    * `インボイス情報の取得 getInvoice <http://techbureau-api-document.readthedocs.io/ja/latest/payment/2_individual/2_getInvoice.html>`_
        作成したインボイスの状態を取得します。
        このAPIを利用すると、支払が完了しているかどうかなどについて、ECサイト側から確認することができます。

    * `インボイスの検索 getInvoiceIdsByOrderNumber <http://techbureau-api-document.readthedocs.io/ja/latest/payment/2_individual/3_getInvoiceIdsByOrderNumber.html>`_
        注文番号を使用してインボイスを検索します。 暗号通貨決済用のインボイスには有効期限があるため、ひとつの注文から複数のインボイスを発行する必要がある可能性があります。
        また、Bitcoinで決済を選択したが、やはりMonacoinで決済したい、などという場合もあるかと思います。
        Zaif決済APIでは、インボイスの作成時に注文番号の重複チェックは行なわないようになっており、同じ注文番号から複数のインボイスを発行することが可能になっています。

    * `インボイスのキャンセル cancelInvoice <http://techbureau-api-document.readthedocs.io/ja/latest/payment/2_individual/4_cancelInvoice.html>`_
        作成したインボイスを取消します。
        支払が完了していたり既に有効期限が切れている場合はエラーとなります。



インボイスの表示
====================

    作成したインボイスから支払フォームを表示することにより、利用者からBitcoin/Monacoinによる支払いを促します。 支払いフォームのURLは

    * https://zaif.jp/invoice/form/{invoiceId}

    となります。{invoiceId}はインボイスの作成時に発行されたIDになります。
    下記のようにしてiframeによる表示を行うことも可能です。

    .. code-block:: python

        <iframe id="zaif_ec_iframe"
        scrolling="no"
        allowtransparency="true"
        frameborder="0"  src='https://zaif.jp/invoice/iframe/{invoiceId}'
        style='width:500px; overflow: hidden; padding:10px;'></iframe>


    また、インボイス作成時に取得したデータを利用し、事業者様のECサイト上で独自にフォームを表示していただくことも可能です。
