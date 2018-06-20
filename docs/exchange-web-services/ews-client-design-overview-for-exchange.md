---
title: Exchange の EWS クライアントの設計の概要
manager: sethgros
ms.date: 3/11/2016
ms.audience: Developer
localization_priority: Normal
ms.assetid: b26f67aa-7c66-4d7d-98b3-746f26ab37f4
description: 'Exchange 用に EWS で開発する場合の設計の考慮事項について説明します。  '
ms.openlocfilehash: ea0e1ad3f8402d19a6163f3320a2a17f08f3ea2a
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "19758895"
---
# <a name="ews-client-design-overview-for-exchange"></a>Exchange の EWS クライアントの設計の概要

Exchange 用に EWS で開発する場合の設計の考慮事項について説明します。   
  
この資料では、Exchange Web サービス (EWS) アプリケーションの設計に関する概要情報を提供します。 EWS では、アプリケーションの右側の API と、使用する必要がある場合は、どのようなタイプのクライアントの実装かどうか確認するのには、この情報を使用できます。 この資料も用意されています Office 365、オンラインの Exchange および Exchange のバージョンを対象とするアプリケーションを設計するためのベスト プラクティス情報 Exchange 2007 では、基本、1 つのコードで、オンプレミスの Exchange を対象とするための重要な意思決定ポイントで始まるサーバーは Exchange Online を対象とするとします。
  
## <a name="is-ews-the-right-api-for-your-application"></a>EWS は作成しようとしているアプリケーションに適した API か
<a name="IsEWSRight"> </a>

アプリケーションの設計を開始する前にすることが重要 EWS が右の API であるかを考慮します。 Exchange Server または Exchange Online を開発している場合 EWS は、優先するクライアントのアクセス技術です。 EWS 上のバージョンの Exchange が Exchange 2007 以降のクライアント アクセスの開発が主されています。 Outlook に実装されているクライアント アクセスの新機能は、Exchange 2007 で導入された Office (OOF) と可用性の機能など、Exchange 2010 で導入されたメール ヒントとルームの取得機能、EWS を使用します。 これは、Exchange クライアントのアプリケーションを開発している内部および外部の両方のパートナーの EWS でコミット投資を表します。
  
EWS は、Exchange クライアント アプリケーションの主なクライアント アクセス API です。ただし、場合によっては、クライアント アプリケーションの開発用として他の Exchange API を検討できます。たとえば、Exchange ActiveSync には、EWS と比較して次の利点があります。
  
- XML データ構造がトークン化されたので、Exchange ActiveSync はよりコンパクトなプロトコルになります。  
- Exchange ActiveSync には、クライアントのアクセスを制御したり、その他の堅牢なエンタープライズ モバイル メッセージング ソリューションを提供したりするポリシー メカニズムが含まれています。
    
