---
title: メールボックス (PreviewItemMailboxType)
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
ms.assetid: e898d737-b6e4-4403-9c2c-aec52a48a83d
description: メールボックスの要素には、メールボックス id およびユーザーのプライマリ簡易メール転送プロトコル (SMTP) アドレスが含まれています。
ms.openlocfilehash: 1b6669928015bc880806479d294a4063034a559f
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "19832255"
---
# <a name="mailbox-previewitemmailboxtype"></a>メールボックス (PreviewItemMailboxType)

**メールボックス**の要素には、メールボックス id およびユーザーのプライマリ簡易メール転送プロトコル (SMTP) アドレスが含まれています。 
  
```XML
<Mailbox>
   <MailboxId/>
   <PrimarySmtpAddress/>
</Mailbox>
```

**PreviewItemMailboxType**

## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

[MailboxId](mailboxid.md) | [PrimarySmtpAddress (文字列)](primarysmtpaddress-string.md)
  
### <a name="parent-elements"></a>親要素

[SearchPreviewItem](searchpreviewitem.md)
  
## <a name="remarks"></a>備考

この要素は Exchange Server 2013 で導入されました。
  
この要素を記述するスキーマは、Exchange Web サービスをホストする IIS 仮想ディレクトリに置かれています。
  
## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/types  <br/> |
|スキーマ名  <br/> |タイプのスキーマ  <br/> |
|検証ファイル  <br/> |Types.xsd  <br/> |
|空にすることができます。  <br/> |false  <br/> |
   
