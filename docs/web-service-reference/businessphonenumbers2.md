---
title: BusinessPhoneNumbers2
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
ms.assetid: f335ea74-9b5b-4224-9475-40ef33fe76bd
description: BusinessPhoneNumbers2 要素は、BusinessPhoneNumber2 要素の配列と関連付けられているペルソナにそのソースの帰属の識別子を指定します。
ms.openlocfilehash: 8a03e102223e5542d6a672c4f47305cef84b850b
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19759582"
---
# <a name="businessphonenumbers2"></a>BusinessPhoneNumbers2

**BusinessPhoneNumbers2**要素は、 **BusinessPhoneNumber2**要素の配列と関連付けられているペルソナにそのソースの帰属の識別子を指定します。 
  
```XML
<BusinessPhoneNumbers2>
    <Value></Value>
    <Attributions></Attributions>
</BusinessPhoneNumbers2>
```

 **ArrayOfPhoneNumberAttributedValuesType**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

|**要素**|**説明**|
|:-----|:-----|
|[値 (PersonaPhoneNumberType)](value-personaphonenumbertype.md) <br/> |帰属のセットが関連付けられているし、電話の数と種類の情報を指定します。  <br/> |
|[帰属 (ArrayOfValueAttributionsType)](attributions-arrayofvalueattributionstype.md) <br/> |帰属、関連付けられている**値**の要素の配列を指定します。  <br/> |
   
### <a name="parent-elements"></a>親要素

|**要素**|**説明**|
|:-----|:-----|
|[ペルソナ](persona.md) <br/> |**GetPersona**の要求によって返されるペルソナ データのセットを指定します。  <br/> |
   
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

