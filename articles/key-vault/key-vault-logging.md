---
title: aaaAzure rejestrowanie Key Vault | Dokumentacja firmy Microsoft
description: "Użyj tego samouczka toohelp Rozpoczynanie pracy z usługą Azure Key Vault rejestrowania."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Funkcja rejestrowania usługi Azure Key Vault
Usługa Azure Key Vault jest dostępna w większości regionów. Aby uzyskać więcej informacji, zobacz hello [cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Wprowadzenie
Po utworzeniu co najmniej jednego magazynu kluczy, prawdopodobnie będzie toomonitor, jak i kiedy klucz magazyny są używane i przez kogo. W tym celu możesz włączyć funkcję rejestrowania dla usługi Key Vault, która zapisuje informacje na podanym przez Ciebie koncie magazynu platformy Azure. Nowy kontener o nazwie **insights-logs-auditevent** jest tworzony automatycznie dla określonego konta magazynu. Tego samego konta magazynu możesz używać do zbierania dzienników dla wielu magazynów kluczy.

Możesz uzyskać co najwyżej dostęp do informacji rejestrowania, 10 minut po klucz hello wykonanej operacji magazynu. W większości przypadków czas będzie krótszy.  Jest tooyou toomanage dzienniki na koncie magazynu:

* Użyj toosecure metod kontroli dostępu na platformie Azure standardowe dzienniki przez ograniczenie, kto ma dostęp do nich.
* Usuń dzienniki nie są już potrzebne tookeep na koncie magazynu.

Użyj tego samouczka toohelp Rozpoczynanie pracy z usługą Azure Key Vault rejestrowanie toocreate Twojego konta magazynu, włączanie rejestrowania i zinterpretować zebrane informacje rejestrowania hello.  

> [!NOTE]
> Ten samouczek nie zawiera instrukcje dotyczące sposobu toocreate klucza magazynów kluczy i kluczy tajnych. Te informacje można znaleźć w temacie [Rozpoczynanie pracy z usługą Azure Key Vault](key-vault-get-started.md). Instrukcje dotyczące wieloplatformowego interfejsu wiersza polecenia znajdują się w [tym równoważnym samouczku](key-vault-manage-with-cli2.md).
>
> Obecnie nie można skonfigurować usługi Azure Key Vault w hello portalu Azure. Zamiast tego użyj tych instrukcji usługi Azure PowerShell.
>
>

Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka, musi mieć następujące hello:

* Istniejący magazyn kluczy, który był przez Ciebie używany.  
* Usługa Azure PowerShell w **minimalnej wersji 1.0.1**. tooinstall programu Azure PowerShell i skojarzyć go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Jeśli jest już zainstalowany program Azure PowerShell, a nie znasz wersji hello z konsoli programu Azure PowerShell hello, wpisz `(Get-Module azure -ListAvailable).Version`.  
* Wystarczająca ilość miejsca w magazynie platformy Azure dla dzienników usługi Key Vault.

## <a id="connect"></a>Połącz tooyour subskrypcji
Uruchom sesję programu PowerShell Azure i zaloguj się tooyour konto platformy Azure za pomocą następującego polecenia hello:  

    Login-AzureRmAccount

W oknie wyskakującym przeglądarki hello wprowadź nazwę użytkownika konta platformy Azure i hasło. Azure PowerShell pobierze wszystkie subskrypcje hello, które są skojarzone z tym kontem i domyślnie, używa hello pierwsza z nich.

Jeśli masz wiele subskrypcji może być toospecify konkretne konto, które były używane toocreate magazyn kluczy Azure. Wpisz powitania po toosee hello subskrypcje dla swojego konta:

    Get-AzureRmSubscription

Następnie toospecify hello subskrypcję skojarzoną z Twoim magazynem kluczy, który będziesz rejestrować, wpisz:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> To jest ważny krok, szczególnie przydatny, jeśli masz wiele subskrypcji skojarzonych z Twoim kontem. Jeśli ten krok zostanie pominięty, może zostać wyświetlony błąd tooregister elemencie Microsoft.Insights.
>   
>

Aby uzyskać więcej informacji na temat konfigurowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Tworzenie nowego konta magazynu dla dzienników
Mimo że można użyć istniejącego konta magazynu dla dzienników, utworzymy nowe konto magazynu, który ma być dedykowane tooKey dzienniki magazynu. Dla wygody gdy mamy toospecify to później, szczegóły hello będzie są przechowywane w zmiennej o nazwie **sa**.

W celu ułatwienia zarządzania użyjemy hello tej samej grupie zasobów, jak Witaj, który zawiera nasz magazyn kluczy. Z hello [Wprowadzenie — samouczek](key-vault-get-started.md), nosi nazwę tej grupy zasobów **ContosoResourceGroup** będziemy lokalizacji Azja Wschodnia hello toouse. Zastąp te wartości własnymi, w razie potrzeby:

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Jeśli zdecydujesz się toouse istniejącego konta magazynu, należy użyć hello tej samej subskrypcji, jako magazynu kluczy i użyj modelu wdrażania usługi Resource Manager hello zamiast hello klasycznego modelu wdrożenia.
>
>

## <a id="identify"></a>Zidentyfikuj hello magazynu kluczy dla dzienników
W naszym samouczku naszych magazyn kluczy został **ContosoKeyVault**, dlatego dalej będziemy toouse nazwy i przechowuj szczegóły hello do zmiennej o nazwie **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Włączanie rejestrowania
tooenable rejestrowanie dla usługi Key Vault użyjemy polecenia cmdlet Set-AzureRmDiagnosticSetting hello, wraz z zmienne hello utworzyliśmy dla naszego nowego konta magazynu i magazynu kluczy. Zaplanujemy też hello **-włączone** Flaga zbyt**$true** i tooAuditEvent kategorii hello (hello jedyna kategoria rejestrowania usługi Key Vault), ustaw:

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

Witaj dane wyjściowe obejmują:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Potwierdza to, że włączono rejestrowanie dla magazynu kluczy i zapisywania konta magazynu tooyour informacji.

Opcjonalnie można także ustawić zasady przechowywania dla dzienników tak, aby starsze dzienniki były automatycznie usuwane. Na przykład ustawić zasady przechowywania, używając **- RetentionEnabled** Flaga zbyt**$true** i ustaw **- RetentionInDays** parametru zbyt**90** tak czy zostaną automatycznie usunięte dzienniki starsze niż 90 dni.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

Co jest rejestrowane:

* Wszystkie uwierzytelnione żądania interfejsu API REST są rejestrowane, w tym żądania zakończone niepowodzeniem z powodu uprawnień dostępu, błędów systemu lub błędów w żądaniach.
* Operacje na powitania klucza magazynu siebie, łącznie z tworzeniem, usuwaniem, ustawiania zasad dostępu do magazynu kluczy, i aktualizowaniem atrybutów magazynu kluczy, takich jak tagi.
* Operacje na kluczach i kluczach tajnych w magazynie kluczy hello, w tym tworzenie, modyfikowanie lub usuwanie tych kluczy lub kluczy tajnych; operacje, takie jak podpisywanie, sprawdź, szyfrowania, odszyfrowywania, zawijać i odpakowywanie kluczy, pobieranie kluczy tajnych, listy kluczy i kluczy tajnych i ich wersje.
* Nieuwierzytelnione żądania, które powodują uzyskanie odpowiedzi 401. Na przykład żądania, które nie mają tokenu elementu nośnego, są nieprawidłowo sformułowane, wygasły lub mają nieprawidłowy token.  

## <a id="access"></a>Uzyskiwanie dostępu do dzienników
Dzienniki magazynu kluczy są przechowywane w hello **insights-logs-auditevent** kontenera na koncie magazynu hello podane. toolist wszystkie hello obiekty BLOB w tym kontenerze, wpisz:

Najpierw Utwórz zmienną hello nazwa kontenera. Będą to używane w hello reszty hello krokach związanych z.

    $container = 'insights-logs-auditevent'

toolist wszystkie hello obiekty BLOB w tym kontenerze, wpisz:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
Hello dane wyjściowe będą wyglądać coś podobnego toothis:

**Identyfikator URI kontenera: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Nazwa**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Jak widać w przedstawionych danych wyjściowych, obiekty BLOB hello zgodne z konwencją nazewnictwa: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

Witaj wartości daty i godziny używają czasu UTC.

Ponieważ hello tego samego konta magazynu mogą być używane toocollect dzienników dla wielu zasobów, hello pełny identyfikator zasobu w nazwie obiektu blob hello jest bardzo przydatne tooaccess lub obiekty BLOB hello tylko pobierania, które należy. Jednak zanim do tego, firma Microsoft, najpierw zostanie omówiony sposób toodownload hello wszystkie obiekty BLOB.

Najpierw utwórz hello toodownload folderu obiektów blob. Na przykład:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Następnie uzyskaj listę wszystkich obiektów blob:  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Przekaż w potoku tej listy za pośrednictwem obiektów blob hello toodownload "Get-AzureStorageBlobContent" do folderu docelowego:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Po uruchomieniu tego drugiego polecenia hello  **/**  ogranicznik w nazwach obiektów blob hello Utwórz pełną strukturę folderów w folderze docelowym hello, a ta struktura będzie używana toodownload i zapisać hello obiekty BLOB jako plików.

tooselectively pobierać obiekty BLOB, użyj symboli wieloznacznych. Na przykład:

* Jeśli masz wiele magazynów kluczy i chcesz toodownload dzienniki dla tylko jednego magazynu kluczy o nazwie CONTOSOKEYVAULT3:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Jeśli masz wiele grup zasobów i chcesz toodownload dzienniki dla tylko jednej grupy zasobów, użyj `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Jeśli chcesz toodownload wszystkie dzienniki hello hello miesiącu stycznia 2016, użyj `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Wszystko jest teraz gotowy toostart wyszukiwanie informacji zawartych w hello dzienników. Jednak zanim który dwoma parametrami polecenia Get-AzureRmDiagnosticSetting trzeba tooknow:

* tooquery hello stan ustawień diagnostycznych dla zasobu magazynu kluczy:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* Rejestrowanie toodisable dla zasobu magazynu kluczy:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Interpretowanie dzienników usługi Key Vault
Poszczególne obiekty blob są przechowywane jako tekst w formacie obiektu blob JSON. To jest przykładowy wpis dziennika po uruchomieniu polecenia `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Witaj poniższej tabeli wymieniono nazwy pól hello wraz z opisami.

| Nazwa pola | Opis |
| --- | --- |
| time |Data i godzina (UTC). |
| resourceId |Identyfikator zasobu usługi Azure Resource Manager W przypadku dzienników usługi Key Vault jest zawsze identyfikator zasobu usługi Key Vault hello |
| operationName |Nazwa operacji hello, zgodnie z opisem w następnej tabeli hello. |
| operationVersion |To jest wersja interfejsu API REST hello zażądał powitania klienta. |
| category |W przypadku dzienników usługi Key Vault kategoria AuditEvent jest hello jedyną dostępną wartością. |
| resultType |Wynik żądania interfejsu API REST. |
| resultSignature |Stan HTTP. |
| resultDescription |Dodatkowy opis wyniku hello, jeśli jest dostępna. |
| durationMs |Czas trwania żądania interfejsu API REST hello tooservice, w milisekundach. Nie obejmuje opóźnienia sieci hello, więc czas zmierzony po stronie klienta hello hello mogą być niezgodne z tym razem. |
| callerIpAddress |Adres IP powitania klienta, który wysłał żądanie hello. |
| correlationId |Opcjonalny identyfikator GUID hello klienta można przekazać toocorrelate dzienników po stronie klienta z dziennikami po stronie usługi (Key Vault). |
| identity |Tożsamość z tokenu hello, który został przedstawiony podczas przesyłania żądania interfejsu API REST hello. Jest to zazwyczaj „użytkownik”, „główna nazwa usługi” lub kombinacja „użytkownik+identyfikator appId”, jak w przypadku żądania wynikającego z polecenia cmdlet usługi Azure PowerShell. |
| properties |To pole zawiera różne informacje oparte na powitania operacji (operationName). W większości przypadków zawiera informacje o kliencie (hello ciąg agenta użytkownika przekazany przez powitania klienta), hello dokładny identyfikator URI żądania interfejsu API REST i kod stanu HTTP. Ponadto gdy obiekt jest zwracany w wyniku żądania (na przykład KeyCreate lub VaultGet) będzie również zawierać hello identyfikator URI klucza (jako "id"), identyfikator URI magazynu lub identyfikator URI klucza tajnego. |

Witaj **operationName** wartości pól są w formacie ObjectVerb. Na przykład:

* Wszystkie operacje magazynu kluczy mają hello "magazynu`<action>`" formatu, takiego jak `VaultGet` i `VaultCreate`.
* Wszystkie operacje kluczy mają hello "klucz`<action>`" formatu, takiego jak `KeySign` i `KeyList`.
* Wszystkie operacje kluczy tajnych mają hello "klucz tajny`<action>`" formatu, takiego jak `SecretGet` i `SecretListVersions`.

Witaj w poniższej tabeli wymieniono hello operationName i odpowiadające jej polecenie interfejsu API REST.

| operationName | Polecenie interfejsu API REST |
| --- | --- |
| Authentication |Za pośrednictwem punktu końcowego usługi Azure Active Directory |
| VaultGet |[Pobierz informacje o magazynie kluczy](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Utwórz lub zaktualizuj magazyn kluczy](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Usuń magazyn kluczy](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Zaktualizuj magazyn kluczy](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Utwórz listę wszystkich magazynów kluczy w grupie zasobów](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Utwórz klucz](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Pobierz informacje o kluczu](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Importuj klucz do magazynu](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Wykonaj kopię zapasową klucza](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[Usuń klucz](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Przywróć klucz](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Podpisz przy użyciu klucza](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Weryfikuj za pomocą klucza](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Opakuj klucz](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Odpakuj klucz](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Szyfruj za pomocą klucza](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Odszyfruj za pomocą klucza](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Zaktualizuj klucz](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Lista hello kluczy w magazynie](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Utwórz listę wersji klucza hello](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Utwórz klucz tajny](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Pobierz klucz tajny](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Zaktualizuj klucz tajny](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Usuń klucz tajny](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Utwórz listę kluczy tajnych w magazynie](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Utwórz listę wersji klucza tajnego](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Korzystanie z usługi Log Analytics

Za pomocą rozwiązania Azure Key Vault hello w tooreview analizy dzienników, dzienniki usługi Azure Key Vault AuditEvent. Aby uzyskać więcej informacji, łącznie ze sposobem tooset to, zobacz [rozwiązania magazynu kluczy Azure Log Analytics](../log-analytics/log-analytics-azure-key-vault.md). Ten artykuł zawiera również instrukcje, jeśli potrzebujesz toomigrate z hello starego magazynu kluczy rozwiązania udostępniona hello analizy dzienników wersji zapoznawczej, którym najpierw kierowane tooan Twojego dzienniki konta magazynu Azure i skonfigurować tooread analizy dzienników z tego miejsca.

## <a id="next"></a>Następne kroki
Aby zapoznać się z samouczkiem, w którym użyto usługi Azure Key Vault w aplikacji sieci Web, zobacz [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md) (Używanie usługi Azure Key Vault za pośrednictwem aplikacji sieci Web).

Odwołania dotyczące programowania, zobacz [hello przewodnik dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).

Aby zapoznać się z listą poleceń cmdlet usługi Azure PowerShell 1.0 dla usługi Azure Key Vault, zobacz artykuł [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Polecenia cmdlet w usłudze Azure Key Vault).

Samouczek dotyczący rotacją kluczy i dziennika inspekcji w usłudze Azure Key Vault, zobacz [jak toosetup Key Vault z tooend zakończenia klucza obracanie i inspekcji](key-vault-key-rotation-log-monitoring.md).
