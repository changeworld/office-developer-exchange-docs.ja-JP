---
title: エラー コード (int)
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
ms.assetid: 65537d96-edf9-41ee-9ad5-91ffe37e2269
description: エラー コード要素は、メールボックスに対して実行が失敗した検索のエラー コードを指定します。
ms.openlocfilehash: ed8a7771376f921303ea093f4be727c4146faa76
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19760319"
---
# <a name="errorcode-int"></a>エラー コード (int)

**エラー コード**要素は、メールボックスに対して実行が失敗した検索のエラー コードを指定します。 
  
```XML
<ErrorCode></ErrorCode>
```

 **int**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

なし。
  
### <a name="parent-elements"></a>親要素

|**要素**|**説明**|
|:-----|:-----|
|[FailedMailbox](failedmailbox.md) <br/> |メールボックスの保留状態を指定します。  <br/> |
   
## <a name="text-value"></a>テキスト値

**エラー コード**要素のテキスト値は、メールボックスに対して実行が失敗した検索で返されるエラー コードです。 
  
## <a name="remarks"></a>備考

この要素は Exchange Server 2013 で導入されました。
  
この要素を記述するスキーマは、Exchange Web サービスをホストする IIS 仮想ディレクトリに置かれています。
  
## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/types  <br/> |
|スキーマ名  <br/> |型のスキーマ  <br/> |
|検証ファイル  <br/> |types.xsd  <br/> |
|空にすることができます。  <br/> ||
   
## <a name="see-also"></a>関連項目



- [Exchange での EWS の XML 要素](ews-xml-elements-in-exchange.md)

