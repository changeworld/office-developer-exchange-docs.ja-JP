---
title: 送信者
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
ms.assetid: 69d88bb1-397c-4fb8-bd2b-21cccc5bb35d
description: 送信者要素では、簡易メール転送プロトコル (SMTP) アドレスの配列を指定します。
ms.openlocfilehash: 0794b042c00183d56b2fb2aefe8587e0fdf1344d
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19833329"
---
# <a name="senders"></a>送信者

**送信者**要素では、簡易メール転送プロトコル (SMTP) アドレスの配列を指定します。 
  
```XML
<Senders>
   <SmtpAddress/>
</Senders>
```

 **ArrayOfSmtpAddressType**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

[SmtpAddress](smtpaddress.md)
  
### <a name="parent-elements"></a>親要素

[FindMailboxStatisticsByKeywords](findmailboxstatisticsbykeywords.md)
  
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
   

