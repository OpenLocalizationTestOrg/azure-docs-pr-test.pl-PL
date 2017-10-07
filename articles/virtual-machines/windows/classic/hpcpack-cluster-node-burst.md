---
title: "aaaAdd serii węzłów tooan HPC Pack klastra | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooexpand HPC Pack klastra w Azure na żądanie, dodając wystąpień roli procesów roboczych uruchomionych w usłudze chmury"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>Dodaj na żądanie "serii" węzłów tooan HPC Pack klaster na platformie Azure
Po skonfigurowaniu [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) klastra na platformie Azure, możesz sposób tooquickly skali hello klastra pojemności w górę lub w dół, bez zachowania zestaw wstępnie węzeł obliczeniowy maszyn wirtualnych. W tym artykule opisano sposób tooadd na żądanie "serii" węzłów (uruchomionych w usłudze chmury wystąpień roli proces roboczy) jako węzła głównego tooa zasoby obliczeniowe na platformie Azure. 

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

![Węzły serii][burst]

etapy Hello w tym artykule ułatwiają szybko dodać węzły platformy Azure tooa oparte na chmurze HPC Pack węzła głównego maszyny Wirtualnej dla testu lub Weryfikacja koncepcji wdrożenia. Ogólne kroki Hello są hello taka sama, jak kroki hello zbyt "serii tooAzure" klaster HPC Pack lokalnymi tooan pojemności chmury tooadd obliczania. Samouczek, zobacz [skonfiguruj hybrydowych klastra obliczeniowego z pakietem Microsoft HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Szczegółowe wskazówki i zagadnienia dotyczące wdrożeń produkcyjnych, zobacz [serii tooAzure z pakietem Microsoft HPC](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Wymagania wstępne
* **Węzłem głównym HPC Pack wdrożony w maszynie Wirtualnej platformy Azure** — możesz użyć węzła głównego autonomicznej maszyny Wirtualnej lub taki, który jest częścią większego klastra. Zobacz toocreate autonomicznego węzła głównego [wdrażanie węźle głównym HPC Pack w maszynie Wirtualnej platformy Azure](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Automatyczne opcji wdrażania klastra HPC Pack, zobacz [opcje toocreate i zarządzanie nimi klastra HPC systemu Windows na platformie Azure z pakietem Microsoft HPC](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Jeśli używasz hello [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) toocreate hello klastra na platformie Azure, możesz dołączyć węzłów Azure serii w danym wdrożeniu automatycznych. Zobacz hello przykłady w tym artykule.
  > 
  > 
* **Subskrypcja platformy Azure** -tooadd Azure węzłów, można wybrać hello tej samej subskrypcji używane węzła głównego toodeploy hello maszyny Wirtualnej, lub innej subskrypcji (lub subskrypcji).
* **Limit przydziału rdzeni** — może być konieczne tooincrease hello przydziału rdzeni, zwłaszcza jeśli toodeploy kilka węzłów Azure o rozmiarze wielordzeniowych. limit przydziału, tooincrease [otwarcia żądania pomocy technicznej online klienta](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) bez dodatkowych opłat.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>Krok 1: Tworzenie usługi w chmurze i konto magazynu dla hello węzły platformy Azure
Użyj hello klasycznego portalu Azure lub analogicznych narzędzi tooconfigure hello następujące zasoby, które są potrzebne toodeploy węzły platformy Azure:

* Nową usługę w chmurze Azure
* Nowe konto magazynu Azure

> [!NOTE]
> Nie ponownego użycia istniejącej usługi w chmurze w ramach subskrypcji. 
> 
> 

**Zagadnienia do rozważenia**

* Konfigurowanie usługi w chmurze osobne dla każdego szablonu Azure węzła zaplanowanie toocreate. Można jednak użyć hello tego samego konta magazynu dla wielu szablonów węzła.
* Zaleca się, Znajdź hello usługi w chmurze i konto magazynu hello hello wdrożenia w hello tego samego regionu systemu Azure.

## <a name="step-2-configure-an-azure-management-certificate"></a>Krok 2: Konfigurowanie certyfikat zarządzania platformy Azure
tooadd Azure węzłów zasoby obliczeniowe, wymagany jest certyfikat zarządzania na powitania węzła głównego i przekazywanie odpowiedniego certyfikatu toohello używane dla wdrożenia hello subskrypcji platformy Azure.

W tym scenariuszu można wybrać hello **domyślne certyfikat zarządzania platformy Azure HPC** HPC Pack instaluje i konfiguruje się automatycznie w węźle głównym. Ten certyfikat jest przydatna przy testowaniu celów i weryfikacja koncepcji wdrożenia. toouse to świadectwo, Przekaż plik 2012\Bin\hpccert.cer C:\Program Files\Microsoft HPC Pack z węzłem głównym hello subskrypcji toothe maszyny Wirtualnej. certyfikat hello tooupload w hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **ustawienia** > **certyfikaty zarządzania**.

Aby uzyskać dodatkowe opcje tooconfigure hello certyfikat zarządzania, zobacz [scenariusze tooConfigure hello certyfikat zarządzania platformy Azure w przypadku wdrożeń serii Azure](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>Krok 3: Wdrażanie klastra toohello węzły platformy Azure
Witaj tooadd kroki i uruchomić Azure węzłów w tym scenariuszu są zazwyczaj hello sam jako hello kroków za pomocą lokalnego węzła głównego. Aby uzyskać więcej informacji, zobacz następujące sekcje w hello [kroki tooDeploy węzłów Azure z pakietem Microsoft HPC](https://technet.microsoft.com/library/gg481758.aspx):

* Tworzenie szablonu Azure węzła
* Dodaj klaster HPC systemu Windows Azure węzłów toohello
* Start (zainicjować obsługi administracyjnej) hello węzły platformy Azure

Po dodaniu i uruchomić hello węzły są gotowe toouse toorun klastra zadania.

W razie wystąpienia problemów podczas wdrażania węzły platformy Azure, zobacz [Rozwiązywanie problemów z wdrożeniami Azure węzłów z pakietem Microsoft HPC](http://technet.microsoft.com/library/jj159097.aspx).

## <a name="next-steps"></a>Następne kroki
* toouse rozmiar wystąpienia obliczeniowych hello serii węzłów, zobacz uwagi hello w [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Jeśli chcesz automatycznie zwiększać i zmniejszać hello Azure zasobów zgodnie z obciążenie klastra hello obliczeniowych, zobacz [automatycznie zwiększyć lub zmniejszyć zasoby obliczeniowe systemu Azure w klastrze HPC Pack](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
