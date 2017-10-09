---
title: "Ustawienia KVSActorStateProvider aaaChange w Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Informacje na temat konfigurowania stanowe uczestnikami typu KVSActorStateProvider sieć szkieletowa usług Azure."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Konfigurowanie Reliable Actors — KVSActorStateProvider
Domyślna konfiguracja hello KVSActorStateProvider można modyfikować, zmieniając pliku settings.xml hello wygenerowanego w hello katalog główny pakietu Microsoft Visual Studio w folderze konfiguracji powitania dla określonego aktora hello.

środowisko uruchomieniowe usługi sieć szkieletowa usług Azure Hello szuka nazwy sekcji wstępnie zdefiniowanych w pliku settings.xml hello i wykorzystuje wartości konfiguracji hello podczas tworzenia hello podstawowych składników środowiska wykonawczego.

> [!NOTE]
> Czy **nie** usunięcia lub zmodyfikowania nazwy sekcji hello hello następujące konfiguracje w pliku settings.xml hello wygenerowanego w hello rozwiązania Visual Studio.
> 
> 

## <a name="replicator-security-configuration"></a>Konfiguracja zabezpieczeń replikatora
Replikator konfiguracjach zabezpieczeń są używane toosecure kanał komunikacyjny hello, używaną podczas replikacji. Oznacza to, czy usługi nie widzi siebie nawzajem ruch związany z replikacją, zapewnia, że dane hello jest zyskuje dużą dostępność również jest bezpieczne.
Domyślnie puste zabezpieczeń sekcji konfiguracji uniemożliwia zabezpieczeń replikacji.

### <a name="section-name"></a>Nazwa sekcji
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Konfiguracja replikatora
Konfiguracje replikatora skonfiguruj replikatora hello, odpowiedzialną za tworzenie stanu dostawcy stanu aktora hello wysoce niezawodne.
Konfiguracja domyślna Hello jest generowany przez hello szablonu Visual Studio i powinny wystarczyć. Ta sekcja zawiera informacje o dodatkowych konfiguracjach, które są dostępne tootune hello replikatora.

### <a name="section-name"></a>Nazwa sekcji
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nazwy konfiguracji
| Nazwa | Jednostka | Wartość domyślna | Uwagi |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Sekundy |0.015 |Czasie, dla których replikatora hello na dodatkowej czeka powitania po otrzymaniu operacji przed odsyła toohello potwierdzenia podstawowego. Inne toobe potwierdzeń, wysyłane do operacji przetwarzane w ramach tego interwału są wysyłane jako jedna odpowiedź. |
| ReplicatorEndpoint |Nie dotyczy |Brak wartości domyślnej — wymagany parametr |Adres IP i port, który hello replikatora podstawowe i pomocnicze użyje toocommunicate z innych replikatorów hello zestawu replik. To powinien odwoływać się do zasobów punkt końcowy protokołu TCP w hello manifestu usługi. Odwołuje się zbyt[zasoby manifestu usługi](service-fabric-service-manifest-resources.md) tooread więcej informacji na temat definiowania zasobów punktu końcowego w hello manifestu usługi. |
| retryInterval |Sekundy |5 |Okres, po którym hello replikatora ponownie przesyła a komunikat, jeśli nie otrzyma potwierdzenia dla danej operacji. |
| MaxReplicationMessageSize |Bajty |50 MB |Maksymalny rozmiar danych replikacji, które mogą być przenoszone w pojedynczym komunikacie. |
| MaxPrimaryReplicationQueueSize |Liczba operacji |1024 |Maksymalna liczba operacji w kolejce głównej hello. Operacja są zwalniane, gdy Replikator głównej hello otrzyma potwierdzenia od wszystkich hello replikatorów dodatkowej. Ta wartość musi być większa niż 64 i potęgą liczby 2. |
| MaxSecondaryReplicationQueueSize |Liczba operacji |2048 |Maksymalna liczba operacji w kolejce dodatkowej hello. Operacja są zwalniane po dokonaniu jej stan wysokiej dostępności za pośrednictwem trwałości. Ta wartość musi być większa niż 64 i potęgą liczby 2. |

## <a name="store-configuration"></a>Konfiguracja magazynu
Konfiguracje magazynu są używane tooconfigure hello lokalnego magazynu, który jest używane toopersist hello stanu, który jest replikowany.
Konfiguracja domyślna Hello jest generowany przez hello szablonu Visual Studio i powinny wystarczyć. Ta sekcja zawiera informacje o dodatkowych konfiguracjach, które są dostępne tootune hello lokalnego magazynu.

### <a name="section-name"></a>Nazwa sekcji
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Nazwy konfiguracji
| Nazwa | Jednostka | Wartość domyślna | Uwagi |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |w milisekundach |200 |Ustawia maksymalną hello przetwarzanie wsadowe interwał zatwierdzeń trwałego magazynu lokalnego. |
| MaxVerPages |Liczba stron |16384 |Witaj maksymalną liczbę stron wersji w lokalne powitania przechowywania bazy danych. Określa maksymalną liczbę oczekujących transakcji hello. |

## <a name="sample-configuration-file"></a>Przykładowy plik konfiguracyjny
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```
## <a name="remarks"></a>Uwagi
Parametr BatchAcknowledgementInterval Hello Określa opóźnienie replikacji. Wartość "0" powoduje hello można uzyskać najmniejsze możliwe opóźnienia, kosztem hello przepływności (jak więcej komunikatów potwierdzenia musi być wysyłane i przetwarzane, zawierający mniejszą liczbę potwierdzeń).
Hello im większa wartość hello BatchAcknowledgementInterval, hello wyższej hello ogólne przepustowość replikacji na powitania kosztem większego opóźnienia operacji. Bezpośrednio przekłada opóźnienia toohello zatwierdzeń transakcji.

