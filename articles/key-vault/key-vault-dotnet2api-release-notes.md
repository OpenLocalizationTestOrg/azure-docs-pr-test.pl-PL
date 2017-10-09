---
title: Informacje o wersji interfejsu API 2.x .NET magazynu aaaKey | Dokumentacja firmy Microsoft
description: ".NET umożliwia deweloperom toocode tego interfejsu API dla usługi Azure Key Vault"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Usługi Azure Key Vault .NET 2.0 — przewodnik migracji i informacje o wersji
Witaj następujące wskazówki i informacje są dla deweloperów korzystających z platformy .NET magazynu kluczy Azure / biblioteki C#. W hello przejście od wersji hello 1.0 w wersji toohello 2.0, liczba aktualizacji wprowadzono tego będzie wymagać pracy migracji w kodzie aby toobenefit z ulepszeń funkcjonalności hello i funkcji dodatków, takich jak **magazyn kluczy Certyfikaty** obsługuje.

## <a name="key-vault-certificates"></a>Magazyn kluczy certyfikatów

Obsługa certyfikatów usługi Key Vault umożliwia zarządzanie x509 Twojego certyfikaty i hello następujące zachowania:  

* Umożliwia toocreate właściciela certyfikatu certyfikatu za pośrednictwem procesu tworzenia usługi Key Vault lub hello importowania istniejącego certyfikatu. Dotyczy to zarówno z podpisem własnym, a urząd certyfikacji generowane certyfikatów.
* Umożliwia właściciela certyfikatu usługi Key Vault tooimplement bezpieczne przechowywanie i zarządzania X509 certyfikatów bez interakcji z materiału klucza prywatnego.  
* Umożliwia toocreate właściciela certyfikatu zasadę, która określa, że magazyn kluczy toomanage hello cyklu życia certyfikatu.  
* Umożliwia właścicieli certyfikatu tooprovide informacje kontaktowe dla powiadomień dotyczących zdarzeń cyklu życia wygaśnięcia i odnawiania certyfikatów.  
* Obsługuje automatycznego odnawiania z wystawców wybranych - Key Vault partnera X509 certyfikatu dostawców / urzędy certyfikacji.
  
  * Uwaga —-współpracę dostawców/urzędów również są dozwolone, ale nie będzie obsługiwał hello automatycznego odnawiania funkcji.

## <a name="net-support"></a>Obsługa .NET

* **.NET 4.0** nie jest obsługiwana przez wersję hello 2.0 hello .NET usługi Azure Key Vault / biblioteki C#
* **Oprogramowanie .NET core** jest obsługiwana przez wersję hello 2.0 hello .NET usługi Azure Key Vault / biblioteki C#

## <a name="namespaces"></a>Przestrzenie nazw

* Witaj w obszarze nazw **modele** została zmieniona z **Microsoft.Azure.KeyVault** za**Microsoft.Azure.KeyVault.Models**.
* Witaj **Microsoft.Azure.KeyVault.Internal** przestrzeni nazw jest porzucany.
* przestrzeń nazw zależności zestawu Azure SDK Hello zmieniła się z **Hyak.Common** i **Hyak.Common.Internals** za**Microsoft.Rest** i  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Zmiana typu

* *Klucz tajny* zmieniony zbyt*SecretBundle*
* *Słownik* zmieniony zbyt*IDictionary*
* *Lista<T>, string []* zmieniony zbyt*IList<T>*
* *NextList* zmieniony zbyt *NextPageLink*

## <a name="return-types"></a>Zwracane typy

* **KeyList** i **SecretList** zwróci *IPage<T>*  zamiast *ListKeysResponseMessage*
* wygenerowany Hello **BackupKeyAsync** zwróci *BackupKeyResult* zawierającą *wartość* (kopie zapasowe obiektów blob). Przed hello metoda została opakowana i zwracanie tylko wartości hello.

## <a name="exceptions"></a>Wyjątki

* *KeyVaultClientException* zostanie zmieniona zbyt*KeyVaultErrorException*
* Błąd usługi Hello została zmieniona z *wyjątku. Błąd* zbyt*wyjątku. Body.Error.Message*.
* Usunięte informacje dodatkowe z hello komunikat o błędzie dla **[JsonExtensionData]**.

## <a name="constructors"></a>Konstruktory

* Zamiast akceptowanie *HttpClient* jako argument konstruktora akceptuje tylko Konstruktor hello *HttpClientHandler* lub *DelegatingHandler []*.

## <a name="downloaded-packages"></a>Pobranych pakietów

Gdy klient przetwarza zależności na następujących hello Key Vault zostały pobrane

### <a name="previous-package-list"></a>Poprzedniej liście pakietu

* Wersja pakietu id="Hyak.Common" = "1.0.2" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Azure.Common" = "2.0.4" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Azure.Common.Dependencies" = "1.0.0" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Azure.KeyVault" = "1.0.0" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Bcl" = "1.1.9" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Bcl.Async" = "1.0.168" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Bcl.Build" = "1.0.14" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Net.Http" = "2.2.22" targetFramework = "net45"

### <a name="current-package-list"></a>Bieżąca lista pakietów

* Wersja pakietu id="Microsoft.Azure.KeyVault" = "2.0.0-preview" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Rest.ClientRuntime" = "2.2.0" targetFramework = "net45"
* Wersja pakietu id="Microsoft.Rest.ClientRuntime.Azure" = "3.2.0" targetFramework = "net45"

## <a name="class-changes"></a>Klasa zmiany

* **UnixEpoch** klasy został usunięty.
* **Base64UrlConverter** klasy jest zmieniana zbyt**Base64UrlJsonConverter**

## <a name="other-changes"></a>Inne zmiany

* Dodano obsługę dla konfiguracji hello KV zasady ponawiania operacji na błędów przejściowych toothis wersji hello interfejsu API.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* Dla operacji hello, które zwrócił *magazynu*, typ zwracany hello został klasę, która zawiera właściwość magazynu. Witaj zwracany typ jest teraz *magazynu*.
* *PermissionsToKeys* i *PermissionsToSecrets* są teraz *Permissions.Keys* i *Permissions.Secrets*
* Niektóre hello zwracać typów zmiany dotyczą toohello kontroli — płaszczyzna również.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* pakietów Hello jest zbyt podzielony**Microsoft.Azure.KeyVault.Extensions** i **Microsoft.Azure.KeyVault.Cryptography** hello operacji kryptograficznych.

