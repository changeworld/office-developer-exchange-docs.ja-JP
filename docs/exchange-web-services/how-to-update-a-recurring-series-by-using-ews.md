---
title: EWS を使用して一連の定期的な更新プログラム
manager: sethgros
ms.date: 11/16/2014
ms.audience: Developer
localization_priority: Normal
ms.assetid: 7e61bee9-4840-4773-a0a7-47b11e1fdf59
description: Exchange の EWS マネージ API または EWS を使用して、定期的なアイテムの予定を変更する方法を説明します。
ms.openlocfilehash: ecee78457d2e6f91483cf897cfb4976fbd83400c
ms.sourcegitcommit: 34041125dc8c5f993b21cebfc4f8b72f0fd2cb6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "19759071"
---
# <a name="update-a-recurring-series-by-using-ews"></a>EWS を使用して一連の定期的な更新プログラム

Exchange の EWS マネージ API または EWS を使用して、定期的なアイテムの予定を変更する方法を説明します。
  
EWS のマネージ API または EWS を使用するには、いずれかの[データ系列全体を更新](how-to-update-a-recurring-series-by-using-ews-in-exchange.md)、または 1 回を更新することにより定期的な系列を更新します。 この資料では、1 回を更新する方法について説明します。
  
系列の 1 つの予定を変更することは、[単独の予定を変更](how-to-update-appointments-and-meetings-by-using-ews-in-exchange.md)するのには非常に似ています。 同じメソッドと、操作を使用するが、変更するアイテムのアイテム ID を使用します。
  
