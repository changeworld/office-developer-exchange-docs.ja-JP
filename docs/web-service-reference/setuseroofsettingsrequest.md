---
title: SetUserOofSettingsRequest
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
api_name:
- SetUserOofSettingsRequest
api_type:
- schema
ms.assetid: 628acf0b-3ebc-42f1-8ce2-7a02b4c8141f
description: SetUserOofSettingsRequest 要素には、メールボックスのユーザーの Office (OOF) の設定を設定するための引数が含まれています。
ms.openlocfilehash: ed54bb1d066da7b15605fb81931a6ef75dfc61bf
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19833474"
---
# <a name="setuseroofsettingsrequest"></a>SetUserOofSettingsRequest

**SetUserOofSettingsRequest**要素には、メールボックスのユーザーの Office (OOF) の設定を設定するための引数が含まれています。 
  
```xml
<SetUserOofSettingsRequest>
   <Mailbox>...</Mailbox>
   <UserOofSettings>...</UserOofSettings>
<SetUserOofSettingsRequest>
```

 **SetUserOofSettingsRequest**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

|**要素**|**説明**|
|:-----|:-----|
|[メールボックス (可用性)](mailbox-availability.md) <br/> |SetUserOofSettings または GetUserOofSettings の要求をメールボックスのユーザーを識別します。  <br/> |
|[UserOofSettings](useroofsettings.md) <br/> |不在の設定を指定します。  <br/> |
   
### <a name="parent-elements"></a>親要素

なし。
  
## <a name="remarks"></a>備考

MicrosoftExchange Server 2007 がインストールされているクライアント アクセス サーバーの役割を実行しているコンピューターの EWS 仮想ディレクトリには、この要素を記述するスキーマがあります。
  
## <a name="example"></a>例

SetUserOofSettings 要求の次の例では、10 日間、不在時の設定を設定します。
  
```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <SetUserOofSettingsRequest xmlns="http://schemas.microsoft.com/exchange/services/2006/messages">
      <Mailbox xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
        <Name>David Alexander</Name>
        <Address>someone@example.com</Address>
        <RoutingType>SMTP</RoutingType>
      </Mailbox>
      <UserOofSettings xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
        <OofState>Enabled</OofState>
        <ExternalAudience>All</ExternalAudience>
        <Duration>
          <StartTime>2005-10-05T00:00:00</StartTime>
          <EndTime>2005-10-25T00:00:00</EndTime>
        </Duration>
        <InternalReply>
          <Message>I am out of office.  This is my internal reply.</Message>
        </InternalReply>
        <ExternalReply>
          <Message>I am out of office. This is my external reply.</Message>
        </ExternalReply>
      </UserOofSettings>
    </SetUserOofSettingsRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/messages  <br/> |
|スキーマ名  <br/> |メッセージ スキーマ  <br/> |
|検証ファイル  <br/> |Messages.xsd  <br/> |
|空に設定可能  <br/> |False  <br/> |
   
## <a name="see-also"></a>関連項目



[SetUserOofSettings 操作](setuseroofsettings-operation.md)

