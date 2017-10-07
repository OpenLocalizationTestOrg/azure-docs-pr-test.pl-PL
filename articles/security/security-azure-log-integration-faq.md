---
title: "aaaAzure dziennika integracji — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule odpowiedzi na pytania dotyczące integracji dziennika Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a>Integracja dzienników Azure — często zadawane pytania
Ten artykuł zawiera odpowiedzi na często zadawane pytania (FAQ) dotyczące integracji dziennika Azure. 

Integracja dziennika Azure to usługa systemu operacyjnego Windows czy można użyć toointegrate raw dzienników z zasobów platformy Azure w sieci lokalnej zabezpieczeń informacji i zdarzenia (SIEM) systemów zarządzania. Integracja ta zapewnia jednolity pulpit nawigacyjny dla wszystkich zasobów, lokalnie lub w chmurze hello. Możesz agregować, skorelowania, analizowanie i alertów zdarzeń zabezpieczeń skojarzonych z aplikacjami.

## <a name="is-hello-azure-log-integration-software-free"></a>Zwolnieniu hello Azure dziennika integracji oprogramowania?
Tak. Brak bezpłatne hello Azure dziennika integracji oprogramowania.

## <a name="where-is-azure-log-integration-available"></a>Gdzie jest integracja dziennika Azure?

Jest obecnie dostępna w Azure handlowych i Azure dla instytucji rządowych i nie jest dostępny w Chinach lub Niemczech.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Jak można wyświetlić hello kont magazynu, z których integracji dziennika Azure jest ściąganie dzienniki maszyny Wirtualnej platformy Azure?
Uruchom polecenie hello **listy źródeł azlog**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>Jak sprawdzić, które subskrypcji hello Azure integracji dziennika są dzienniki z?

W przypadku hello dzienników inspekcji, które są umieszczone w hello **AzureResourcemanagerJson** katalogów, identyfikator subskrypcji hello jest nazwa pliku dziennika hello. Dotyczy to również dzienniki w hello **AzureSecurityCenterJson** folderu. Na przykład:

20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**JSON

Dzienniki inspekcji w usłudze Azure Active Directory obejmować identyfikator dzierżawy hello jako część nazwy hello.

Dzienniki diagnostyczne, które są odczytywane z Centrum zdarzeń nie ma identyfikator subskrypcji hello jako część nazwy hello. Zamiast tego zawierają hello przyjazną nazwę określony jako część hello utworzeniu źródła Centrum zdarzeń hello. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Jak można zaktualizować konfiguracji serwera proxy hello?
Jeśli ustawienie serwera proxy nie zezwalają na dostęp do magazynu Azure bezpośrednio, otwórz hello **AZLOG. WYWOŁANIE PLIKU EXE. CONFIG** w pliku **c:\Program Files\Microsoft Azure dziennika integracji**. Aktualizacja hello pliku tooinclude hello **defaultProxy —** sekcji o adresie serwera proxy hello Twojej organizacji. Po ukończeniu aktualizacji hello, zatrzymać i uruchomić usługę hello za pomocą poleceń hello **azlog net stop** i **net start azlog**.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>Jak można wyświetlić informacji o subskrypcji hello w zdarzeń systemu Windows?
Dołącz hello subskrypcji identyfikator toohello przyjaznej nazwy podczas dodawania źródła hello:

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
Zdarzenie Hello XML ma powitania po metadanych, w tym hello identyfikator subskrypcji:

![Zdarzenie XML][1]

## <a name="error-messages"></a>Komunikaty o błędach
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Po uruchomieniu polecenia hello **azlog createazureid**, dlaczego uzyskać hello następujący błąd?
Błąd:

  *Nie powiodło się toocreate aplikacji AAD - dzierżawy 72f988bf-86f1-41af-91ab-2d7cd011db37 - Przyczyna = "Zabronione" - komunikat = "Operacja hello toocomplete niewystarczające uprawnienia".*

