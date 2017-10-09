---
title: "Magistrala usług .NET i protokołu AMQP 1.0 aaaService | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Service Bus z .NET z protokołu AMQP"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>Przy użyciu usługi Service Bus z .NET z protokołu AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>Pobieranie hello zestaw SDK usługi Service Bus

Obsługa protokołu AMQP 1.0 jest dostępna w hello zestaw SDK usługi Service Bus w wersji 2.1 lub nowszej. Zapewnia masz najnowszą wersję hello pobierając hello magistrali usługi bits z [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>Konfigurowanie toouse aplikacji .NET protokołu AMQP 1.0

Domyślnie biblioteki klienta .NET magistrali usługi hello komunikuje się z hello usługi Service Bus przy użyciu dedykowanych protokołu opartego na protokole SOAP. toouse protokołu AMQP 1.0 zamiast hello domyślnym protokołem wymaga jawnego konfiguracji hello parametry połączenia magistrali usług, zgodnie z opisem w następnej sekcji hello. Inne niż ta zmiana kodu aplikacji pozostaje niezmieniony, korzystając z protokołu AMQP 1.0.

W bieżącej wersji hello istnieje kilka funkcji interfejsu API, które nie są obsługiwane w przypadku korzystania z protokołu AMQP. Nieobsługiwanych funkcji są później wymienione w sekcji hello [nieobsługiwane funkcje, ograniczenia i różnice funkcjonalne](#unsupported-features-restrictions-and-behavioral-differences). Niektóre zaawansowane ustawienia konfiguracji hello również mieć inne znaczenie, korzystając z protokołu AMQP.

### <a name="configuration-using-appconfig"></a>Konfiguracja przy użyciu pliku App.config

Dobrym rozwiązaniem dla ustawień toostore pliku konfiguracji App.config aplikacji toouse hello jest. W przypadku aplikacji usługi Service Bus można użyć parametry połączenia magistrali usług hello toostore App.config. Przykładowy plik App.config wygląda następująco:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

Witaj wartość hello `Microsoft.ServiceBus.ConnectionString` ustawienie jest hello parametry połączenia magistrali usług, które jest używane tooconfigure hello połączenia tooService magistrali. Hello format jest następujący:

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Gdzie `[namespace]` i `SharedAccessKey` są uzyskiwane z hello [portalu Azure] [ Azure portal] po utworzeniu przestrzeni nazw usługi Service Bus. Aby uzyskać więcej informacji, zobacz [tworzenie przestrzeni nazw usługi Service Bus przy użyciu portalu Azure hello][Create a Service Bus namespace using hello Azure portal].

Podczas korzystania z protokołu AMQP, Dołącz hello ciągu połączenia za pomocą `;TransportType=Amqp`. Ten element notation nakazuje powitania klienta biblioteki toomake jego tooService połączenia magistrali przy użyciu protokołu AMQP 1.0.

## <a name="message-serialization"></a>Serializacja wiadomości

Za pomocą protokołu domyślne hello hello domyślnej serializacji biblioteki klienta .NET hello jest toouse hello [DataContractSerializer] [ DataContractSerializer] wpisz tooserialize [BrokeredMessage ] [ BrokeredMessage] wystąpienia dla transportu między powitania klienta biblioteki i hello usługi Service Bus. Gdy tryb transportu protokołu AMQP hello jest używany, powitania klienta biblioteki używa system typów protokołu AMQP hello serializacji hello [komunikatu obsługiwanego przez brokera] [ BrokeredMessage] do wiadomości protokołu AMQP. Serializacja tego umożliwia toobe wiadomość hello odebrał i interpretowane przez aplikację odbierającą, potencjalnie jest uruchomiona na innej platformie, na przykład aplikację języka Java, która używa hello tooaccess JMS interfejsu API usługi Service Bus.

Podczas konstruowania [BrokeredMessage] [ BrokeredMessage] wystąpienia obiektu .NET. można podać jako parametr toohello Konstruktor tooserve jako hello treści wiadomości powitania. Dla obiektów, które mogą być mapowane tooAMQP typy pierwotne treści hello jest serializowany z typami danych protokołu AMQP. Jeśli obiekt hello nie można zamapować bezpośrednio do typu pierwotnego protokołu AMQP; oznacza to, że definicja aplikacji hello, a następnie obiekt hello typu niestandardowego jest zserializowanym przy użyciu hello [DataContractSerializer][DataContractSerializer], i hello serializacji bajty są wysyłane wiadomości protokołu AMQP danych.

toofacilitate współdziałania z klientami z systemem innym niż .NET używać tylko typów .NET, które można serializować bezpośrednio do typów protokołu AMQP dla treści wiadomości powitania hello. Witaj w poniższej tabeli Szczegóły tych typów i hello odpowiednie mapowanie toohello AMQP typu systemu.

| Typ obiektu treści .NET | Typ protokołu AMQP zamapowane | Typ sekcji treści protokołu AMQP |
| --- | --- | --- |
| wartość logiczna |Wartość logiczna |Wartość AMQP |
| Bajtów |ubyte |Wartość AMQP |
| ushort |ushort |Wartość AMQP |
| uint |uint |Wartość AMQP |
| ulong |ulong |Wartość AMQP |
| sbyte — |Bajtów |Wartość AMQP |
| krótki |krótki |Wartość AMQP |
| int |int |Wartość AMQP |
| długa |długa |Wartość AMQP |
| Float |Float |Wartość AMQP |
| O podwójnej precyzji |O podwójnej precyzji |Wartość AMQP |
| Decimal |decimal128 |Wartość AMQP |
| char |char |Wartość AMQP |
| Data i godzina |sygnatura czasowa |Wartość AMQP |
| Identyfikator GUID |Identyfikator UUID |Wartość AMQP |
| Byte] |Binarne |Wartość AMQP |
| Ciąg |Ciąg |Wartość AMQP |
| Interfejs System.Collections.IList |Lista |Wartość AMQP: elementy zawarte w kolekcji hello można tylko te, które są zdefiniowane w tej tabeli. |
| System.Array |Tablica |Wartość AMQP: elementy zawarte w kolekcji hello można tylko te, które są zdefiniowane w tej tabeli. |
| System.Collections.IDictionary |mapy |Wartość AMQP: elementy zawarte w kolekcji hello można tylko te, które są zdefiniowane w tej tabeli. Uwaga: obsługiwane są tylko kluczy będących ciągami. |
| Identyfikator URI |Opisane ciąg (zobacz hello w poniższej tabeli) |Wartość AMQP |
| DateTimeOffset |Opisane długi (zobacz hello w poniższej tabeli) |Wartość AMQP |
| Zakres czasu |Opisane długi (zobacz poniżej hello) |Wartość AMQP |
| Strumień |Binarne |Dane AMQP (może to być wiele). Witaj danych sekcje zawierają hello bajtów raw odczytywać hello obiektu strumienia. |
| Drugi obiekt |Binarne |Dane AMQP (może to być wiele). Zawiera dane binarne hello serializacji obiektu hello, który używa hello DataContractSerializer lub serializatora dostarczone przez aplikację hello. |

| Typ architektury .NET | Zmapowane AMQP opisem typu | Uwagi |
| --- | --- | --- |
| Identyfikator URI |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| DateTimeOffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| Zakres czasu |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Nieobsługiwane funkcje, ograniczenia i różnice funkcjonalne

następujące funkcje interfejsu API usługi Service Bus .NET hello Hello nie są obecnie obsługiwane, korzystając z protokołu AMQP:

* Transakcje
* Wyślij za pośrednictwem docelowego transferu

Istnieją również pewne niewielkie różnice w zachowaniu hello hello interfejsu API usługi Service Bus .NET, korzystając z protokołu AMQP, porównaniu toohello domyślnym protokołem:

* Witaj [OperationTimeout] [ OperationTimeout] właściwość jest ignorowana.
* `MessageReceiver.Receive(TimeSpan.Zero)`jest zaimplementowany jako `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Kończenie wiadomości przez tokeny blokady jest możliwe tylko przez odbiorców wiadomość hello, początkowo odebranych wiadomości powitania.

## <a name="controlling-amqp-protocol-settings"></a>Kontrolowanie ustawień protokołu AMQP

Witaj [interfejsów API architektury .NET](/dotnet/api/) ujawnia kilka ustawień toocontrol hello zachowanie hello protokołu AMQP:

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: formanty hello początkowej środki stosowane tooa łącza. Witaj domyślna to 0.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: formanty hello maksymalny rozmiar ramki protokołu AMQP oferowane podczas negocjowania hello na czas otwarcia połączenia. Witaj domyślny to 65 536 bajtów.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: Jeśli transfery batchable, ta wartość określa maksymalne opóźnienie hello wysyłania przepisy. Dziedziczone przez nadawców/odbiorcy domyślnie. Poszczególne nadawcy/odbiorcy mogą zastąpić hello domyślna, czyli 20 milisekund.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**: Określa, czy protokół AMQP nawiązywane są połączenia za pośrednictwem połączenia SSL. Domyślnie Hello **true**.

## <a name="next-steps"></a>Następne kroki

Gotowe toolearn więcej? Odwiedź hello następującego łącza:

* [Omówienie protokołu AMQP magistrali usług]
* [Obsługa protokołu AMQP 1.0 tematów i kolejek usługi Service Bus na partycje]
* [Protokół AMQP w usłudze Service Bus dla systemu Windows Server]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Omówienie protokołu AMQP magistrali usług]: service-bus-amqp-overview.md
[Obsługa protokołu AMQP 1.0 tematów i kolejek usługi Service Bus na partycje]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Protokół AMQP w usłudze Service Bus dla systemu Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
