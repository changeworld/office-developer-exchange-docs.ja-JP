---
title: Exchange で EWS を使用して連絡先グループを作成する
manager: sethgros
ms.date: 11/16/2014
ms.audience: Developer
localization_priority: Normal
ms.assetid: acec6e73-c016-419d-be1a-8ec5d993addb
description: Exchange で EWS マネージ API または EWS を使用して、連絡先グループを作成する方法について説明します。
ms.openlocfilehash: b3357f24e07a9c1b3b37ccb63b0f4f0d0a1d6fcf
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2018
ms.locfileid: "19758934"
---
# <a name="create-contact-groups-by-using-ews-in-exchange"></a>Exchange で EWS を使用して連絡先グループを作成する

Exchange で EWS マネージ API または EWS を使用して、連絡先グループを作成する方法について説明します。
  
EWS マネージ API または EWS を使用して、個人用[配布グループ](distribution-groups-and-ews-in-exchange.md)である連絡先グループを作成できます。 連絡先グループを作成するには、[ContactGroup](http://msdn.microsoft.com/ja-JP/library/office/microsoft.exchange.webservices.data.contactgroup%28v=exchg.80%29.aspx) EWS マネージ API クラスのメソッドを使用するか、[CreateItem](http://msdn.microsoft.com/library/78a52120-f1d0-4ed7-8748-436e554f75b6%28Office.15%29.aspx) EWS 操作を使用します。 
  
EWS マネージ API と EWS のどちらを使用したとしても、ユニバーサル配布グループもセキュリティ グループも作成できません。 ユニバーサル配布グループまたはセキュリティ グループを作成するには、[New-DistributionGroup](http://technet.microsoft.com/ja-JP/library/aa998856%28v=exchg.150%29.aspx) [Exchange 管理シェル コマンドレット](http://msdn.microsoft.com/ja-JP/library/ff326159%28v=exchg.140%29.aspx)を使用できます。 
  
## <a name="create-a-contact-group-by-using-the-ews-managed-api"></a>EWS マネージ API を使用して連絡先グループを作成する
<a name="bk_EWSMA"> </a>

連絡先グループを作成するために必要となるのは、2 つの情報、つまりグループの名前とグループに追加するメンバーだけです。次の例は、2 人のグループ メンバーが含まれる簡単な連絡先グループを作成する方法を示します。
  
```cs
// Create a new contact group object.
ContactGroup myContactGroup = new ContactGroup(service);
// Give the group a name.
myContactGroup.DisplayName = "My Contact Group";
// Add some members to the group.
myContactGroup.Members.Add(new GroupMember("sadie@contoso.com"));
myContactGroup.Members.Add(new GroupMember("alfred@contoso.com"));
// Save the group.
myContactGroup.Save();

```

## <a name="create-a-contact-group-by-using-ews"></a>EWS を使用して連絡先グループを作成する
<a name="bk_EWSMA"> </a>

コードがさらに数行必要となる可能性がありますが、[CreateItem](http://msdn.microsoft.com/library/78a52120-f1d0-4ed7-8748-436e554f75b6%28Office.15%29.aspx) EWS 操作を使用して連絡先グループを作成できます。 次の XML 要求例は、連絡先グループを作成する方法を示しています。 またこれは、[EWS マネージ API を使用して連絡先グループを作成する](#bk_EWSMA)際に、送信される XML 要求でもあります。
  
```XML
<?xml version="1.0" encoding="utf-8"?>
   <CreateItem xmlns="http://schemas.microsoft.com/exchange/services/2006/messages" 
MessageDisposition="SaveOnly">
      <Items xmlns:m="http://schemas.microsoft.com/exchange/services/2006/messages">
         <DistributionList xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
            <DisplayName xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
               My Contact Group
            </DisplayName>
            <Members xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
               <Member xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
                  <Mailbox xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
                     <EmailAddress xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
                        sadie@contoso.com
                     </EmailAddress>
                  </Mailbox>
               </Member>
               <Member xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
                  <Mailbox xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
                     <EmailAddress xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
                        alfred@contoso.com
                     </EmailAddress>
                  </Mailbox>
               </Member>
            </Members>
         </DistributionList>
      </Items>
   </CreateItem>
```

要求に対して成功した XML 応答の例を次に示します。返される値に、新しい連絡先グループのアイテム ID、および連絡先グループを変更したり、グループを展開してメンバーを表示したりするために他のコードで使用できる変更キーが含まれている点に注目してください。アイテム ID は読みやすいように短縮されています。
  
```XML
<?xml version="1.0" encoding="utf-8"?>
   <CreateItemResponse xmlns="http://schemas.microsoft.com/exchange/services/2006/messages">
      <ResponseMessages xmlns="http://schemas.microsoft.com/exchange/services/2006/messages">
         <CreateItemResponseMessage ResponseClass="Success" 
             xmlns="http://schemas.microsoft.com/exchange/services/2006/messages">
            <ResponseCode xmlns="http://schemas.microsoft.com/exchange/services/2006/messages">
               NoError
            </ResponseCode>
            <Items xmlns="http://schemas.microsoft.com/exchange/services/2006/messages">
               <DistributionList xmlns="http://schemas.microsoft.com/exchange/services/2006/types">
                  <ItemId xmlns="http://schemas.microsoft.com/exchange/services/2006/types" 
                          Id="AAMkADBlY…" 
                          ChangeKey="EgAAABYAAAAD7hO1SJPWTbICFWZ4U3NMAABXzQiK" />
               </DistributionList>
            </Items>
         </CreateItemResponseMessage>
      </ResponseMessages>
   </CreateItemResponse>
```

## <a name="see-also"></a>関連項目


- [Exchange の配布グループと EWS](distribution-groups-and-ews-in-exchange.md)
    
- [Exchange 2013 の EWS を使用して配布グループを展開する](how-to-expand-distribution-groups-by-using-ews-in-exchange-2013.md)
    