シリーズの 1 回を変更すると、その出現は一連の定期的なマスターに関連付けられている変更の予定の配列に追加されます。 [Appointment.ModifiedOccurrences](http://msdn.microsoft.com/en-us/library/microsoft.exchange.webservices.data.appointment.modifiedoccurrences%28v=exchg.80%29.aspx) EWS のマネージ API のプロパティまたは[ModifiedOccurrences](http://msdn.microsoft.com/library/552932fc-b3b4-486e-8d73-32c0bb10bd68%28Office.15%29.aspx)の EWS の要素を使用するには、変更された系列のすべての予定にアクセスします。 
  
## <a name="modify-a-single-occurrence-in-a-series-by-using-the-ews-managed-api"></a>EWS マネージ API を使用して定期的なアイテムの単一のオカレンスを変更する

定期的なアイテムの単一のインスタンスを変更するには、次の操作を実行します。
  
1. 項目のインデックス値、またはアイテムの ID を使用して[Appointment.Bind](http://msdn.microsoft.com/en-us/library/microsoft.exchange.webservices.data.appointment.bind%28v=exchg.80%29.aspx)メソッドと[Appointment.BindToOccurrence](http://msdn.microsoft.com/en-us/library/office/microsoft.exchange.webservices.data.appointment.bindtooccurrence%28v=exchg.80%29.aspx)メソッドを使用して変更しアイテムへのバインドします。 発生に対応する[予定](http://msdn.microsoft.com/en-us/library/microsoft.exchange.webservices.data.appointment%28v=exchg.80%29.aspx)のオブジェクトの[Id](http://msdn.microsoft.com/en-us/library/microsoft.exchange.webservices.data.item.id%28v=exchg.80%29.aspx)プロパティとは、[アイテム Id](http://msdn.microsoft.com/en-us/library/microsoft.exchange.webservices.data.occurrenceinfo.itemid%28v=exchg.80%29.aspx)オブジェクトのプロパティ、 [OccurrenceInfo](http://msdn.microsoft.com/en-us/library/microsoft.exchange.webservices.data.occurrenceinfo%28v=exchg.80%29.aspx)の発生に対応するから、この ID を取得します。 
    
2. オカレンスの Appointment オブジェクトのプロパティを更新します。
    
3. [Appointment.Save](http://msdn.microsoft.com/en-us/library/office/microsoft.exchange.webservices.data.appointment.save%28v=exchg.80%29.aspx)メソッドを使用して発生の予定オブジェクトへの変更を保存します。 
    
次の例では、一連の定期的な予定を更新し、定期的なマスターの変更後の予定が更新されたことを確認します。 次の使用例は、認証済み Exchange サーバーおよび**サービス**をという名前の[ExchangeService](http://msdn.microsoft.com/en-us/library/microsoft.exchange.webservices.data.exchangeservice%28v=exchg.80%29.aspx)オブジェクトを取得することを想定しています。 `recurrenceMasterId`のパラメーターでは、出現する位置を変更する定期的なマスターに関連付けられている識別子です。 
  
```cs
public static ItemId ModifyARecurringSeries(ExchangeService service, ItemId recurrenceMasterId)
{
    Appointment calendarItem = Appointment.Bind(service, recurrenceMasterId, new PropertySet(AppointmentSchema.AppointmentType));
    Appointment recurrMaster = new Appointment(service);
    if (calendarItem.AppointmentType == AppointmentType.RecurringMaster)
    {
        // Get the recurring master from an occurrence in a recurring series with the properties you need.
        recurrMaster = Appointment.Bind(service,
                                        recurrenceMasterId,
                                        new PropertySet(AppointmentSchema.AppointmentType,
                                                        AppointmentSchema.Subject,
                                                        AppointmentSchema.FirstOccurrence,
                                                        AppointmentSchema.LastOccurrence,
                                                        AppointmentSchema.ModifiedOccurrences,
                                                        AppointmentSchema.DeletedOccurrences));
    }
    else
    {
        Console.WriteLine("Item id was not for a recurring master.");
        return recurrenceMasterId;
    }
    // Bind to the second occurrence in the series with the properties to modify.
    Appointment occurrenceToModify = Appointment.BindToOccurrence(service,
                                                                    recurrMaster.Id,
                                                                    2,
                                                                    new PropertySet(AppointmentSchema.Location,
                                                                                    AppointmentSchema.Start,
                                                                                    AppointmentSchema.End,
                                                                                    AppointmentSchema.RequiredAttendees,
                                                                                    AppointmentSchema.Subject));
    // Update the properties you want to change.
    occurrenceToModify.Location = "Helipad of Contoso Bldg 1";
    occurrenceToModify.Start = occurrenceToModify.Start.AddDays(1);
    occurrenceToModify.End = occurrenceToModify.End.AddDays(1);
    occurrenceToModify.RequiredAttendees.Add("Contoso CEO", "sadie@contoso");
    occurrenceToModify.RequiredAttendees.Add("Contoso Head of Research", "ronnie@contoso.com");
    occurrenceToModify.RequiredAttendees.Add("Contoso Head of Security", "alfred@contoso.com");
    occurrenceToModify.Subject = occurrenceToModify.Subject.ToString() + ":Mandatory";
    // Update the occurrence in your calendar folder and send meeting update requests to attendees.
    // This method call results in an UpdateItem request to EWS.
    occurrenceToModify.Update(ConflictResolutionMode.AlwaysOverwrite, SendInvitationsOrCancellationsMode.SendToAllAndSaveCopy);
    // View updated and deleted occurrences on the recurring master prior to retrieving updated information.
    Console.WriteLine("Modified Occurrences prior to updating recurring master: {0}",
                    (recurrMaster.ModifiedOccurrences == null ? "None" : recurrMaster.ModifiedOccurrences.Count.ToString()));
    // Update the recurring master to view the modified and deleted occurrences.
    recurrMaster = Appointment.Bind(service, recurrenceMasterId, new PropertySet(AppointmentSchema.ModifiedOccurrences,
                                                                        AppointmentSchema.DeletedOccurrences));
    // View updated and deleted occurrences on the recurring master after retrieving updated information.
    Console.WriteLine("Modified Occurrences after updating recurring master:\t {0}",
                    (recurrMaster.ModifiedOccurrences == null ? "None" : recurrMaster.ModifiedOccurrences.Count.ToString()));
    return recurrMaster.Id;            
}

```

## <a name="modify-a-single-occurrence-in-a-series-by-using-ews"></a>EWS を使用して定期的なアイテムの単一のオカレンスを変更する

シリーズの 1 つのインスタンスを変更することは、本質的に単独の予定を変更することと同じです。 [アイテム Id](http://msdn.microsoft.com/library/3350b597-57a0-4961-8f44-8624946719b4%28Office.15%29.aspx)または[OccurrenceItemId](http://msdn.microsoft.com/library/4a15bbc3-5b93-4193-b9ec-da32f0a9a552%28Office.15%29.aspx)要素のいずれかを使用して変更するのには発生することが可能です。 
  
[UpdateItem](http://msdn.microsoft.com/library/5d027523-e0bc-4da2-b60b-0cb9fc1fdfe4%28Office.15%29.aspx)操作を使用して定期的な予定の系列での出来事を更新するとき、次の使用例は要求 XML を示します。 **アイテム Id**と**変更キー**は、読みやすくするために短縮されます。 
  
```XML
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
               xmlns:m="http://schemas.microsoft.com/exchange/services/2006/messages" 
               xmlns:t="http://schemas.microsoft.com/exchange/services/2006/types" 
               xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Header>
    <t:RequestServerVersion Version="Exchange2010" />
  </soap:Header>
  <soap:Body>
    <m:UpdateItem ConflictResolution="AlwaysOverwrite" SendMeetingInvitationsOrCancellations="SendToAllAndSaveCopy">
      <m:ItemChanges>
        <t:ItemChange>
          <t:ItemId Id="AAMkA" ChangeKey="DwAAAB" />
          <t:Updates>
            <t:SetItemField>
              <t:FieldURI FieldURI="calendar:Location" />
              <t:CalendarItem>
                <t:Location>Helipad of Contoso Bldg 1</t:Location>
              </t:CalendarItem>
            </t:SetItemField>
            <t:SetItemField>
              <t:FieldURI FieldURI="calendar:Start" />
              <t:CalendarItem>
                <t:Start>2014-03-27T19:33:00.000-07:00</t:Start>
              </t:CalendarItem>
            </t:SetItemField>
            <t:SetItemField>
              <t:FieldURI FieldURI="calendar:End" />
              <t:CalendarItem>
                <t:End>2014-03-27T20:33:00.000-07:00</t:End>
              </t:CalendarItem>
            </t:SetItemField>
            <t:SetItemField>
              <t:FieldURI FieldURI="calendar:RequiredAttendees" />
              <t:CalendarItem>
                <t:RequiredAttendees>
                  <t:Attendee>
                    <t:Mailbox>
                      <t:Name>Mack@contoso.com</t:Name>
                      <t:EmailAddress>Mack@contoso.com</t:EmailAddress>
                      <t:RoutingType>SMTP</t:RoutingType>
                    </t:Mailbox>
                  </t:Attendee>
                  <t:Attendee>
                    <t:Mailbox>
                      <t:Name>Sadie@contoso.com</t:Name>
                      <t:EmailAddress>Sadie@contoso.com</t:EmailAddress>
                      <t:RoutingType>SMTP</t:RoutingType>
                    </t:Mailbox>
                  </t:Attendee>
                  <t:Attendee>
                    <t:Mailbox>
                      <t:Name>Magdalena@contoso.com</t:Name>
                      <t:EmailAddress>Magdalena@contoso.com</t:EmailAddress>
                      <t:RoutingType>SMTP</t:RoutingType>
                    </t:Mailbox>
                  </t:Attendee>
                  <t:Attendee>
                    <t:Mailbox>
                      <t:Name>Contoso CEO</t:Name>
                      <t:EmailAddress>sadie@contoso</t:EmailAddress>
                    </t:Mailbox>
                  </t:Attendee>
                  <t:Attendee>
                    <t:Mailbox>
                      <t:Name>Contoso Head of Research</t:Name>
                      <t:EmailAddress>ronnie@contoso.com</t:EmailAddress>
                    </t:Mailbox>
                  </t:Attendee>
                  <t:Attendee>
                    <t:Mailbox>
                      <t:Name>Contoso Head of Security</t:Name>
                      <t:EmailAddress>alfred@contoso.com</t:EmailAddress>
                    </t:Mailbox>
                  </t:Attendee>
                </t:RequiredAttendees>
              </t:CalendarItem>
            </t:SetItemField>
            <t:SetItemField>
              <t:FieldURI FieldURI="item:Subject" />
              <t:CalendarItem>
                <t:Subject>Weekly Update Meeting:Mandatory</t:Subject>
              </t:CalendarItem>
            </t:SetItemField>
          </t:Updates>
        </t:ItemChange>
      </m:ItemChanges>
    </m:UpdateItem>
  </soap:Body>
</soap:Envelope>
```

**NoError**発生が正常に更新されたことを示すとの[ItemId](http://msdn.microsoft.com/library/3350b597-57a0-4961-8f44-8624946719b4%28Office.15%29.aspx)の[ResponseCode](http://msdn.microsoft.com/library/4b84d670-74c9-4d6d-84e7-f0a9f76f0d93%28Office.15%29.aspx)値が含まれることを示す[UpdateItemResponse](http://msdn.microsoft.com/library/023b79b4-c675-4669-9112-d85499ec4fc4%28Office.15%29.aspx)メッセージの**UpdateItem**要求に対するサーバーの応答します。更新の予定です。 
  
## <a name="see-also"></a>関連項目


- [Calendars and EWS in Exchange](calendars-and-ews-in-exchange.md)
    
- [Exchange EWS を使用して予定および会議を更新します。](how-to-update-appointments-and-meetings-by-using-ews-in-exchange.md)
    
- [定期的なパターンと EWS](recurrence-patterns-and-ews.md)
    
- [Exchange で EWS を使用して、定期的にアクセスします。](how-to-access-a-recurring-series-by-using-ews-in-exchange.md)
    
- [Exchange EWS を使用して定期的な系列を作成します。](how-to-create-a-recurring-series-by-using-ews-in-exchange.md)
    
- [Exchange EWS を使用して一連の定期的な予定を削除します。](how-to-delete-appointments-in-a-recurring-series-by-using-ews-in-exchange.md)
    
- [Exchange EWS を使用して一連の定期的な更新プログラム](how-to-update-a-recurring-series-by-using-ews-in-exchange.md)
    