> [!NOTE]
> Exchange ActiveSync クライアントを開発するためにライセンスが必要です。 Exchange ActiveSync と EWS の違いについては、 [Exchange ActiveSync と Exchange Web サービス (EWS) との間の選択](http://msdn.microsoft.com/en-us/library/dn144954%28v=exchg.140%29.aspx)を参照してください。 
  
MAPI RPC over HTTP は、Exchange クライアントのアプリケーション用のもう 1 つのプログラミング オプションです。しかし、MAPI RPC over HTTP は、クライアントとサーバー間の通信に直感的なインターフェイスを提供しません。
  
Exchange 開発テクノロジに関する詳細については、 [EWS のマネージ API のエクスプ ローラー、EWS、および web サービスの Exchange](explore-the-ews-managed-api-ews-and-web-services-in-exchange.md)を参照してください。
  
## <a name="options-for-ews-client-development"></a>EWS クライアント開発のためのオプション
<a name="EWSClientOptions"> </a>

EWS を使用して Exchange を対象に開発を行うためのいくつかのオプションがあります。最良のオプションは、開発プラットフォーム、ツール、使用可能な実装、組織のアプリケーションの要件によって異なります。EWS のクライアント アプリケーションを構築するために利用可能な 4 つの主要なオプションは、次のとおりです。
  
- EWS マネージ API
- EWS Java API
- EWS の自動生成されたプロキシ
- カスタム EWS クライアント API
    
### <a name="ews-managed-api"></a>EWS Managed API

[EWS のマネージ API](http://aka.ms/ews-managed-api-readme)は、カスタム web サービス クライアントです。 .NET Framework アプリケーションの標準的なクライアント アクセス API です。 
  
以下は、EWS マネージ API を使用する利点の一部です。
  
- 直感的なオブジェクト モデルが用意されています。   
- WSDL ファイルとスキーマ ファイルでのサービス記述の複雑さを軽減します。   
- クライアント側のビジネス ロジックが含まれています。   
- Web 要求と応答や、オブジェクトのシリアル化と逆シリアル化を処理します。   
- Microsoft によるサポートがあります。
    
ただし、EWS のマネージ API は、完全なソリューションではないことに注意してください。 EWS のマネージ API では、いくつかの機能は実装されていません。 EWS のマネージ API では、EWS のすべての機能を実装しないが次の理由により、クライアント アプリケーションの開発に最適な選択肢があります。
  
- 開発に .NET Framework を使用できます。
- EWS オブジェクト モデルの大部分に加えて、自動検出を実装しています。
- [ExchangeService](http://msdn.microsoft.com/en-us/library/office/microsoft.exchange.webservices.data.exchangeservice%28v=exchg.80%29.aspx)クラスでの EWS を操作するためのクライアント側のビジネス ロジックを実装します。 
    
次の理由のいずれかにより、EWS マネージ API ではなく EWS の Web サービス API を使用することもできます。
  
- アプリケーションが .NET Framework を使用しない場合。 
- EWS のマネージ API のアセンブリを配布したくないです。 
- アプリケーションでは、EWS のマネージ API で実装されていない機能を使用します。
    
詳細については、 [EWS のマネージ API のクライアント アプリケーションを使い始める](get-started-with-ews-managed-api-client-applications.md)を参照してください。
  
> [!NOTE]
> EWS のマネージ API は、 [GitHub](http://aka.ms/ews-managed-api-github)のオープン ソース プロジェクトとしてされています。 オープン ソース ライブラリを使用することができます。 
> - バグ修正と API の機能強化に貢献します。 
> - 公式のリリースで利用可能になる前に、修正プログラムや拡張機能を取得できます。
> - API の最も包括的かつ最新の実装にアクセスして、参照として使用するか、新しいプラットフォームで新しいライブラリを作成します。 
> 
> GitHub を使用してあなたの[投稿](https://github.com/OfficeDev/ews-managed-api/blob/master/CONTRIBUTING.md)をお待ちします。 
  
### <a name="ews-java-api"></a>EWS Java API

EWS の Java API は、更新およびコミュニティによって拡張できる[GitHub](https://github.com/OfficeDev/ews-java-api)のオープン ソース プロジェクトです。 [EWS のマネージ API](http://msdn.microsoft.com/en-us/library/office/jj220535%28v=exchg.80%29.aspx)のような stylistically と、EWS の SOAP 要求と応答を使用して、ネットワーク経由で。 すべての[EWS の SOAP 操作](http://msdn.microsoft.com/library/cf6fd871-9a65-4f34-8557-c8c71dd7ce09%28Office.15%29.aspx)をアクセスできない場合は、オープン ソース プロジェクトの[最新の作成](http://blogs.office.com/2014/08/28/open-sourcing-exchange-web-services-ews-java-api/)時に、EWS の Java API を使用して、私たちはこのギャップを埋めるためのコミュニティを模索しています。 マイクロソフト サポート、適切なサポートの契約には質問に対応 EWS の SOAP プロトコルがない、EWS Java API 自体に関連する注意してください。 EWS の Java API は、 [GitHub](https://github.com/OfficeDev/ews-java-api)のダウンロードとコミュニティの貢献度を使用できます。
  
### <a name="ews-autogenerated-proxies"></a>EWS の自動生成されたプロキシ

自動生成されたクライアント API は、EWS の WSDL および XML スキーマ定義から生成されます。多くの言語でクライアント オブジェクト モデルのジェネレーターが用意されています。一般に、自動生成されたオブジェクト モデルは、オブジェクトのシリアル化および逆シリアル化を管理します。これにビジネス ロジックは含まれておらず、自動生成プロセスによって成果物が作成される結果、直感的には使用しにくいオブジェクト モデルになることが少なくありません。Exchange のサポートはクライアントによって送受信される XML を対象としますが、オブジェクト モデルは対象となりません。
  
### <a name="custom-ews-client-api"></a>カスタム EWS クライアント API

EWS 機能の小さなセットを使用する一部のアプリケーション用に、Exchange と通信するためのカスタム クライアント API を作成できます。これにより、使用するシステム リソースが少なくなります。これは、.NET Micro Framework を実行するクライアントなど、メモリに制約のあるデバイス上で実行されるクライアントに役立ちます。
  
## <a name="ews-client-features"></a>EWS のクライアント機能
<a name="EWSFeatures"> </a>

どの開発オプションを選ぶにせよ、EWS 機能をクライアントでどのように実装するかをご検討ください。機能が使用可能かどうかは、アプリケーションが対象とする EWS のスキーマのバージョン次第です。EWS のスキーマは後方互換性と前方互換性を持つため、Exchange Server 2007 SP1 などの以前のバージョンのスキーマを対象とするアプリケーションを作成する場合、アプリケーションは Exchange Server 2013 SP1 のサービスや Exchange Online など、後のバージョンのスキーマでも動作します。  
  
機能および機能の更新はスキーマによって決定されるため、クライアント アプリケーションに実装する EWS 機能を対象としているもののうち、最も古い共通のコード ベースを使用することをお勧めします。多くのアプリケーションは Exchange2007_SP1 バージョンを対象にできます。なぜなら、Exchange 2007 SP1 のスキーマには、Exchange のストアのアイテムやフォルダーを操作するための Exchange のほとんどすべての主要機能が含まれているためです。EWS のスキーマのバージョンごとに、コードの分岐を維持することをお勧めします。現在利用可能なスキーマのバージョンを次に示します。  
  
```XML
  <xs:simpleType name="ExchangeVersionType">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Exchange2007" />
      <xs:enumeration value="Exchange2007_SP1" />
      <xs:enumeration value="Exchange2010" />
      <xs:enumeration value="Exchange2010_SP1" />
      <xs:enumeration value="Exchange2010_SP2" />
      <xs:enumeration value="Exchange2013" />
      <xs:enumeration value="Exchange2013_SP1" />
    </xs:restriction>
  </xs:simpleType>
```

**ExchangeVersionType**単純型では、スキーマのバージョンが維持されます。 
  
EWS スキーマの各バージョンで利用可能な機能の詳細については、 [Exchange での EWS のスキーマ バージョン](ews-schema-versions-in-exchange.md)を参照してください。
  
## <a name="in-this-section"></a>このセクションの内容
<a name="bk_inthissection"> </a>

- [Exchange および EWS のマネージ API の web サービス API 機能の可用性](web-service-api-feature-availability-in-exchange-and-the-ews-managed-api.md)
    
- [Exchange のスキーマ バージョンの EWS](ews-schema-versions-in-exchange.md)
    
- [Exchange 内の構成オプション](configuration-options-for-ews-in-exchange.md)
    
- [オンラインの Exchange および Exchange、オンプレミスのクライアントがプログラミングを比較します。](comparing-exchange-online-and-exchange-on-premises-client-programming.md)
    
- [EWS の交換で調整](ews-throttling-in-exchange.md)
    
- [EWS のマネージ API の再配布の条件](redistribution-requirements-for-the-ews-managed-api.md)
    
- [EWS および他の Exchange クライアントの要求を実装](instrumenting-client-requests-for-ews-and-rest-in-exchange.md)
    
## <a name="see-also"></a>関連項目
 
- [Exchange で Web サービスの使用を開始する](start-using-web-services-in-exchange.md)
- [Exchange の Web サービス クライアントを開発する](develop-web-service-clients-for-exchange.md) 
- [EWS アプリケーションの種類](ews-application-types.md)
    
