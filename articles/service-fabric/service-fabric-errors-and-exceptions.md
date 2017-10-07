---
title: "aaaCommon klienta fabricclient z rolą wyjątki zgłaszane | Dokumentacja firmy Microsoft"
description: "Opisuje hello wspólnej wyjątków i błędów, które powitania klienta fabricclient z rolą interfejsów API może zostać wygenerowany podczas wykonywania operacji zarządzania aplikacji i klastra."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Typowe wyjątków i błędów podczas pracy z powitania klienta fabricclient z rolą interfejsów API
Witaj [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) interfejsy API umożliwia klastra i aplikacji administratorzy tooperform zadań administracyjnych w aplikacji, usługi lub klastra sieci szkieletowej usług. Na przykład wdrożenia aplikacji, uaktualniania i usuwania, sprawdzania kondycji hello klastra lub testowanie usługi. Deweloperzy aplikacji i Administratorzy klastra za pomocą hello interfejsów API klienta fabricclient z rolą toodevelop narzędzi do zarządzania hello klastra sieci szkieletowej usług i aplikacji.

Istnieje wiele różnych typów działań, które mogą być wykonywane przy użyciu klienta fabricclient z rolą.  Każda metoda można zgłaszają wyjątki, błędy tooincorrect danych wejściowych, błędy podczas wykonywania lub infrastruktury przejściowych problemów.  Zobacz dokumentacji toofind odwołanie hello interfejsu API, które wyjątki są zgłaszane przez określonej metody. Istnieją pewne wyjątki, jednak może zostać wygenerowany przez wiele różnych [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) interfejsów API. Witaj poniższej tabeli wymieniono hello wyjątki, które są wspólne dla powitania klienta fabricclient z rolą interfejsów API.

| Wyjątek | Generowane, gdy |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Witaj [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) obiekt jest w stanie zamkniętym. Usuwa hello [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) obiekt jest używany i utworzenia wystąpienia nowy [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) obiektu. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |Upłynął limit czasu operacji Hello. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) jest zwracany, gdy operacja hello przyjmuje więcej niż toocomplete parametru MaxOperationTimeout. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |Nie można sprawdzić dostępu Hello hello operacji. Zwracany jest błąd E_ACCESSDENIED. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Wystąpił błąd w czasie wykonywania podczas wykonywania operacji hello. Powitania klienta fabricclient z rolą metod potencjalnie może zgłosić [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) właściwość wskazuje dokładną przyczynę hello hello wyjątku. Kody błędów są zdefiniowane w hello [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) wyliczenia. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |Witaj operacja nie powiodła się ze względu na stan błędu przejściowego tooa określonego rodzaju. Na przykład operacji może nie powieść, ponieważ kworum replik jest tymczasowo niedostępna. Wyjątki przejściowej odpowiada toofailed operacje, które można ponowić. |

Niektóre typowe [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) błędów, które mogą być zwracane w [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException):

| Błąd | Warunek |
| --- |:--- |
| CommunicationError |Witaj operacji toofail, ponów próbę wykonania operacji hello z powodu błędu komunikacji. |
| InvalidCredentialType |Typ poświadczeń Hello jest nieprawidłowy. |
| InvalidX509FindType |Witaj X509FindType jest nieprawidłowy. |
| InvalidX509StoreLocation |Lokalizacja magazynu Hello X509 jest nieprawidłowy. |
| InvalidX509StoreName |Nazwa magazynu Hello X509 jest nieprawidłowy. |
| InvalidX509Thumbprint |ciąg odcisk palca certyfikatu Hello X509 jest nieprawidłowy. |
| InvalidProtectionLevel |poziom ochrony Hello jest nieprawidłowy. |
| InvalidX509Store |Nie można otworzyć magazynu certyfikatów Hello X509. |
| InvalidSubjectName |Nazwa podmiotu Hello jest nieprawidłowa. |
| InvalidAllowedCommonNameList |format Hello wspólnej nazwy ciąg z listą jest nieprawidłowy. Powinno być rozdzielaną przecinkami listą. |

