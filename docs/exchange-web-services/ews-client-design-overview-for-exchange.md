---
title: Exchange の EWS クライアントの設計の概要
manager: sethgros
ms.date: 3/11/2016
ms.audience: Developer
localization_priority: Normal
ms.assetid: b26f67aa-7c66-4d7d-98b3-746f26ab37f4
description: Exchange 用に EWS で開発する場合の設計の考慮事項について説明します。
ms.openlocfilehash: 10e1c78bdd93dc5aede6e3f9337aa70b0214b770
ms.sourcegitcommit: 9061fcf40c218ebe88911783f357b7df278846db
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2018
ms.locfileid: "21353904"
---
# <a name="ews-client-design-overview-for-exchange"></a>Exchange の EWS クライアントの設計の概要

Exchange 用に EWS で開発する場合の設計の考慮事項について説明します。 
  
この記事では、Exchange Web サービス (EWS) アプリケーションの設計に関する概要情報を提供します。 この情報を使用して、EWS がアプリケーションに適した API であるかどうか、そして適している場合、どのような種類のクライアント実装を使用すべきかを判断することができます。 また、この記事では、1 つのコード ベースで Office 365、Exchange Online、Exchange 2007 以降のバージョンの Exchange をターゲットにできるアプリケーションの設計に関するベスト プラクティス情報や、オンプレミスの Exchange サーバーと Exchange Online のどちらをターゲットにすべきかに関する重要な判断ポイントも提供しています。
  
## <a name="is-ews-the-right-api-for-your-application"></a>EWS は作成しようとしているアプリケーションに適した API か
<a name="IsEWSRight"> </a>

アプリケーションの設計を開始する前に、EWS が用途に適した API であるかどうかを考慮することが重要です。 Exchange Server または Exchange Online を対象に開発している場合、EWS は優先すべきクライアント アクセス技術です。 Exchange 2007 以降のバージョンの Exchange 用のクライアント アクセスの開発では、主に EWS に焦点が当てられてきました。 Outlook に実装されているクライアント アクセスの新機能は EWS を使用しています。これには、Exchange 2007 で導入された不在 (OOF) および空き時間の機能や、Exchange 2010 で導入されたメール ヒントと GetRooms 機能が含まれます。 これは、Exchange クライアント アプリケーションを開発する社内および社外のパートナーの両方に対して、EWS に集中的に投資していることを示すものです。
  
EWS は、Exchange クライアント アプリケーションの主なクライアント アクセス API です。ただし、場合によっては、クライアント アプリケーションの開発用として他の Exchange API を検討できます。たとえば、Exchange ActiveSync には、EWS と比較して次の利点があります。
  
- XML データ構造がトークン化されたので、Exchange ActiveSync はよりコンパクトなプロトコルになります。  
- Exchange ActiveSync には、クライアントのアクセスを制御したり、その他の堅牢なエンタープライズ モバイル メッセージング ソリューションを提供したりするポリシー メカニズムが含まれています。
    
