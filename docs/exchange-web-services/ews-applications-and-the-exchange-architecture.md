---
title: EWS アプリケーションと Exchange のアーキテクチャ
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
localization_priority: Normal
ms.assetid: c10f308a-65bb-4a0b-8fdd-b4a61503f0fd
description: EWS が Exchange アーキテクチャで動作する仕組みと、EWS が依存するプロトコルについて説明します。
ms.openlocfilehash: 1fbc1e68edbca829555fbbf1b9f0bc4723da9524
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19758901"
---
# <a name="ews-applications-and-the-exchange-architecture"></a>EWS アプリケーションと Exchange のアーキテクチャ

EWS が Exchange アーキテクチャで動作する仕組みと、EWS が依存するプロトコルについて説明します。
  
Exchange Web Services (EWS) は、Exchange Online、Office 365 の一部としての Exchange Online、Exchange 2007 以降のオンプレミス バージョンの  Exchange からのメール メッセージ、会議、連絡先などのメールボックス アイテムにアプリケーションがアクセスするためのクロスプラットフォーム API です。 [EWS アプリケーション](ews-application-types.md)は、SOAP ベースの XML メッセージで要求を送信することによって、ローカルまたはリモートでメールボックス アイテムにアクセスできます。 SOAP メッセージは、アプリケーションとサーバーの間で送信されるときに、HTTP メッセージに埋め込まれます。つまり、アプリケーションが HTTP 経由で XML を投稿できる場合に限り、EWS を使用して Exchange にアクセスできます。 
  
## <a name="exchange-architecture-overview"></a>Exchange のアーキテクチャ概要
<a name="bk_techarch"> </a>

次の図は、Exchange 2013 および Exchange Online と通信する場合に EWS アプリケーションで使用される認証方法および通信パスを示しています。EWS アプリケーションの観点からすると、通信パスは同じであり、認証方法だけが多少異なります。主な違いは、Exchange バックエンドを見ることができるかどうかということです。
  
**図 1. EWS アプリケーションと Exchange オンプレミス アーキテクチャ**

![Exchange オンプレミス アーキテクチャのコンテキストにおける EWS アプリケーションを表示している図。この図のコンポーネントについては、このイメージおよび次のイメージの後に続くテキストの項目 1 から 8 を参照してください。](media/Ex2013_ArchitecturesOverview.png)
  
図 2 は、Exchange Online と通信するときに EWS アプリケーションで使用される、図 1 に示したのと同じ通信パスを示しています。
  
**図 2. EWS アプリケーションと Exchange Online アーキテクチャ**

![EWS アプリケーションのための Exchange Online アーキテクチャのコンテキストにおける EWS アプリケーションを表示している図。この図のコンポーネントについては、このイメージに続くテキストの項目 1、2、3、6、および 9 を参照してください。](media/Ex2013_Architectures_Online.png)
  
図に示されているコンポーネントは次のとおりです。
  
1. EWS アプリケーション - これは、[クライアント、ポータル、またはサービス アプリケーション](ews-application-types.md)であり、クライアントまたは Exchange オンプレミスのクライアント アクセス サーバー上にインストールできます。 EWS マネージ API を使用して EWS アプリケーションを開発する場合、EWS マネージ API アセンブリをクライアントにインストールし、[アプリケーションで再配布](redistribution-requirements-for-the-ews-managed-api.md)する必要があります。
    
2. SOAP XML メッセージ - SOAP エンベロープ内の XML メッセージであり、クライアント アクセス サーバー上の Services.wsdl ファイルに準拠した HTTP/S メッセージに埋め込まれています。HTTPS は、Exchange オンプレミスで推奨されており、Exchange Online では必須です。 
    
3. 認証方法 - EWS メッセージには、基本認証、NTLM 認証 (Windows 統合認証) または OAuth 認証の情報が HTTP ペイロードの一部として含まれます。 
    
4. ロード バランサー - ロード バランサーは、クライアント アクセス サーバー アレイ内のクライアント アクセス サーバーにメッセージを配信します。このコンポーネントは、Exchange オンプレミス アーキテクチャでのみ表示されます。
    
