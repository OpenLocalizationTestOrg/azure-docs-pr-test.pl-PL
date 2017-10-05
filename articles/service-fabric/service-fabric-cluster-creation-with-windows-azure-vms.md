---
title: Tworzenie klastra autonomiczny z systemem Windows maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Informacje o sposobie tworzenia i zarządzania nimi klastra usługi sieć szkieletowa usług Azure na maszynach wirtualnych Azure systemem Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Tworzenie klastra sieci szkieletowej usług autonomiczny trzech węzłów z systemem Windows Server maszyn wirtualnych platformy Azure
W tym artykule opisano sposób tworzenia klastra w przypadku komputerów z systemem Windows Azure maszyn wirtualnych (VM), za pomocą autonomicznego Instalatora usługi sieć szkieletowa usług dla systemu Windows Server. Scenariusz jest specjalny przypadek [tworzenie i Zarządzanie klastrem w systemie Windows Server](service-fabric-cluster-creation-for-windows-server.md) skutkującej maszyn wirtualnych [maszynach wirtualnych platformy Azure, systemem operacyjnym Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), ale nie są tworzone [platformy Azure oparte na chmurze klaster sieci szkieletowej usług](service-fabric-cluster-creation-via-portal.md). Różnica w poniższych ten wzorzec jest czy klastra sieci szkieletowej usług autonomiczny utworzony przez następujące kroki całkowicie jest zarządzana przez użytkownika, Azure opartej na chmurze klastrów sieci szkieletowej usług są zarządzane i uaktualniane przez zasobów sieci szkieletowej usług Dostawca.

## <a name="steps-to-create-the-standalone-cluster"></a>Kroki umożliwiające utworzenie klastra autonomiczny
1. Zaloguj się do portalu Azure i utworzyć nowe systemu Windows Server 2012 R2 Datacenter lub maszyny Wirtualnej systemu Windows Server 2016 centrum danych w grupie zasobów. Przeczytaj artykuł na temat [utworzyć Maszynę wirtualną systemu Windows w portalu Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) więcej szczegółów.
2. Dodaj kilka więcej maszyn wirtualnych do tej samej grupie zasobów. Sprawdź, czy poszczególnych maszyn wirtualnych ma taką samą nazwę użytkownika administratora i hasła podczas tworzenia. Po utworzeniu powinny być widoczne wszystkie trzy maszyny wirtualne w tej samej sieci wirtualnej.
3. Nawiązywanie połączenia wszystkich maszynach wirtualnych i wyłączyć za pomocą zapory systemu Windows [Menedżera serwera, pulpitu nawigacyjnego serwera lokalnego](https://technet.microsoft.com/library/jj134147.aspx). Dzięki temu, że ruch sieciowy może komunikować się między komputerami. Podczas połączenia z każdego komputera, należy uzyskać adres IP, należy otworzyć wiersz polecenia i wpisując `ipconfig`. Alternatywnie można wyświetlić adres IP każdego komputera na portalu, wybierając zasobów sieci wirtualnej dla grupy zasobów i sprawdzanie interfejsów sieciowych, tworzony dla każdego z tych urządzeń.
4. Połącz do jednej z maszyn wirtualnych i przetestować, czy można pomyślnie ping innych dwóch maszyn wirtualnych.
5. Podłącz do jednego z maszyn wirtualnych i [Pobierz autonomicznych pakietu sieci szkieletowej usług dla systemu Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) do nowego folderu na komputerze i wyodrębniania pakietu.
6. Otwórz *ClusterConfig.Unsecure.MultiMachine.json* pliku w Notatniku i edytować każdy węzeł z trzech adresów IP maszyn. Zmień nazwę klastra u góry i Zapisz plik.  Poniżej przedstawiono częściowe przykład manifestu klastra.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Zdecyduj, czy ma być bezpieczne klastra, zabezpieczenie chcesz i wykonaj kroki opisane w temacie skojarzone łącze: [certyfikatu X509](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md). Konfigurowanie klastra przy użyciu zabezpieczeń systemu Windows, należy skonfigurować kontroler domeny do zarządzania usługą Active Directory. Należy pamiętać, że używanie maszyny kontrolera domeny jako usługi sieć szkieletowa węzeł nie jest obsługiwane.
8. Otwórz [okno programu PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Przejdź do folderu, w którym wyodrębniono pakiet pobrany Autonomiczny Instalator i zapisania pliku konfiguracji klastra. Uruchom następujące polecenie programu PowerShell, aby wdrożyć klaster:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

Skrypt zdalnie konfiguruje klaster sieci szkieletowej usług i zgłoś postęp wdrażania przedstawia za pośrednictwem.

9. Po około minutę, możesz sprawdzić, czy klaster działa przez nawiązanie połączenia za pomocą jednego z adresów IP na komputerze, na przykład za pomocą Eksploratora usługi sieć szkieletowa `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Następne kroki
* [Tworzenie autonomicznych klastrów usługi Service Fabric w systemie Windows Server lub Linux](service-fabric-deploy-anywhere.md)
* [Dodaj lub usuń węzły do klastra usługi sieć szkieletowa autonomiczny](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Ustawienia konfiguracji dla autonomicznych klastra systemu Windows](service-fabric-cluster-manifest.md)
* [Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows](service-fabric-windows-cluster-windows-security.md)
* [Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów](service-fabric-windows-cluster-x509-security.md)