> [!NOTE]
> Exchange ActiveSync クライアントを開発するには、ライセンスが必要です。 Exchange ActiveSync と EWS の違いについては、[「Exchange ActiveSync と EWS のどちらかを選ぶ」](http://msdn.microsoft.com/ja-JP/library/dn144954%28v=exchg.140%29.aspx)を参照してください。 
  
MAPI RPC over HTTP は、Exchange クライアントのアプリケーション用のもう 1 つのプログラミング オプションです。しかし、MAPI RPC over HTTP は、クライアントとサーバー間の通信に直感的なインターフェイスを提供しません。
  
Exchange 開発技術の詳細については、[「Exchange の EWS Managed API、EWS、および Web サービスについて学ぶ」](explore-the-ews-managed-api-ews-and-web-services-in-exchange.md)を参照してください。
  
## <a name="options-for-ews-client-development"></a>EWS クライアント開発のためのオプション
<a name="EWSClientOptions"> </a>

EWS を使用して Exchange を対象に開発を行うためのいくつかのオプションがあります。最良のオプションは、開発プラットフォーム、ツール、使用可能な実装、組織のアプリケーションの要件によって異なります。EWS のクライアント アプリケーションを構築するために利用可能な 4 つの主要なオプションは、次のとおりです。
  
- EWS マネージ API
- EWS Java API
- EWS の自動生成されたプロキシ
- カスタム EWS クライアント API
    
### <a name="ews-managed-api"></a>EWS マネージ AP

[EWS マネージ API](http://aka.ms/ews-managed-api-readme) は、カスタム Web サービス クライアントです。 これは、.NET Framework アプリケーションのための標準的なクライアント アクセス API です。 
  
以下は、EWS マネージ API を使用する利点の一部です。
  
- 直感的なオブジェクト モデルが用意されています。   
- WSDL ファイルとスキーマ ファイルでのサービス記述の複雑さを軽減します。   
- クライアント側のビジネス ロジックが含まれています。   
- Web 要求と応答や、オブジェクトのシリアル化と逆シリアル化を処理します。   
- Microsoft によるサポートがあります。
    
ただし、EWS マネージ API は、完全なソリューションではないことにご注意ください。 一部の機能は、EWS マネージ API では実装されていません。 EWS マネージ API は EWS のすべての機能を実装してはいませんが、次の理由により、クライアント アプリケーション開発の最良の選択肢になり得ます。
  
- 開発に .NET Framework を使用できます。
- EWS オブジェクト モデルの大部分に加えて、自動検出を実装しています。
- EWS と連携するためのクライアント側のビジネス ロジックが [ExchangeService](http://msdn.microsoft.com/ja-JP/library/office/microsoft.exchange.webservices.data.exchangeservice%28v=exchg.80%29.aspx) クラスで実装されています。 
    
次の理由のいずれかにより、EWS マネージ API ではなく EWS の Web サービス API を使用することもできます。
  
- アプリケーションが .NET Framework を使用しない場合。 
- EWS マネージ API のアセンブリを配布することを望まない場合。 
- EWS マネージ API で実装されていない機能をアプリケーションで使用する場合。
    
詳細については、「[EWS マネージ API クライアント アプリケーションの概要](get-started-with-ews-managed-api-client-applications.md)」をご覧ください。
  
> [!NOTE]
> EWS マネージ API は、[GitHub](http://aka.ms/ews-managed-api-github) でオープンソース プロジェクトとして利用可能になりました。 オープン ソース ライブラリを使用して、以下のことができます。 
> - バグ修正と API の機能強化に貢献します。 
> - 公式のリリースで利用可能になる前に、修正プログラムや拡張機能を取得できます。
> - API の最も包括的かつ最新の実装にアクセスして、参照として使用するか、新しいプラットフォームで新しいライブラリを作成します。
> 
> GitHub を通した皆様の[貢献](https://github.com/OfficeDev/ews-managed-api/blob/master/CONTRIBUTING.md)を歓迎いたします。 
  
### <a name="ews-java-api"></a>EWS Java API

EWS Java API は、コミュニティが更新および拡張できる [GitHub](https://github.com/OfficeDev/ews-java-api) のオープン ソース プロジェクトです。 形式的には [EWS マネージ API](http://msdn.microsoft.com/ja-JP/library/office/jj220535%28v=exchg.80%29.aspx) と似ており、EWS SOAP 要求と応答をネットワーク経由で使用します。 EWS Java API を使用してすべての [EWS SOAP 操作](http://msdn.microsoft.com/library/cf6fd871-9a65-4f34-8557-c8c71dd7ce09%28Office.15%29.aspx)にアクセスできるわけではありませんが、[最近作成された](http://blogs.office.com/2014/08/28/open-sourcing-exchange-web-services-ews-java-api/)オープン ソース プロジェクトにより、コミュニティがこのギャップを埋めることが期待されます。 Microsoft サポートは、適切なサポート契約がある場合に、EWS SOAP プロトコルに関連する質問には対応しますが、EWS Java API 自体に関連する質問には対応しないことにご注意ください。 [GitHub](https://github.com/OfficeDev/ews-java-api) で EWS Java API をダウンロードしたり、そのコミュニティに貢献したりすることができます。
  
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

スキーマのバージョンは **ExchangeVersionType** の単純型で保持されます。 
  
EWS スキーマの各バージョンで利用可能な機能については、「[Exchange の EWS スキーマのバージョン](ews-schema-versions-in-exchange.md)」をご覧ください。
  
## <a name="in-this-section"></a>このセクションの内容
<a name="bk_inthissection"> </a>

- [Exchange および EWS Managed API の Web サービス API 機能の可用性](web-service-api-feature-availability-in-exchange-and-the-ews-managed-api.md)   
- [Exchange の EWS スキーマのバージョン](ews-schema-versions-in-exchange.md)  
- [Exchange 内の EWS の構成オプション](configuration-options-for-ews-in-exchange.md)  
- [Exchange Online と Exchange オンプレミス クライアント プログラミングの比較](comparing-exchange-online-and-exchange-on-premises-client-programming.md)   
- [Exchange での EWS 調整](ews-throttling-in-exchange.md)  
- [EWS マネージ API の再配布の要件](redistribution-requirements-for-the-ews-managed-api.md)  
- [Exchange で EWS と REST のクライアントの要求をインストルメント化する](instrumenting-client-requests-for-ews-and-rest-in-exchange.md)
    
## <a name="see-also"></a>関連項目
 
- [Exchange で Web サービスの使用を開始する](start-using-web-services-in-exchange.md)
- [Exchange の Web サービス クライアントを開発する](develop-web-service-clients-for-exchange.md) 
- [EWS アプリケーションの種類](ews-application-types.md)
    

