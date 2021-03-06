---
title: LastOccurrence
manager: sethgros
ms.date: 09/17/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
api_name:
- LastOccurrence
api_type:
- schema
ms.assetid: c9ef0fcb-4265-4e60-9986-fff0f211d00b
description: LastOccurrence 要素は、定期的な予定表アイテムが最後に見つかった位置を表します。
ms.openlocfilehash: 2c8fdfc0005e86c9dda84a48ae1d3692b5134ca8
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19832209"
---
# <a name="lastoccurrence"></a>LastOccurrence

**LastOccurrence**要素は、定期的な予定表アイテムが最後に見つかった位置を表します。 
  
```xml
<LastOccurrence>
   <ItemId/>
   <Start/>
   <End/>
   <OriginalStart/>
</LastOccurrence>
```

 **OccurrenceInfoType**
## <a name="attributes-and-elements"></a>属性および要素

以下のセクションで、属性、子要素、親要素について説明します。
  
### <a name="attributes"></a>属性

なし。
  
### <a name="child-elements"></a>子要素

|**要素**|**説明**|
|:-----|:-----|
|[ItemId](itemid.md) <br/> |定期的な予定表アイテムが最後に見つかった位置の一意の識別子と変更キーが含まれています。  <br/> |
|[Start](start.md) <br/> |定期的な予定表アイテムが最後に見つかった位置の開始時刻を表します。  <br/> |
|[終わり](end-ex15websvcsotherref.md) <br/> |最後に出現する定期的な予定表アイテムの終了時刻を表します。  <br/> |
|[OriginalStart](originalstart.md) <br/> |定期的な予定表アイテムが最後に見つかった位置の元の開始時刻を表します。  <br/> |
   
### <a name="parent-elements"></a>親要素

|**要素**|**説明**|
|:-----|:-----|
|[カレンダー項目](calendaritem.md) <br/> |Exchange 予定表アイテムを表します。  <br/> |
|[MeetingRequest](meetingrequest.md) <br/> |Exchange ストア内の会議出席依頼を表します。  <br/> |
   
## <a name="remarks"></a>備考

この要素は、 [CalendarItemType](calendaritemtype.md)に RecurringMaster の値が設定されている場合に有効です。 
  
MicrosoftExchange Server 2007 がインストールされているクライアント アクセス サーバーの役割を実行しているコンピューターの EWS 仮想ディレクトリには、この要素を記述するスキーマがあります。
  
## <a name="element-information"></a>要素情報

|||
|:-----|:-----|
|名前空間  <br/> |http://schemas.microsoft.com/exchange/services/2006/types  <br/> |
|スキーマ名  <br/> |タイプのスキーマ  <br/> |
|検証ファイル  <br/> |Types.xsd  <br/> |
|空にすることができます。  <br/> |False  <br/> |
   
## <a name="see-also"></a>関連項目



- [Exchange での EWS の XML 要素](ews-xml-elements-in-exchange.md)
  

  [Exchange 用 EWS リファレンス](ews-reference-for-exchange.md)

