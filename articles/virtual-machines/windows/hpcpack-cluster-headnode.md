---
title: "aaaCreate HPC Pack węzła głównego w maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toouse wdrożenia usługi Azure Resource Manager portal i hello modelu toocreate Microsoft HPC Pack 2012 R2 węzła głównego w maszynie Wirtualnej platformy Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Utwórz hello węzła głównego klastra HPC Pack w maszynie Wirtualnej platformy Azure z obrazu z witryny Marketplace
Użyj [obraz maszyny wirtualnej Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) z hello Azure Marketplace i hello Azure toocreate portalu hello węzła głównego klastra HPC. Tego obrazu maszyny Wirtualnej programu HPC Pack jest oparta na systemie Windows Server 2012 R2 Datacenter z preinstalowanym HPC Pack 2012 R2 Update 3. Użyj tego węzła głównego do weryfikacji koncepcji wdrożenia pakietu HPC na platformie Azure. Następnie można dodać węzłów obliczeniowych toohello toorun klastra HPC obciążenia pracą.

> [!TIP]
> toodeploy całego klastra HPC Pack 2012 R2 na platformie Azure, zawierającą hello węzła głównego i węzły obliczeniowe, zalecane jest użycie zautomatyzowaną metodę. Dostępne są następujące opcje hello [skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) i szablony Menedżera zasobów, takich jak hello [klastra HPC Pack dla obciążeń systemu Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Dostępne są również szablony Menedżera zasobów [klastrów Microsoft HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Zagadnienia dotyczące planowania
Jak pokazano na następującej ilustracji hello, możesz wdrożyć hello HPC Pack węzła głównego w domenie usługi Active Directory w sieci wirtualnej platformy Azure.

![HPC Pack węzła głównego][headnode]

* **Domena usługi Active Directory**: hello HPC Pack 2012 R2 musi być węzłem głównym przyłączone do domeny usługi Active Directory tooan na platformie Azure przed rozpoczęciem usług HPC hello na powitania maszyny Wirtualnej. Jak pokazano w tym artykule, weryfikacja koncepcji wdrożenia, możesz podwyższyć poziom hello maszyny Wirtualnej tworzonej dla węzła głównego hello jako kontroler domeny, przed uruchomieniem usługi HPC hello. Innym rozwiązaniem jest toodeploy kontrolera domeny oddzielne i lasu w toowhich Azure, aby sprzęgane hello węzła głównego maszyny Wirtualnej.

* **Model wdrażania**: dla większości nowych wdrożeń, firma Microsoft zaleca użycie modelu wdrażania usługi Resource Manager hello. W tym artykule przyjęto założenie, że używasz tego modelu wdrażania.

* **Sieć wirtualna platformy Azure**: użycie hello Resource Manager deployment model toodeploy hello węzła głównego, określ, lub Utwórz sieć wirtualną platformy Azure. Możesz użyć sieci wirtualnej hello, jeśli potrzebujesz toojoin hello węzła głównego tooan istniejącej domeny usługi Active Directory. Należy również jego nowsze tooadd węzeł obliczeniowy klastra toohello maszyn wirtualnych.

## <a name="steps-toocreate-hello-head-node"></a>Kroki węzła głównego hello toocreate
Poniżej przedstawiono ogólne kroki toouse hello toocreate portalu Azure maszyny Wirtualnej platformy Azure dla węzła głównego HPC Pack hello przy użyciu modelu wdrażania usługi Resource Manager hello. 

1. Jeśli chcesz toocreate nowego lasu usługi Active Directory na platformie Azure z kontrolera domeny oddzielne maszyn wirtualnych, jedną z opcji jest toouse [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Proste dowodu wdrożenia pojęcie ma drobne tooomit ten krok i skonfigurować węzła głównego hello samej maszyny Wirtualnej jako kontroler domeny. Ta opcja jest opisane w dalszej części tego artykułu.
2. Na powitania [HPC Pack 2012 R2 w witrynie Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) w hello Azure Marketplace, kliknij przycisk **Utwórz maszynę wirtualną**. 
3. W portalu hello na powitania **HPC Pack 2012 R2 w systemie Windows Server 2012 R2** strona, wybierz hello **Resource Manager** model wdrażania, a następnie kliknij przycisk **Utwórz**.
   
    ![HPC Pack obrazu][marketplace]
4. Użyj ustawień hello portalu tooconfigure hello i Utwórz hello maszyny Wirtualnej. Jeśli nowy tooAzure czynności opisane w samouczku hello [Utwórz maszynę wirtualną systemu Windows w portalu Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Do weryfikacji koncepcji wdrożenia zazwyczaj można zaakceptować domyślne hello lub zalecanych ustawień.
   
   > [!NOTE]
   > Jeśli chcesz tooan węzła głównego hello toojoin istniejącej domeny usługi Active Directory na platformie Azure, upewnij się, że zostanie hello sieci wirtualnej dla tej domeny podczas tworzenia hello maszyny Wirtualnej.
   > 
   > 
5. Po utworzeniu hello maszyny Wirtualnej i hello maszyna wirtualna jest uruchomiona, [toohello maszyny Wirtualnej Połącz](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przez pulpit zdalny. 
6. Dołącz do lasu usługi Active Directory tooan hello maszyny Wirtualnej w domenie, wybierając jedną z hello następujące opcje:
   
   * Jeśli utworzono hello maszyny Wirtualnej w sieci wirtualnej platformy Azure z istniejącym lesie domeny, Dołącz hello wirtualna toohello lasu przy użyciu standardowych narzędzi Menedżera serwera lub środowiska Windows PowerShell. Następnie uruchom ponownie.
   * Jeśli utworzono hello maszyny Wirtualnej w nowej sieci wirtualnej (bez istniejącego lasu domeny), podwyższyć poziom hello maszyny Wirtualnej, jako kontroler domeny. Użyj standardowych czynności tooinstall i skonfigurować rolę usług domenowych w usłudze Active Directory hello na powitania węzła głównego. Aby uzyskać szczegółowe instrukcje, zobacz [instalowania nowego lasu systemu Windows Server 2012 Active Directory](https://technet.microsoft.com/library/jj574166.aspx).
7. Po hello maszyna wirtualna jest uruchomiona i tooan przyłączone do lasu usługi Active Directory, uruchamiania usług HPC Pack hello w następujący sposób:
   
    a. Połącz węzła głównego toohello maszyny Wirtualnej przy użyciu konta domeny, które jest członkiem lokalnej grupy administratorów hello. Na przykład użyć hello konta administratora, które można skonfigurować podczas tworzenia węzła głównego hello maszyny Wirtualnej.
   
    b. Dla domyślnej konfiguracji węzła głównego Uruchom program Windows PowerShell jako administrator i wpisz następujące hello:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Może upłynąć kilka minut toostart usług HPC Pack hello.
   
    Dla węzła głównego dodatkowe opcje konfiguracji, wpisz `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Następne kroki
* Teraz możesz pracować z hello węzła głównego klastra HPC Pack. Na przykład uruchomić Menedżera klastra HPC i pełne hello [listy zadań do wykonania wdrożenia](https://technet.microsoft.com/library/jj884141.aspx).
* Tooincrease hello klastra obliczeniowego pojemności na żądanie, należy dodać [Azure serii węzłów](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) w usłudze w chmurze. 
* Spróbuj uruchomić test obciążenia w klastrze hello. Na przykład zobacz hello HPC Pack [Wprowadzenie — przewodnik](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
