---
title: SharedFolderId
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
api_name:
- SharedFolderId
api_type:
- schema
ms.assetid: 21181ba3-9626-4284-9717-0b1c16948e8f
description: SharedFolderId 要素は、GetSharingFolder 操作の要求で返されます、ローカル フォルダーの識別子を共有フォルダーの識別子を表します。
ms.openlocfilehash: 6d4e541ef3cae89e413efa8cc5f1beaf651dc4dd
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19833477"
---
# <a name="sharedfolderid"></a>SharedFolderId

**SharedFolderId**要素は、 [GetSharingFolder 操作](getsharingfolder-operation.md)の要求で返されます、ローカル フォルダーの識別子を共有フォルダーの識別子を表します。 
  
```xml
<SharedFolderId/>
```

 **NonEmptyStringType**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

なし。
  
### <a name="parent-elements"></a>親要素

|**要素**|**説明**|
|:-----|:-----|
|[GetSharingFolder](getsharingfolder.md) <br/> |指定した共有フォルダーのローカル フォルダーの識別子を取得する要求を定義します。  <br/> |
   
## <a name="text-value"></a>テキスト値

テキスト値は、 [GetSharingFolder 操作](getsharingfolder-operation.md)の要求で返されます、ローカル フォルダーの識別子を共有フォルダーの識別子を表す文字列です。 
  
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



[GetSharingFolder 操作](getsharingfolder-operation.md)


- [Exchange での EWS の XML 要素](ews-xml-elements-in-exchange.md)