Witaj **azlog createazureid** polecenie podejmuje toocreate nazwy głównej usługi w wszystkich dzierżaw hello Azure AD dla subskrypcji hello, które hello Azure logowania ma dostęp. Jeśli logowanie w usłudze Azure jest tylko użytkownik-Gość w tej dzierżawie usługi Azure AD, hello polecenia nie powiodło się "Operacja hello toocomplete niewystarczające uprawnienia". Poproś administratora tooadd dzierżawy hello Twojego konta jako użytkownik w dzierżawie powitalnych.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Po uruchomieniu polecenia hello **azlog autoryzować**, dlaczego uzyskać hello następujący błąd?
Błąd:

  *Ostrzeżenie tworzenia przypisania roli - AuthorizationFailed: powitania klienta janedo@microsoft.com"z obiektem id"fe9e03e4-4dad-4328-910f-fd24a9660bd2"nie ma autoryzacji tooperform akcji"Microsoft.Authorization/roleAssignments/write"w zakresie" / Subskrypcje / 70d 95299-d689-4c 97-b971-0d8ff0000000 ".*

Hello **autoryzować azlog** polecenia przypisuje hello roli nazwy głównej usługi Azure AD toohello czytnika (utworzone za pomocą **azlog createazureid**) toohello podane subskrypcji. Jeśli hello Azure logowania nie jest administratora współpracującego lub właściciela subskrypcji hello, jego kończy się niepowodzeniem z komunikatem o błędzie "Autoryzacja nie powiodła się.". Azure opartej na rolach kontroli dostępu (RBAC) administratora współpracującego lub właściciela jest wymagane toocomplete tej akcji.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Gdzie mogę znaleźć hello definicji właściwości hello w dzienniku inspekcji hello?
Zobacz:

* [Operacje inspekcji z usługi Azure Resource Manager](../azure-resource-manager/resource-group-audit.md)
* [Lista zdarzeń zarządzania hello w ramach subskrypcji w hello interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Gdzie znaleźć szczegółowe informacje o alertach Centrum zabezpieczeń Azure
Zobacz [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>Jak zmodyfikować, jakie informacje są zbierane z diagnostyki maszyny Wirtualnej?
Szczegółowe informacje w sposób tooget, modyfikować i konfiguracji hello diagnostyki Azure, możesz znaleźć [tooenable Użyj programu PowerShell diagnostyki Azure na maszynie wirtualnej z systemem Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Poniższy przykład Hello pobiera konfigurację diagnostyki Azure hello:

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

Poniższy przykład Hello modyfikuje hello Azure Diagnostics konfigurację. W tej konfiguracji tylko zdarzeń 4624 identyfikator i identyfikator 4625 są zbierane z dziennika zdarzeń zabezpieczeń hello. Antimalware Microsoft Azure zdarzenia są zbierane z hello w dzienniku zdarzeń systemowych. Aby uzyskać szczegółowe informacje z użyciem wyrażenia XPath hello, zobacz [wykorzystywanie zdarzenia](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Witaj poniższy przykład przedstawia hello Azure Diagnostics konfiguracji:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

Po wprowadzeniu zmian Sprawdź tooensure konta magazynu hello tego hello poprawny są zbierane zdarzenia.

Jeśli masz problemy podczas hello instalacji i konfiguracji, otwórz [żądania obsługi](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Wybierz **integracji dziennika** jako usługa hello żądania pomocy technicznej.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>Dzienniki obserwatora sieciowego toointegrate integracji dziennika Azure można używać do mojego SIEM?

Azure obserwatora sieciowego generuje duże ilości danych rejestrowania. Dzienniki te nie są przeznaczone toobe wysyłane tooa SIEM. miejsce docelowe Hello obsługiwane tylko dla dzienników obserwatora sieciowego jest konto magazynu. Integracja z usługą Azure dziennika nie obsługuje odczytywania te dzienniki i udostępnia je tooa dostępne rozwiązania SIEM.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
