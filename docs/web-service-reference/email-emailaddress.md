---
title: 電子メール (EmailAddress)
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
ms.assetid: 5c40a6b6-e2d1-44ba-b439-5720490cbd43
description: Email 要素は、会議に参加者を識別します。
ms.openlocfilehash: 8b95aa066d545a579ec3c14627d99dd0e326477e
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19760209"
---
# <a name="email-emailaddress"></a>電子メール (EmailAddress)

**Email**要素は、会議に参加者を識別します。 
  
```XML
<Email></Email>
```

 **EmailAddress**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

なし。
  
### <a name="parent-elements"></a>親要素

[MailboxData](mailboxdata.md)
  
## <a name="text-value"></a>テキスト値

Email 要素のテキスト値は、 **GetUserAvailability**操作の応答で返される参加者を識別します。 
  
## <a name="remarks"></a>備考

この要素は Exchange Server 2013 で導入されました。
  
この要素を記述するスキーマは、Exchange Web サービスをホストする IIS 仮想ディレクトリに置かれています。
  
## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/types  <br/> |
|スキーマ名  <br/> |タイプのスキーマ  <br/> |
|検証ファイル  <br/> |Types.xsd  <br/> |
|空にすることができます。  <br/> ||
   

