---
title: "aaaEnable Podłączanie pulpitu zdalnego dla roli w usług Azure Cloud Services przy użyciu programu PowerShell"
description: "Jak tooconfigure platformy azure w chmurze usługi aplikacji przy użyciu programu PowerShell tooallow obsługi połączeń pulpitu zdalnego"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Włącz połączenia pulpitu zdalnego dla roli w usług Azure Cloud Services przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Program Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Pulpit zdalny umożliwia pulpitu hello tooaccess roli działające na platformie Azure. Można użyć tootroubleshoot połączenia pulpitu zdalnego i diagnozowanie problemów z aplikacją, jest uruchomiona.

W tym artykule opisano sposób tooenable pulpitu zdalnego na role usługi w chmurze przy użyciu programu PowerShell. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello wymagania wstępne wymagane dla tego artykułu. PowerShell korzysta hello rozszerzenia usług pulpitu zdalnego, więc można włączyć pulpitu zdalnego, po wdrożeniu aplikacji hello.

## <a name="configure-remote-desktop-from-powershell"></a>Konfigurowanie pulpitu zdalnego z programu PowerShell
Witaj [AzureServiceRemoteDesktopExtension zestaw](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenie cmdlet pozwala tooenable pulpitu zdalnego na określone role lub wszystkie role tego wdrożenia usługi chmury. polecenia cmdlet Hello pozwala określić hello nazwy użytkownika i hasła dla hello użytkownika pulpitu zdalnego za pośrednictwem hello *poświadczeń* parametr, który akceptuje obiektu PSCredential.

Jeśli używasz programu PowerShell interaktywnego, łatwo można ustawić obiektu PSCredential hello przez wywołanie hello [poświadczenia Get](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.

```
$remoteusercredentials = Get-Credential
```

To polecenie wyświetla okno dialogowe, dzięki czemu możesz tooenter hello username i hasło dla użytkownika zdalnego hello w bezpieczny sposób.

Ponieważ PowerShell pomaga w scenariuszach automatyzacji, można również skonfigurować hello **PSCredential** obiektu w taki sposób, który nie wymaga interakcji z użytkownikiem. Najpierw należy tooset bezpieczne hasło. Rozpoczynać się od określenia hasła w postaci zwykłego tekstu przekonwertować ciągu bezpiecznego tooa przy użyciu [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). Następnie tooconvert parametry te będą potrzebne bezpieczny do za pomocą zaszyfrowanego ciągu standardowego [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx). Teraz możesz zapisać ten zaszyfrowanego ciągu standardowego tooa plików przy użyciu [zestawu zawartości](https://technet.microsoft.com/library/ee176959.aspx).

Można także utworzyć plik bezpieczne hasło, dzięki czemu nie trzeba tootype w haśle hello zawsze. Ponadto plik bezpieczne hasło jest lepszym rozwiązaniem niż zwykły plik tekstowy. Użyj hello następującego środowiska PowerShell toocreate pliku bezpieczne hasło:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Przy ustawianiu hasła hello, upewnij się, że spełniają hello [wymagania dotyczące złożoności](https://technet.microsoft.com/library/cc786468.aspx).
>
>

toocreate hello obiektu poświadczenia z hello pliku bezpieczne hasło, należy odczytać zawartości pliku hello i przekonwertować je wstecz tooa bezpieczny ciąg za pomocą [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Witaj [AzureServiceRemoteDesktopExtension zestaw](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenia cmdlet również akceptuje *wygaśnięcia* parametr, który określa **DateTime** użytkownika hello wygaśnięciem konta. Na przykład można ustawić tooexpire konta hello za kilka dni od hello bieżącą datę i godzinę.

W tym przykładzie programu PowerShell pokazuje, jak tooset hello rozszerzenia usług pulpitu zdalnego na usługi w chmurze:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
Można również opcjonalnie określić hello miejsce wdrożenia i role, które mają tooenable pulpitu zdalnego na. Jeśli nie podano tych parametrów, polecenia cmdlet hello umożliwia pulpitu zdalnego na wszystkich ról w hello **produkcji** miejsca wdrożenia.

Witaj rozszerzenia usług pulpitu zdalnego jest powiązane z wdrożeniem. Jeśli utworzysz nowe wdrożenie usługi hello masz tooenable pulpitu zdalnego w tym wdrożeniu. Zawsze należy toohave pulpitu zdalnego włączyć następnie należy rozważyć włączenie hello skryptów programu PowerShell do przepływu pracy wdrażania.

## <a name="remote-desktop-into-a-role-instance"></a>Pulpit zdalny do wystąpienia roli
Witaj [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) polecenia cmdlet jest używane tooremote pulpitu do konkretnej roli wystąpienie usługi w chmurze. Można użyć hello *LocalPath* hello toodownload parametru RDP plików lokalnie. Możesz użyć hello *uruchamianie* parametru toodirectly uruchamiania hello Podłączanie pulpitu zdalnego w oknie dialogowym tooaccess hello wystąpienia roli usługi w chmurze.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Sprawdź, czy rozszerzenie Pulpit zdalny jest włączony w usłudze
Witaj [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) polecenie cmdlet wyświetla który pulpitu zdalnego jest włączone lub wyłączone w ramach wdrożenia usługi. polecenie cmdlet Hello zwraca username hello hello użytkownika pulpitu zdalnego i hello ról, które rozszerzenia usług pulpitu zdalnego hello jest włączone dla. Domyślnie dzieje się tak na powitania miejsce wdrożenia i hello toouse przemieszczania miejsca zamiast tego można wybrać.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Usuń rozszerzenie Pulpit zdalny z usługą
Jeśli została już włączona hello rozszerzenia usług pulpitu zdalnego w ramach wdrożenia i wymagają tooupdate hello ustawienia pulpitu zdalnego, należy najpierw usunąć hello rozszerzenia. I włącz ją ponownie przy hello nowych ustawień. Na przykład jeśli chcesz, aby tooset nowe hasło dla konta użytkownika zdalnego hello, lub konta hello wygasł. W ten sposób jest wymagany dla istniejącego wdrożenia, których hello zdalnego pulpitu rozszerzenie. W przypadku nowych wdrożeń można po prostu zastosować rozszerzenia hello bezpośrednio.

tooremove hello zdalnego pulpitu rozszerzenie z wdrożenia hello, można użyć hello [AzureServiceRemoteDesktopExtension Usuń](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenia cmdlet. Opcjonalnie można określić miejsce wdrożenia hello i roli, z którego mają rozszerzenia usług pulpitu zdalnego hello tooremove.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> Konfiguracja rozszerzenia hello Usuń toocompletely, należy wywołać hello *Usuń* polecenia cmdlet z hello **UninstallConfiguration** parametru.
>
> Witaj **UninstallConfiguration** parametru odinstalowuje żadnej konfiguracji rozszerzenia czyli zastosowane toohello usługi. Konfiguracja każdego rozszerzenia jest skojarzona z konfiguracją usługi hello. Wywoływanie hello *Usuń* polecenia cmdlet bez **UninstallConfiguration** Usuwa skojarzenia hello <mark>wdrożenia</mark> hello rozszerzenia konfiguracji, co powoduje wykluczenie rozszerzenie Hello. Jednak konfiguracja rozszerzenia hello pozostaje skojarzony z usługą hello.
>
>

## <a name="additional-resources"></a>Dodatkowe zasoby

[Jak usługi w chmurze tooConfigure](cloud-services-how-to-configure.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)