5. クライアント アクセス サーバー アレイ - クライアント アクセス サーバーは、クライアント アクセス サーバー アレイと呼ばれる負荷分散グループに編成されています。 個々のクライアント アクセス サーバーは、認証、制限付きリダイレクト、およびプロキシ サービスを提供します。 クライアント アクセス サーバー自体はデータのレンダリングを実行しません。クライアント アクセス サーバーにはキューに入れられるデータまたは格納されるデータは何もありません。これは、最小限の機能を備えたステートレス サーバーであり、要求を認証し、自動検出を実行してから、メールボックス サーバーへの要求をプロキシ処理します。 クライアント アクセス サーバーは、ユーザーのデータをホストしているメールボックス サーバーと 1 対 1 のリレーションシップを維持します。 HTTP プロトコル (自己署名入りの証明書を使用して SSL を経由してセキュリティで保護されます) は、クライアント アクセス サーバーとメールボックス サーバーの間で使用されます。 このコンポーネントは、Exchange オンプレミス アーキテクチャでのみ表示されます。
    
6. 自動検出サービス - 自動検出サービスは、Active Directory Domain Services (AD DS) にアクセスすることでサービス検出を実行し、ユーザーのデータのアクティブ コピーをホストしているメールボックス サーバーのメールボックスのバージョンと場所を取得します。
    
