---
title: "aaaUnderstand udostępnionych adresów IP w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure DevTest Labs używa udostępnionego IP adresów toominimize hello publicznego adresu IP adresy wymagane tooaccess laboratorium maszyn wirtualnych."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Zrozumienie udostępnionego adresów IP w usłudze Azure DevTest Labs

Azure DevTest Labs umożliwia laboratorium udziału maszyn wirtualnych hello publicznego adresu IP adres toominimize hello tyle publicznego tooaccess wymaganych adresów IP laboratorium poszczególnych maszyn wirtualnych.  W tym artykule opisano, jak udostępnione pracy adresów IP oraz ich powiązane opcje konfiguracji.

## <a name="shared-ip-setting"></a>Udostępnione ustawienie adresu IP

Po utworzeniu laboratorium znajduje się w podsieci sieci wirtualnej.  Domyślnie ta podsieć jest tworzony z **Włącz udostępnione publicznego adresu IP** ustawić także*tak*.  Ta konfiguracja tworzy jeden publiczny adres IP hello całej podsieci.  Aby uzyskać więcej informacji na temat konfigurowania sieci wirtualnych i podsieci, zobacz [Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nowa podsieć laboratorium](media/devtest-lab-shared-ip/lab-subnet.png)

Istniejące labs tę opcję można włączyć, wybierając **konfiguracji i zasadach > sieci wirtualnych**. Następnie wybierz sieć wirtualną z listy hello i wybierz **Włącz UDOSTĘPNIONE publicznego adresu IP** dla wybranej podsieci. Można również wyłączyć tę opcję w dowolnym laboratorium, jeśli nie chcesz tooshare publicznego adresu IP w laboratorium maszyn wirtualnych.

Wszystkie maszyny wirtualne utworzone w toousing domyślne tego laboratorium udostępnionego IP.  Podczas tworzenia hello maszyny Wirtualnej, to ustawienie można zaobserwować w hello **Zaawansowane ustawienia** bloku w obszarze **konfiguracji adresu IP**.

![Nowej maszyny Wirtualnej](media/devtest-lab-shared-ip/new-vm.png)

- **Shared:** wszystkie maszyny wirtualne utworzone jako **Shared** są umieszczane w jednej grupy zasobów (zarządcy zasobów). Pojedynczy adres IP jest przypisany do tego zarządcy zasobów i wszystkich maszyn wirtualnych w hello zarządcy zasobów będzie używać tego adresu IP.
- **Publicznego:** każdej maszyny Wirtualnej tworzonej ma swój adres IP i jest tworzona w jego własnej grupy zasobów.
- **Prywatne:** każdej maszyny Wirtualnej tworzonej używa prywatnego adresu IP. Nie będą mogli tooconnect toothis maszyny Wirtualnej bezpośrednio z hello internet przy użyciu pulpitu zdalnego.

Przy każdym dodaniu toohello podsieci maszyny Wirtualnej z udostępnionego IP włączone DevTest Labs automatycznie dodaje hello modułu równoważenia obciążenia tooa dla maszyny Wirtualnej i przypisuje numer portu TCP na powitania publicznego adresu IP, przekazywania toohello portem RDP na powitania maszyny Wirtualnej.  

## <a name="using-hello-shared-ip"></a>Używanie hello udostępnionego IP

- **Użytkownicy systemu Linux:** toohello SSH maszyny Wirtualnej za pomocą adresu IP hello lub pełną nazwę domeny, wprowadź dwukropek, a następnie hello portu. Na przykład w poniższym obrazie hello, hello RDP adresów toohello tooconnect maszyna wirtualna jest `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Przykład maszyny Wirtualnej](media/devtest-lab-shared-ip/vm-info.png)

- **Użytkownicy systemu Windows:** wybierz hello **Connect** znajdującego się na powitania toodownload portalu Azure wstępnie skonfigurowany plik RDP i dostępu hello maszyny Wirtualnej.

## <a name="next-steps"></a>Następne kroki

* [Definiowanie zasad laboratorium w usłudze Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs](devtest-lab-configure-vnet.md)





