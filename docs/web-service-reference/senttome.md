---
title: SentToMe
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
api_name:
- SentToMe
api_type:
- schema
ms.assetid: f18aecd1-ad33-41c3-b275-4ca648ce1da0
description: SentToMe 要素は、メールボックスの所有者が ToRecipients プロパティを適用する場合の条件または例外の順序で受信したメッセージであるかどうかを示します。
ms.openlocfilehash: 7f4d24e985256b68d2c5f124f4130f03f35f26e5
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19833365"
---
# <a name="senttome"></a>SentToMe

**SentToMe**要素は、メールボックスの所有者が**ToRecipients**プロパティを適用する場合の条件または例外の順序で受信したメッセージであるかどうかを示します。 
  
```XML
<SentToMe>true | false</SentToMe>
```

 **ブール型 (Boolean)**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

なし。
  
### <a name="parent-elements"></a>親要素

|**要素**|**説明**|
|:-----|:-----|
|[条件](conditions.md) <br/> |条件を表しますが、満たされるとときに、ルールのルールの処理をトリガーします。  <br/> |
|[Exceptions](exceptions.md) <br/> |受信トレイ ルールの使用可能なルールの例外条件をすべてを表します。  <br/> |
   
## <a name="text-value"></a>テキスト値

テキスト値が**true**のでは、メールボックスの所有者を適用する場合の条件または例外の順序で受信メッセージの**ToRecipients**プロパティにする必要があることを示します。 **False**の値を示します**ToRecipients**プロパティを適用する場合の条件または例外の順序で受信メッセージのでは、メールボックスの所有者でなければなりません。 
  
## <a name="remarks"></a>備考

この要素を記述するスキーマは、Exchange Web サービスをホストする IIS 仮想ディレクトリに置かれています。
  
## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/messages  <br/> |
|スキーマ名  <br/> |メッセージ スキーマ  <br/> |
|検証ファイル  <br/> |Messages.xsd  <br/> |
|空に設定可能  <br/> |True  <br/> |
   
## <a name="see-also"></a>関連項目



- [Exchange での EWS の XML 要素](ews-xml-elements-in-exchange.md)

