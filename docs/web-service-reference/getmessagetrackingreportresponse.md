---
title: GetMessageTrackingReportResponse
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
api_name:
- GetMessageTrackingReportResponse
api_type:
- schema
ms.assetid: 41177894-2008-44a6-86f8-bc34c0a48e36
description: GetMessageTrackingReportResponse 要素には、GetMessageTrackingReport 操作に対する応答が含まれています。
ms.openlocfilehash: bdb8b97e57f92a32cbdc498d09297920366b58bd
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19760794"
---
# <a name="getmessagetrackingreportresponse"></a>GetMessageTrackingReportResponse

**GetMessageTrackingReportResponse**要素には、 [GetMessageTrackingReport 操作](getmessagetrackingreport-operation.md)の応答が含まれています。
  
```xml
<GetMessageTrackingReportResponse ResponseClass="">
   <MessageText/>
   <ResponseCode/>
   <DescriptiveLinkKey/>
   <MessageXml/>
   <MessageTrackingReport/>
   <Diagnostics/>
   <Errors/>
   <Properties/>
</GetMessageTrackingReportResponse>
```

 **GetMessageTrackingReportResponseMessageType**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

|**属性**|**説明**|
|:-----|:-----|
|**ResponseClass** <br/> | 応答のステータスについて説明します。 <br/><br/>次の値は、この属性の有効です。  <br/><br/>-成功  <br/>-警告  <br/>-エラー  <br/> |
   
#### <a name="responseclass-attribute-values"></a>ResponseClass 属性の値

|**値**|**説明**|
|:-----|:-----|
|**Success** <br/> |満了する要求をについて説明します。  <br/> |
|**Warning** <br/> | 処理されなかった要求をについて説明します。 警告は、要求内のアイテムを処理し、それ以降の項目を処理できませんでした、エラーが発生した場合に返される場合があります。<br/><br/> 警告の送信元の例を次に示します。  <br/><br/>-Exchange ストアは、バッチの実行中にオフラインです。  <br/>-Active Directory ドメイン機能 (AD DS) は、オフラインです。  <br/>-メールボックスは移動されました。  <br/>-メッセージ データベース (MDB) は、オフラインです。  <br/>-パスワードの有効期限が切れています。  <br/>クォータを超えています。  <br/> |
|**Error** <br/> | 満たせない要求をについて説明します。 <br/><br/>次に、エラーのソースの例を示します。  <br/>  無効な属性または要素  <br/><br/>属性または要素の範囲を超えています。  <br/>-不明なタグ  <br/>属性または要素のコンテキストでは有効ではないです。  <br/>-任意のクライアントから不正なアクセス試行  <br/>-クライアント側の有効な呼び出しへの応答でサーバー側エラー  <br/><br/>  エラーに関する情報は、 [ResponseCode](responsecode.md)および[メッセージ テキスト](messagetext.md)の要素を参照しています。  <br/> |
   
### <a name="child-elements"></a>子要素

|**要素**|**説明**|
|:-----|:-----|
|[MessageText](messagetext.md) <br/> |応答のステータスの説明を提供します。  <br/> |
|[ResponseCode](responsecode.md) <br/> |要求で発生した特定のエラーを識別するエラー コードを提供します。  <br/> |
|[DescriptiveLinkKey](descriptivelinkkey.md) <br/> |現在使用されていない、将来使用するために予約されています。 この要素には、0 の値が含まれています。  <br/> |
|[MessageXml](messagexml.md) <br/> |追加のエラー応答情報を提供します。  <br/> |
|[MessageTrackingReport](messagetrackingreport.md) <br/> |[GetMessageTrackingReport 操作](getmessagetrackingreport-operation.md)で返される 1 つのメッセージが含まれています。  <br/> |
|[診断](diagnostics.md) <br/> |データ センターに報告するために使用されるタイミングとパフォーマンスの情報を提供します。  <br/> |
|[エラー](errors-ex15websvcsotherref.md) <br/> |Web サービスから返されるエラーを格納するプロパティ バッグに含まれています。  <br/> |
|[プロパティ (ArrayOfTrackingPropertiesType)](properties-arrayoftrackingpropertiestype.md) <br/> |1 つまたは複数の追跡のプロパティの一覧が含まれています。  <br/> |
   
### <a name="parent-elements"></a>親要素

なし。
  
## <a name="text-value"></a>テキスト値

なし。
  
## <a name="remarks"></a>備考

この要素を記述するスキーマは、Exchange Web サービスをホストする IIS 仮想ディレクトリに置かれています。
  
## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/messages  <br/> |
|スキーマ名  <br/> |メッセージ スキーマ  <br/> |
|検証ファイル  <br/> |Messages.xsd  <br/> |
|空に設定可能  <br/> |False  <br/> |
   
## <a name="see-also"></a>関連項目

- [GetMessageTrackingReport 操作](getmessagetrackingreport-operation.md)
- [Exchange での EWS の XML 要素](ews-xml-elements-in-exchange.md)

