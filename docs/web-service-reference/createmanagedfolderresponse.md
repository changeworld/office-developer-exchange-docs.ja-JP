---
title: CreateManagedFolderResponse
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
api_name:
- CreateManagedFolderResponse
api_type:
- schema
ms.assetid: 99062401-d356-4ce7-a5d0-c8c7aab99912
description: CreateManagedFolderResponse 要素は、CreateManagedFolder 要求への応答を定義します。
ms.openlocfilehash: fc486a197b7b0a0ed7310dda88d4bf8735f99876
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19759852"
---
# <a name="createmanagedfolderresponse"></a>CreateManagedFolderResponse

**CreateManagedFolderResponse**要素は、CreateManagedFolder 要求への応答を定義します。 
  
```xml
<CreateManagedFolderResponse>
   <ResponseMessages/>
</CreateManagedFolderResponse>
```

 **CreateManagedFolderResponseType**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

|**要素**|**説明**|
|:-----|:-----|
|[ResponseMessages](responsemessages.md) <br/> |Exchange Web サービス要求に対する応答メッセージが含まれています。  <br/> |
   
### <a name="parent-elements"></a>親要素

なし。
  
## <a name="remarks"></a>備考

MicrosoftExchange Server 2007 がインストールされているクライアント アクセス サーバーの役割を実行しているコンピューターの EWS 仮想ディレクトリには、この要素を記述するスキーマがあります。
  
## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/messages  <br/> |
|スキーマ名  <br/> |メッセージ スキーマ  <br/> |
|検証ファイル  <br/> |Messages.xsd  <br/> |
|空にすることができます。  <br/> |False  <br/> |
   
## <a name="see-also"></a>関連項目



[CreateManagedFolder 操作](createmanagedfolder-operation.md)
  
[CreateManagedFolder](createmanagedfolder.md)


- [Exchange での EWS の XML 要素](ews-xml-elements-in-exchange.md)

