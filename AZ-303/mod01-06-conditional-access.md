
# Azure AD 条件付きアクセス (conditional access)

「セキュリティの既定値（群）＝有効」よりも柔軟で強力なアクセス制御を行うための機能。条件付きアクセスを使用する場合は、「セキュリティの既定値（群）」は無効化する。

条件付きアクセスでは「セキュリティの既定値（群）＝有効」の場合の動作をすべて実装することができ、さらに以下のような条件に基づくカスタマイズが可能。

- ユーザー/グループ
- アプリ
- アクセスに使用する使用するデバイス
- アクセス元のネットワーク
- その他（カスタムの「利用条件」ドキュメントへの同意を求める等）

https://docs.microsoft.com/ja-jp/azure/active-directory/conditional-access/overview

Azure portal ＞ Azure AD ＞ セキュリティ ＞ 条件付きアクセス

![](images/ss-2022-09-26-10-44-22.png)

■条件付きアクセスとは？

特定の条件が発生したときにアクセス要件を適用することができる。

例: ユーザーが会社のネットワーク外からAzure ADにサインインする場合に、多要素認証(MFA)を使用する必要がある

条件によって、必要な場合は適切なアクセス制御を適用（MFAを要求するなど）して組織のセキュリティを維持し、必要でない場合は、（MFAの要求をスキップするなどして）ユーザーの邪魔にならないようにすることができる。

■セキュリティの既定値（群）＝有効の場合との違い

基本的な違い:

条件付きアクセスのほうが、「セキュリティの既定値（群）＝有効」よりも柔軟で強力。「条件付きアクセスポリシー」を複数定義できる。

MFAの観点での比較:

- セキュリティの既定値（群）＝有効
  - 管理者ユーザーがサインインする際は常にMFAを要求
  - 一般ユーザーがサインインする際はMFAが必要になる場合がある
    - 場所、デバイス、役割、タスクなどの要因に基づいて、ユーザーにMFAを要求
- 条件付きアクセス
  - 管理者が指定した条件に該当する場合のみMFAを要求する


■「条件付きアクセスポリシー」作成例

- 名前: mobile-mfa-policy
- （割り当て）「すべてのユーザー」 が
- （クラウド アプリまたは操作）「Office 365」 に
- （条件＞デバイス）「iOS」または「Android」 を使用してアクセスする場合に
- （アクセス制御）「多要素認証(MFA)を要求」 した上で
- （アクセス制御）アクセスを許可する（アクセス権を付与）

![](images/ss-2022-09-26-10-55-49.png)

![](images/ss-2022-09-26-10-56-24.png)

![](images/ss-2022-09-26-10-56-52.png)

![](images/ss-2022-09-26-10-57-24.png)

■ポリシーの有効化オプション

![](images/ss-2022-09-26-10-59-04.png)

- レポート専用: 「レポート専用モード」で運用（後述）
- オン: ポリシーをオンにする（条件に基づき、実際のアクセスが許可・拒否される）
- オフ: ポリシーをオフにする（条件に基づくアクセス制御を行わない。仮保存）

■レポート専用モード

https://learn.microsoft.com/ja-JP/azure/active-directory/conditional-access/plan-conditional-access#set-up-report-only-mode

レポート専用モードを使用すると、管理者は、環境で条件付きアクセス ポリシーを有効にする前に、その影響（ポリシーが正しく動作しているかどうか、どのポリシーがアクセスに影響するか、など）を評価できる。

本番環境で適用する前に、ポリシーをレポート専用モードで構成して一定期間様子を見る。


■Azure portalへのアクセスに対する条件を設定するには？

https://learn.microsoft.com/ja-jp/azure/active-directory/conditional-access/concept-conditional-access-cloud-apps#microsoft-azure-management

クラウドアプリとして「Microsoft Azure Management」を選択する。

■テンプレートから新しいポリシーを作成する

よく使われるパターンのポリシーを簡単に作成できる機能。

![](images/ss-2022-09-26-11-36-36.png)

![](images/ss-2022-09-26-11-37-10.png)

たとえばテンプレート「Azure管理に多要素認証を必要とする」を選択すると、クラウドアプリとして「Microsoft Azure Management」を選択し、有効化オプションで「レポート専用」に設定したポリシーが作成される。作成されたポリシーはあとからカスタマイズが可能。

■ネームド ロケーション（Named location）

![](images/ss-2022-09-26-11-06-48.png)

https://docs.microsoft.com/ja-jp/azure/active-directory/conditional-access/location-condition#named-locations

ユーザーのアクセス元の「国」や「IPアドレス範囲」に、わかりやすい名前をつける機能。

つけた名前は、ポリシーの「条件」の「場所」で利用することができる。

- 「国の場所」（Countries location）
  - 1つ～複数の国（「日本」「台湾」など）を選択して、名前をつける機能。
  - アクセス元の国の特定には、「アクセス元のIPアドレス」や、「GPS」（モバイル デバイスにインストールされたMicrosoft Authenticatorアプリから送信された緯度経度情報）が使用される
- 「IP範囲の場所」（IP ranges location）
  - パブリックのIPアドレス範囲を指定して、名前をつける

たとえば、「日本」と「台湾」に拠点がある企業では、この2つの国を選択して「アジア拠点」といった名前をつけて「ネームドロケーション」として保存する。

![](images/ss-2022-09-26-11-08-51.png)

![](images/ss-2022-09-26-11-11-02.png)

すると、「条件付きアクセスポリシー」の「条件＞場所」で「アジア地域」を指定できる。これで、日本と台湾の拠点からのアクセスを許可または拒否する、といった条件を作成できる。

![](images/ss-2022-09-26-11-12-10.png)

■多要素認証の信頼できるIPの構成

![](images/ss-2022-09-26-11-07-08.png)

![](images/ss-2022-09-26-11-07-36.png)

https://docs.microsoft.com/ja-jp/azure/active-directory/authentication/howto-mfa-mfasettings#trusted-ips

Azure AD MFA の 「信頼できる IP」機能を使用すると、定義された IP アドレス範囲からサインインするユーザーに対する多要素認証がバイパス（迂回）される。

会社のイントラネットなど、「安全と判断されるIPアドレス」から、Azure ADにサインインする場合に、MFAのチェックを省略することができる。

■「利用規約」（使用条件、terms of use, TOU)への同意を求める

https://learn.microsoft.com/ja-jp/azure/active-directory/conditional-access/require-tou

特定の アプリにアクセスする前に「利用規約」への同意を要求することができる。

あらかじめPDF等で利用規約の文書を作成しておき、アプリの利用規約として登録する。

![](images/ss-2022-09-26-11-31-08.png)

条件付きアクセスポリシーを作成する際に、「条件」でその利用条件を指定する。

![](images/ss-2022-09-26-11-31-40.png)

すると、エンドユーザーがアプリを使用する際に、設定した利用規約の文書が表示される。利用規約に同意することで、アプリへのアクセスが許可される。

