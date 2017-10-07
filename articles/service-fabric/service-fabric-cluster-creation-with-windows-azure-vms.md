---
title: aaaCreate autonomiczny klastra z systemem Windows maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate i zarządzanie nimi klastra usługi sieć szkieletowa usług Azure na maszynach wirtualnych Azure systemem Windows Server."
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
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Tworzenie klastra sieci szkieletowej usług autonomiczny trzech węzłów z systemem Windows Server maszyn wirtualnych platformy Azure
W tym artykule opisano, jak toocreate a klastra na opartych na systemie Windows Azure maszynach wirtualnych (VM), za pomocą hello autonomicznego Instalatora usługi sieć szkieletowa usług dla systemu Windows Server. Scenariusz Hello jest specjalny przypadek [tworzenie i Zarządzanie klastrem w systemie Windows Server](service-fabric-cluster-creation-for-windows-server.md) gdzie hello maszyny wirtualne są [maszynach wirtualnych platformy Azure, systemem operacyjnym Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), ale nie są tworzone [platformy Azure oparte na chmurze klaster sieci szkieletowej usług](service-fabric-cluster-creation-via-portal.md). rozróżnienie Hello w poniższych ten wzorzec jest hello klastra sieci szkieletowej usług autonomiczny utworzony przez hello następujące kroki całkowicie jest zarządzane przez użytkownika, powitalne Azure opartej na chmurze usługi sieć szkieletowa klastry są zarządzane i uaktualniane przez hello sieci szkieletowej usług dostawcy zasobów.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Kroki toocreate hello autonomiczny klastra
1. Zaloguj się toohello portalu Azure i utworzyć nowe systemu Windows Server 2012 R2 Datacenter lub maszyny Wirtualnej systemu Windows Server 2016 centrum danych w grupie zasobów. Przeczytaj artykuł hello [utworzyć Maszynę wirtualną systemu Windows w portalu Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) więcej szczegółów.
2. Dodaj kilka więcej toohello maszyn wirtualnych tej samej grupie zasobów. Upewnij się, że każdy hello maszyn wirtualnych ma hello tej samej nazwy użytkownika administratora i hasła podczas tworzenia. Po utworzeniu powinny być widoczne wszystkie trzy maszyny wirtualne w hello tej samej sieci wirtualnej.
3. Połącz tooeach hello maszyn wirtualnych i wyłączyć hello zapory systemu Windows przy użyciu hello [Menedżera serwera, pulpitu nawigacyjnego serwera lokalnego](https://technet.microsoft.com/library/jj134147.aspx). Dzięki temu, że ruch sieciowy hello może komunikować się między maszynami hello. Podczas tooeach podłączonego komputera, należy uzyskać adres IP hello, otwórz wiersz polecenia i wpisując `ipconfig`. Można również widać hello IP adres każdej maszyny w portalu hello, wybierając hello zasobów sieci wirtualnej dla grupy zasobów hello i sprawdzanie interfejsów sieciowych hello tworzony dla każdego z tych urządzeń.
4. Połącz tooone hello maszyn wirtualnych i test, który może wysyłać polecenia ping hello pomyślnie innych dwóch maszyn wirtualnych.
5. Połącz tooone hello maszyn wirtualnych i [Pobierz hello autonomicznej usługi sieć szkieletowa usług dla systemu Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) do nowego folderu na powitania komputera i wyodrębniać hello pakietu.
6. Otwórz hello *ClusterConfig.Unsecure.MultiMachine.json* pliku w Notatniku i edytować każdy węzeł z adresami IP hello trzech hello maszyn. Zmień nazwę klastra hello u góry hello i Zapisz plik hello.  Poniżej przedstawiono częściowe przykład hello manifestu klastra.
   
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
7. Jeśli planujesz tego toobe bezpiecznego klastra, zdecyduj, zabezpieczenie hello chcesz toouse i wykonaj czynności hello hello skojarzone łącze: [certyfikatu X509](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md). Konfigurowanie klastra hello przy użyciu zabezpieczeń systemu Windows, należy tooset się toomanage kontrolera domeny usługi Active Directory. Należy pamiętać, że używanie maszyny kontrolera domeny jako usługi sieć szkieletowa węzeł nie jest obsługiwane.
8. Otwórz [okno programu PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Przejdź toohello folder, w którym wyodrębnić pakiet instalatora autonomicznego pobrany hello i zapisania pliku konfiguracji klastra hello. Uruchom powitania po klastra hello toodeploy polecenia programu PowerShell:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

skrypt Hello zdalnie konfiguruje klaster sieci szkieletowej usług hello i zgłoś postęp wdrażania przedstawia za pośrednictwem.

9. Po około minutę, możesz sprawdzić, jeśli klaster hello działa łącząc toohello Service Fabric Explorer przy użyciu jednego adresu IP komputera hello dotyczy, na przykład za pomocą `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Następne kroki
* [Tworzenie autonomicznych klastrów usługi Service Fabric w systemie Windows Server lub Linux](service-fabric-deploy-anywhere.md)
* [Dodawanie lub usuwanie klastra sieci szkieletowej usług autonomiczny tooa węzłów](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Ustawienia konfiguracji dla autonomicznych klastra systemu Windows](service-fabric-cluster-manifest.md)
* [Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows](service-fabric-windows-cluster-windows-security.md)
* [Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów](service-fabric-windows-cluster-x509-security.md)