7. EWS サービス - EWS サービスは、次の 3 つのファイルで記述されます。Services.wsdl、Messages.xsd、Types.xsd、および EWS マネージ API のアセンブリです。Services.wsdl はクライアントとサーバーの間のコントラクトを記述し、Messages.xsd は要求および応答の SOAP メッセージを定義し、Types.xsd は SOAP メッセージで使用される要素を定義します。以前のバージョンのスキーマが存在する場合でも、Messages.xsd と Types.xsd には常に最新バージョンのスキーマが含まれます。Services.wsdl、Messages.xsd、Types.xsd はクライアント アクセス サーバーで利用可能ですが、実際にはスキーマの検証で使用されないことに注意してください。これらは参照目的でのみ提供されます。EWS マネージ API アセンブリは、サーバー側の EWS クライアント アプリケーションに提供され、クライアント アクセス サーバーだけでなく、すべての Exchange Server の役割で展開されます。このコンポーネントは、Exchange オンプレミス アーキテクチャでのみ表示されます。
    
    機能が使用可能かどうかは、アプリケーションが対象とする EWS のスキーマのバージョン次第です。 EWS のスキーマは後方互換性と前方互換性を持つため、Exchange  2007 SP1 などの以前のバージョンのスキーマを対象とするアプリケーションを作成する場合、アプリケーションは Exchange 2010 SP2 のサービスや Exchange Online など、後のバージョンのスキーマでも動作します。 機能および機能の更新はスキーマによって決定されるため、クライアント アプリケーションに実装する EWS 機能を対象としているもののうち、最も古い共通のコード ベースを使用することをお勧めします。 多くのアプリケーションは Exchange2007_SP1 バージョンを対象にできます。なぜなら、Exchange 2007 SP1 のスキーマには、Exchange のストアのアイテムやフォルダーを操作するための Exchange のほとんどすべての主要機能が含まれているためです。 詳細については、[EWS のクライアント機能](ews-client-design-overview-for-exchange.md#EWSFeatures)を参照してください。
    
8. データベース可用性グループ (DAG) - メールボックス サーバーを 1 つの可用性の高い DAG にまとめら、1 つまたは複数のデータ センターに展開することができます。メールボックス サーバーは、メールボックス データベースを含んでおり、サーバー上のアクティブ メールボックスのすべてのアクティビティを処理します。データを処理、表示、格納するすべてのコンポーネントは、メールボックス サーバー上にあります。クライアントはメールボックス サーバーに直接接続しません。すべての接続はクライアント アクセス サーバーによって処理されます。このコンポーネントは、Exchange オンプレミス アーキテクチャでのみ表示されます。
    
9. Exchange Online および Office 365 の一部としての Exchange Online - クラウド ベースのサービスとして Exchange の機能を提供するホスト型のメッセージング ソリューション。
    
EWS アプリケーションが Exchange ストアから情報を要求すると、SOAP 規格に準拠した XML 要求メッセージが作成され、Exchange サーバーに送信されます。Exchange サーバーは要求を受信すると、クライアントによって提供される資格情報を検証し、要求データの XML を自動的に解析します。次に、サーバーは、要求された厳密に型指定されたオブジェクトとそのプロパティを表す XML データを含む SOAP 応答を作成します。XML データは、HTTP 応答でアプリケーションに送り返されます。アプリケーションは、XML を逆シリアル化し、そのデータを使用して厳密に型指定されたオブジェクトを再構成します。
  
## <a name="protocols-and-standards-that-ews-applications-must-support"></a>EWS アプリケーションでサポートする必要があるプロトコルおよび規格
<a name="bk_standards"> </a>

Exchange サーバーと通信するには、EWS アプリケーションは次のプロトコルと規格をサポートしている必要があります。
  
**表 1. プロトコル**

|**プロトコル**|**使用方法**|
|:-----|:-----|
|HTTP/S  <br/> |クライアントがインターネット上にあるかイントラネット上にあるかにかかわらず、EWS アプリケーションがネットワーク経由で Exchange データベースのデータにアクセスできるようにします。  <br/> |
|SOAP 1.0  <br/> |メッセージング ペイロードの周囲にエンベロープを形成します。EWS では、SOAP エンベロープのさまざまな部分を使用して SOAP プロトコルを実装し、さまざまな機能を実現します。SOAP ヘッダーは、偽装する場合や、バージョン管理データを提供する場合に使用されます。SOAP 本体は、実行する操作および操作に送信されるデータについての情報を提供します。SOAP は、呼び出す操作を記述する WSDL に依存します。  <br/> |
|WSDL 1.0  <br/> |Services.wsdl ファイルで、EWS 操作の呼び出しに使用されるバインド、操作、プロパティについて記述します。このファイルは、参照されるスキーマ ファイルと共に、EWS アプリケーションと Exchange サーバーの間のコントラクトを構成し、ベンダー固有のツールと共に使用され、プラットフォーム固有のアプリケーションを作成します。WSDL ファイルは、Web サイトのルートにある、EWS 仮想ディレクトリに配置されています。  <br/> |
|トランスポート層セキュリティ (TLS)/SSL  <br/> |インターネットやイントラネット上にセキュリティで保護された Web 通信を提供します。TLS を使用すると、アプリケーションはサーバーを認証でき、オプションでサーバーが EWS アプリケーションを認証できます。また、通信の暗号化によってセキュリティ チャネルが提供されます。TLS は最新バージョンの SSL (Secure Sockets Layer) プロトコルです。  <br/> |
|XML/XSD  <br/> |Exchange サーバーとクライアント間で情報を交換するための汎用のメッセージ形式を提供します。XML は、複雑な Exchange データベースのデータを、定義された構造でクライアント アプリケーションに提供します。XML の長所は、EWS アプリケーションおよびサーバーが共通のプラットフォームを共有しない場合でもデータを交換できるという点です。  <br/> |
   
さらに、EWS アプリケーションは、以下の認証規格をサポートする必要があります。
  
- SSL 経由の基本認証 (Exchange Online または Exchange オンプレミスを対象とするアプリケーション用)。
    
- SSL 経由の NTLM 認証 (Exchange オンプレミスをサポートするアプリケーション用)。
    
- OAuth 2.0 トークン認証 (信頼できるパートナー アプリケーション、および Lync Server 2013 と SharePoint Server 2013 との相互運用のため)。
    
## <a name="see-also"></a>関連項目


- [Exchange で Web サービスの使用を開始する](start-using-web-services-in-exchange.md)
    
- [EWS アプリケーションの種類](ews-application-types.md)
    
- [Exchange の EWS クライアントの設計の概要](ews-client-design-overview-for-exchange.md)
    

