---
title: AltitudeAccuracy
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
ms.assetid: aadc1f90-e9ab-4411-b51f-2d43e5e22f2a
description: AltitudeAccuracy 要素は、住所のプロパティの高度の精度を指定します。
ms.openlocfilehash: 09ec86e4913327feb47067f5e5de7a60efc47bc5
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19759313"
---
# <a name="altitudeaccuracy"></a>AltitudeAccuracy

**AltitudeAccuracy**要素は、住所のプロパティの高度の精度を指定します。 
  
```XML
<AltitudeAccuracy></AltitudeAccuracy>
```

 **xs:double**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

なし。
  
### <a name="parent-elements"></a>親要素

|**要素**|**説明**|
|:-----|:-----|
|[住所 (PersonaPostalAddressType)](postaladdress-personapostaladdresstype.md) <br/> |場所の郵便の宛先を指定します。  <br/> |
   
## <a name="text-value"></a>テキスト値

**AltitudeAccuracy**要素のテキスト値は、住所の高度のプロパティの正確さの見積もりです。 
  
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

