---
title: "aaaAzure rozwiązania analizy dzienników usługi Key Vault | Dokumentacja firmy Microsoft"
description: "Za pomocą rozwiązania Azure Key Vault hello w tooreview analizy dzienników, dzienniki usługi Azure Key Vault."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Azure Key Vault Analytics rozwiązania analizy dzienników

![Symbol magazyn kluczy](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

Za pomocą rozwiązania Azure Key Vault hello w tooreview analizy dzienników, dzienniki usługi Azure Key Vault AuditEvent.

toouse hello rozwiązanie, należy tooenable rejestrowanie usługi Azure Key Vault diagnostyki i bezpośredniego hello obszaru roboczego analizy dzienników tooa dla diagnostyki. Nie jest magazynu obiektów Blob tooAzure niezbędne toowrite hello dzienników.

> [!NOTE]
> W stycznia 2017 r. hello obsługiwane wysyłać dzienniki z tooLog Key Vault, zmienić Analytics. Jeśli używasz hello Key Vault rozwiązanie zawiera *(przestarzałe)* w tytule hello odwoływać się za[migrowania hello starego magazynu kluczy rozwiązania](#migrating-from-the-old-key-vault-solution) czynności należy toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj hello następujące instrukcje tooinstall i skonfiguruj rozwiązanie usługi Azure Key Vault hello:

1. Włącz hello Azure Key Vault rozwiązania z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. Włącz diagnostykę rejestrowania toomonitor zasobów usługi Key Vault hello, używając albo hello [portal](#enable-key-vault-diagnostics-in-the-portal) lub [programu PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Włącz diagnostykę Key Vault w portalu hello

1. W hello portalu Azure Przejdź toomonitor zasobu usługi Key Vault toohello
2. Wybierz *dzienników diagnostycznych* hello tooopen po stronie

   ![obrazów kafelków usługi Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Kliknij przycisk *Włącz diagnostykę* hello tooopen po stronie

   ![obrazów kafelków usługi Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. Kliknij tooturn diagnostykę, *na* w obszarze *stanu*
5. Kliknij przycisk wyboru hello *wysyłania tooLog analityka*
6. Wybierz istniejący obszar roboczy analizy dzienników lub tworzenie obszaru roboczego
7. tooenable *AuditEvent* dzienniki, kliknij pole wyboru hello dziennika
8. Kliknij przycisk *zapisać* tooenable hello rejestrowania diagnostyki tooLog analityka

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Włącz diagnostykę Key Vault przy użyciu programu PowerShell
Witaj następującego skryptu programu PowerShell zawiera przykładowy sposób toouse `Set-AzureRmDiagnosticSetting` tooenable diagnostyczne dla usługi Key Vault:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Przejrzyj szczegóły zbierania danych usługi Azure Key Vault
Azure Key Vault rozwiązania służy do zbierania dzienników diagnostycznych bezpośrednio z hello Key Vault.
Nie jest konieczne toowrite hello dzienniki tooAzure magazynu obiektów Blob i agent nie jest wymagany do zbierania danych.

Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o sposobie dane są zbierane dla usługi Azure Key Vault.

| Platforma | Bezpośrednie agenta | Agent menedżera operacji centrum systemów | Azure | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość zbierania |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | po przybyciu |

## <a name="use-azure-key-vault"></a>Korzystanie z rozwiązania Azure Key Vault
Po [zainstalować rozwiązanie hello](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), przeglądać dane usługi Key Vault hello klikając hello **usługi Azure Key Vault** Kafelek z hello **omówienie** strony analizy dzienników.

![obrazów kafelków usługi Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Po kliknięciu hello **omówienie** kafelka, można wyświetlić podsumowania dzienników, a następnie Drąż w toodetails dla hello następujące kategorie:

* Wolumin wszystkie operacje magazynu kluczy w czasie
* Nie powiodła się operacja woluminów wraz z upływem czasu
* Średni czas oczekiwania operacyjnej, przez operację
* Jakość usług dla operacji o hello liczba operacji, które przyjmują więcej niż 1000 ms oraz listę działań, które przyjmują więcej niż 1000 ms

![Obraz pulpitu nawigacyjnego usługi Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Obraz pulpitu nawigacyjnego usługi Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>Szczegóły tooview do żadnej operacji
1. Na powitania **omówienie** kliknij przycisk hello **usługi Azure Key Vault** kafelka.
2. Na powitania **usługi Azure Key Vault** pulpitu nawigacyjnego, przejrzyj hello informacje podsumowania w jednym z bloków hello, a następnie kliknij jedną tooview szczegółowe informacje o nim w hello dziennik wyszukiwania strony.

    Na wszystkich stronach wyszukiwania dziennika hello można wyświetlić wyniki według czasu, szczegółowe wyniki i historię dziennik wyszukiwania. Można również filtrować według aspekty toonarrow hello wyników.

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
Witaj rozwiązania Azure Key Vault analizuje rekordów, które mają typ **KeyVaults** które są zbierane z [dzienniki AuditEvent](../key-vault/key-vault-logging.md) w diagnostyce Azure.  Właściwości te rekordy są hello w poniższej tabeli:  

| Właściwość | Opis |
|:--- |:--- |
| Typ |*AzureDiagnostics* |
| SourceSystem |*Azure* |
| CallerIpAddress |Adres IP klienta hello, który wysłał żądanie hello |
| Kategoria | *AuditEvent* |
| CorrelationId |Opcjonalny identyfikator GUID hello klienta można przekazać toocorrelate dzienników po stronie klienta z dziennikami po stronie usługi (Key Vault). |
| DurationMs |Czas trwania żądania interfejsu API REST hello tooservice, w milisekundach. Tym razem nie obejmuje opóźnienia sieci, więc czas zmierzony po stronie klienta hello hello mogą być niezgodne z tym razem. |
| httpStatusCode_d |Zwrócony przez Żądanie hello kod stanu HTTP (na przykład *200*) |
| id_s |Unikatowy identyfikator żądania hello |
| identity_claim_appid_g | Identyfikator GUID dla identyfikatora aplikacji hello |
| OperationName |Nazwa operacji hello, zgodnie z opisem w [rejestrowanie usługi Azure Key Vault](../key-vault/key-vault-logging.md) |
| OperationVersion |Wersja interfejsu API REST zażądał powitania klienta (na przykład *2015-06-01*) |
| requestUri_s |Identyfikator URI żądania hello |
| Zasób |Nazwa magazynu kluczy hello |
| ResourceGroup |Grupa zasobów hello magazyn kluczy |
| Identyfikator zasobu |Identyfikator zasobu usługi Azure Resource Manager W przypadku dzienników usługi Key Vault jest hello Key Vault z identyfikatorem zasobu. |
| ResourceProvider |*FIRMY MICROSOFT. KEYVAULT* |
| ResourceType | *MAGAZYNÓW* |
| ResultSignature |Stan HTTP (na przykład *OK*) |
| Typ ResultType |Wynik żądania interfejsu API REST (na przykład *Powodzenie*) |
| SubscriptionId |Identyfikator subskrypcji Azure subskrypcji hello zawierający hello magazyn kluczy |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Migracja z rozwiązania do hello starego magazynu kluczy
W stycznia 2017 r. hello obsługiwane wysyłać dzienniki z tooLog Key Vault, zmienić Analytics. Te zmiany zapewniają hello następujące korzyści:
+ Dzienniki są zapisywane bezpośrednio tooLog Analytics bez hello muszą toouse konta magazynu
+ Mniejsze opóźnienia od czasu hello, kiedy są dzienniki generowane toothem dostępne w analizy dzienników
+ Mniejszej liczby kroków konfiguracji
+ Format wspólne dla wszystkich typów Diagnostyka Azure

Witaj toouse zaktualizowane rozwiązania:

1. [Skonfiguruj toobe diagnostyki wysyłane bezpośrednio tooLog Analytics z magazynu kluczy](#enable-key-vault-diagnostics-in-the-portal)  
2. Włącz rozwiązanie usługi Azure Key Vault hello przy użyciu hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md)
3. Wszystkie zapisane kwerendy, pulpity nawigacyjne lub alerty toouse hello nowy typ danych
  + Typ jest zmiana z: KeyVaults tooAzureDiagnostics. Możesz użyć hello ResourceType toofilter tooKey dzienniki magazynu.
  - Zamiast: `Type=KeyVaults`, użyj`Type=AzureDiagnostics ResourceType=VAULTS`
  + Pola: (nazwy pól jest rozróżniana wielkość liter)
  - Dla dowolnego pola, które sufiks \_s, \_d, lub \_g w nazwie hello, zmień hello pierwszy znak toolower przypadku
  - Dla dowolnego pola, które sufiks \_o w polu Nazwa danych hello jest podzielony na poszczególnych pól na podstawie nazw pól hello zagnieżdżone. Na przykład hello UPN wywołującego hello jest przechowywany w polu`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - TooCallerIPAddress CallerIpAddress pola zmienione
   - Pole RemoteIPCountry nie jest już obecne
4. Usuń hello *analityka magazynu kluczy (przestarzały)* rozwiązania. Jeśli używasz programu PowerShell, użyj`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

Dane zbierane przed hello zmiany nie jest widoczna w hello nowego rozwiązania. Możesz kontynuować tooquery dla tego danych przy użyciu hello stary typ i nazwy pola.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Następne kroki
* Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane usługi Azure Key Vault.
