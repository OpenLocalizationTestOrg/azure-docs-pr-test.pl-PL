---
title: aaaAzure Linux maszyny wirtualnej DotNet Core samouczek 1 | Dokumentacja firmy Microsoft
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b3652e86-0c44-4ac9-8cd1-27abdeaea4d4
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e6f047197336de1e93c50413b6eabb718230bc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toolinux-virtual-machines"></a>Automatyzowanie aplikacji wdrożeń tooLinux maszyny wirtualne 

Ta seria czteroczęściową zawiera szczegóły dotyczące wdrażania i konfigurowania zasobów platformy Azure i aplikacji przy użyciu szablonów usługi Azure Resource Manager. W tej serii przykładowy szablon został wdrożony i hello zbadane Szablon wdrożenia. Celem tej serii Hello jest tooeducate hello relacji między zasobami Azure i tooprovide przekazuje na wdrażanie szablonów usługi Azure Resource Manager pełni zintegrowane środowisko. Tym dokumencie przyjęto założenie podstawowy poziom wiedzy za pomocą Menedżera zasobów Azure, przed rozpoczęciem tego samouczka należy zapoznać się z podstawowe pojęcia dotyczące usługi Azure Resource Manager. 

## <a name="music-store-application"></a>Muzyka aplikację ze sklepu
Witaj przykład używany w tej serii jest .net aplikacja Core symulując magazynu muzyki, atrakcyjne. Ta aplikacja może być wdrożony tooeither Linux lub Windows systemu wirtualnego, przykładowego wdrożenia zostały utworzone dla obu. Aplikacja Hello zawiera aplikacji sieci web i bazy danych SQL. Przed przeczytaniem hello artykuły w tej serii, wdrażanie aplikacji hello za pomocą przycisku wdrożenia hello znaleziono na tej stronie. Po wdrożeniu w pełni hello architektury aplikacji / usługi Azure wygląda jak powitania po diagramu. 

Szablon Menedżera zasobów magazynu utworów muzycznych Hello znajduje się w tym miejscu [utworów muzycznych magazynu Linux szablonu](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)

![Aplikację ze sklepu utworów muzycznych](./media/dotnet-core-1-landing/music-store.png)

Każdy z tych składników, w tym hello Kojarzenie szablonu JSON jest sprawdzany w hello następujące cztery artykułów.

* [**Aplikacja — architektura** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — składniki aplikacji, takich jak witryny sieci web i baz danych muszą toobe hostowanych na komputerze Azure zasobów, takich jak maszyn wirtualnych i baz danych Azure SQL. Ten dokument przeprowadzi Cię przez mapowania muszą obliczeń, tooAzure zasobów i wdrażanie tych zasobów przy użyciu szablonu usługi Azure Resource Manager. 
* [**Dostęp i większe bezpieczeństwo** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — odnośnie do hostowania aplikacji na platformie Azure, jest konieczne tooconsider, sposobie uzyskania dostępu do aplikacji hello oraz konfigurowania składników w innej aplikacji, dostęp do siebie. Ten dokument zawiera szczegóły zapewnianie i zabezpieczania dostępu między składnikami aplikacji i aplikacji tooan dostęp do Internetu.
* [**Dostępności i skalowalności** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — dostępności i skalowalności można znaleźć toostay możliwości aplikacji toohello działania podczas przestoje w ramach infrastruktury i hello tooscale możliwości obliczeniowe żądanie aplikacji toomeet zasobów. Ten dokument szczegóły hello składniki wymagane toodeploy równoważenia obciążenia i wysokiej dostępności aplikacji.
* [**Wdrażanie aplikacji** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — w przypadku wdrażania aplikacji na maszynach wirtualnych platformy Azure, metoda hello, przez które hello plików binarnych aplikacji są zainstalowane na powitania maszyny wirtualnej, należy rozważyć użycie. Ten dokument zawiera szczegóły dotyczące automatyzacji instalacji aplikacji przy użyciu rozszerzenia skryptów niestandardowych maszyny wirtualnej Azure.

Celem Hello, podczas tworzenia szablonów usługi Azure Resource Manager jest tooautomate hello wdrażania infrastruktury platformy Azure i hello instalacji i konfiguracji wszystkie aplikacje obsługiwane w tej infrastrukturze Azure. Pracy nad tymi artykułami zawiera przykład tej czynności.

## <a name="deploy-hello-music-store-application"></a>Wdrażanie aplikacji magazynu utworów muzycznych hello
Hello aplikacji utworów muzycznych magazynu można wdrożyć za pomocą tego przycisku.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

Szablon usługi Azure Resource Manager Hello wymaga hello następujące wartości parametrów.

| Nazwa parametru | Opis |
| --- | --- |
| SSHKEYDATA |Dane klucza SSH używane toosecure toohello dostęp do maszyny wirtualnej. Aby uzyskać informacje dotyczące tworzenia parę kluczy SSH, zobacz [tworzenie SSH kluczy dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). |
| ADMINUSERNAME |Nazwa użytkownika administratora jest używany w maszynie wirtualnej hello i hello bazy danych SQL Azure. |
| SQLADMINPASSWORD |Hasło, które jest używane na powitania bazy danych SQL Azure. |
| NUMBEROFINSTANCES |Liczba Hello toobe maszyny wirtualne utworzone. Każdy z tych aplikacji sieci web sklep muzyczny hello maszyny wirtualne hosta, a także cały ruch jest równoważone między nimi. |
| PUBLICIPADDRESSDNSNAME |Globalnie unikatowa nazwa DNS skojarzone z hello publicznego adresu IP. |

Po zakończeniu wdrażania szablonu hello Przeglądaj toohello adres publiczny adres IP przy użyciu dowolnej przeglądarki internetowej. Witaj .net Core muzyka witryna zostanie wyświetlone.

## <a name="next-steps"></a>Następne kroki
<hr>

[Krok 1 — Architektura aplikacji z szablonów usługi Azure Resource Manager](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Krok 2 — dostępu i zabezpieczeń w szablonach usługi Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Krok 3 — dostępności i skalowalności w szablonach usługi Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Krok 4. wdrożenie aplikacji z szablonów usługi Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

