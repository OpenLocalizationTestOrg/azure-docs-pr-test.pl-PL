---
title: "aaaTroubleshoot ustawienia lokalnego klastra usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Rozwiązywanie problemów z konfiguracji klastra lokalnego rozwoju
Jeśli napotkasz problem podczas interakcji z lokalnym klastrem programowanie sieć szkieletowa usług Azure, przejrzyj powitania po sugestie dotyczące potencjalne rozwiązania.

## <a name="cluster-setup-failures"></a>Błędy instalacji klastra
### <a name="cannot-clean-up-service-fabric-logs"></a>Nie można wyczyścić dzienniki sieci szkieletowej usług
#### <a name="problem"></a>Problem
Podczas uruchamiania skryptu DevClusterSetup hello, zostanie wyświetlony błąd w następujący sposób:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Rozwiązanie
Zamknij bieżące okno programu PowerShell hello i otworzyć nowe okno programu PowerShell jako administrator. Teraz powinno być możliwe toosuccessfully Uruchom skrypt hello.

## <a name="cluster-connection-failures"></a>Liczba błędów połączenia klastra
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Polecenia cmdlet programu PowerShell usługi Service Fabric nie są rozpoznawane w programie Azure PowerShell
#### <a name="problem"></a>Problem
Jeśli spróbujesz toorun żadnego hello poleceń cmdlet programu PowerShell usługi Service Fabric, takich jak `Connect-ServiceFabricCluster` w oknie programu PowerShell usługi Azure jej nie powiedzie się, informujący o tym, to polecenie cmdlet hello nie został rozpoznany. Witaj przyczyną tego błędu jest używany hello 32-bitowa wersja programu Windows PowerShell (nawet na 64-bitowe wersje systemu operacyjnego), programu Azure PowerShell hello poleceń cmdlet usługi sieć szkieletowa tylko pracy w środowiskach 64-bitowych.

#### <a name="solution"></a>Rozwiązanie
Zawsze uruchamiaj polecenia cmdlet usługi sieć szkieletowa bezpośrednio z programu Windows PowerShell.

> [!NOTE]
> Hello najnowszą wersję programu Azure PowerShell nie tworzy specjalne skrót, więc nie powinno to nastąpić.
> 
> 

### <a name="type-initialization-exception"></a>Wyjątek inicjowania typu
#### <a name="problem"></a>Problem
Podczas łączenia z toohello klastra w programie PowerShell zostanie wyświetlony błąd hello typeinitializationexception — System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Rozwiązanie
Podczas instalacji nie ustawiono poprawnie zmiennej path. Wyloguj się z systemem Windows i zaloguj się ponownie. Spowoduje to odświeżenie ścieżki.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Połączenia klastra kończy się niepowodzeniem z "Obiekt jest zamknięty"
#### <a name="problem"></a>Problem
Wywołanie tooConnect-ServiceFabricCluster zakończy się niepowodzeniem z powodu błędu w następujący sposób:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Rozwiązanie
Zamknij bieżące okno programu PowerShell hello i otworzyć nowe okno programu PowerShell jako administrator. Teraz powinno być możliwe połączenie toosuccessfully.

### <a name="fabric-connection-denied-exception"></a>Wyjątek odmowa połączenia sieci szkieletowej
#### <a name="problem"></a>Problem
Podczas debugowania w programie Visual Studio, otrzymasz komunikat o błędzie FabricConnectionDeniedException.

#### <a name="solution"></a>Rozwiązanie
Ten błąd zazwyczaj występuje podczas toostart procesu hosta usługi ręcznie, zamiast stosowanie toostart środowiska uruchomieniowego platformy Service Fabric hello go.

Upewnij się, że nie masz żadnych projektów usług Ustaw jako projekty startowe w rozwiązaniu. Tylko projekty aplikacji sieci szkieletowej usług powinna być ustawiona jako projekty startowe.

> [!TIP]
> Jeśli po zakończeniu instalacji, klaster lokalny rozpoczyna toobehave nieprawidłowo, można zresetować go przy użyciu aplikacji na pasku zadań systemu Menedżera klastra lokalnego hello. Spowoduje to usunięcie hello istniejącego klastra i skonfigurować nowy. Należy pamiętać, że wszystkie wdrożone aplikacje i skojarzone dane zostaną usunięte.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Omówienie i rozwiązywanie problemów klastra za pomocą raportów o kondycji systemu](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

