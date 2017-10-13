---
title: "Rozwiązywanie problemów z ustawienia lokalnego klastra usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano zestaw sugestie dotyczące rozwiązywania problemów z lokalnego klastra projektowego"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Rozwiązywanie problemów z konfiguracji klastra lokalnego rozwoju
Jeśli napotkasz problem podczas interakcji z lokalnym klastrem programowanie sieć szkieletowa usług Azure, przejrzyj poniższe sugestie potencjalnych rozwiązań.

## <a name="cluster-setup-failures"></a>Błędy instalacji klastra
### <a name="cannot-clean-up-service-fabric-logs"></a>Nie można wyczyścić dzienniki sieci szkieletowej usług
#### <a name="problem"></a>Problem
Podczas uruchamiania skryptu DevClusterSetup, zostanie wyświetlony błąd w następujący sposób:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Rozwiązanie
Zamknij bieżące okno programu PowerShell i otworzyć nowe okno programu PowerShell jako administrator. Teraz można pomyślnie uruchomić skryptu.

## <a name="cluster-connection-failures"></a>Liczba błędów połączenia klastra
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Polecenia cmdlet programu PowerShell usługi Service Fabric nie są rozpoznawane w programie Azure PowerShell
#### <a name="problem"></a>Problem
Jeśli zostanie podjęta próba uruchomienia dowolnych poleceniach cmdlet programu PowerShell usługi Service Fabric, takich jak `Connect-ServiceFabricCluster` w oknie programu PowerShell usługi Azure jej nie powiedzie się, informujący o tym, że polecenie cmdlet nie została rozpoznana. Przyczyną jest używany 32-bitowej wersji środowiska Windows PowerShell (nawet na 64-bitowe wersje systemu operacyjnego), programu Azure PowerShell poleceń cmdlet usługi sieć szkieletowa tylko pracy w środowiskach 64-bitowych.

#### <a name="solution"></a>Rozwiązanie
Zawsze uruchamiaj polecenia cmdlet usługi sieć szkieletowa bezpośrednio z programu Windows PowerShell.

> [!NOTE]
> Najnowszą wersję programu Azure PowerShell nie tworzy specjalne skrót, więc nie powinno to nastąpić.
> 
> 

### <a name="type-initialization-exception"></a>Wyjątek inicjowania typu
#### <a name="problem"></a>Problem
Podczas łączenia z klastrem w programie PowerShell zostanie wyświetlony błąd typeinitializationexception — System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Rozwiązanie
Podczas instalacji nie ustawiono poprawnie zmiennej path. Wyloguj się z systemem Windows i zaloguj się ponownie. Spowoduje to odświeżenie ścieżki.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Połączenia klastra kończy się niepowodzeniem z "Obiekt jest zamknięty"
#### <a name="problem"></a>Problem
Wywołanie Connect-ServiceFabricCluster zakończy się niepowodzeniem z powodu błędu w następujący sposób:

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Rozwiązanie
Zamknij bieżące okno programu PowerShell i otworzyć nowe okno programu PowerShell jako administrator. Teraz można nawiązywać połączeń.

### <a name="fabric-connection-denied-exception"></a>Wyjątek odmowa połączenia sieci szkieletowej
#### <a name="problem"></a>Problem
Podczas debugowania w programie Visual Studio, otrzymasz komunikat o błędzie FabricConnectionDeniedException.

#### <a name="solution"></a>Rozwiązanie
Ten błąd występuje zazwyczaj, gdy użytkownik próbuje uruchomić proces hosta usługi ręcznie, zamiast stosowanie środowiska uruchomieniowego platformy Service Fabric ją uruchomić za.

Upewnij się, że nie masz żadnych projektów usług Ustaw jako projekty startowe w rozwiązaniu. Tylko projekty aplikacji sieci szkieletowej usług powinna być ustawiona jako projekty startowe.

> [!TIP]
> Jeśli po zakończeniu instalacji, lokalnego klastra zaczyna działać nieprawidłowo, można zresetować go przy użyciu aplikacji na pasku zadań systemu Menedżera klastra lokalnego. Spowoduje to usunięcie istniejącego klastra i skonfigurować nowy. Należy pamiętać, że wszystkie wdrożone aplikacje i skojarzone dane zostaną usunięte.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Omówienie i rozwiązywanie problemów klastra za pomocą raportów o kondycji systemu](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

