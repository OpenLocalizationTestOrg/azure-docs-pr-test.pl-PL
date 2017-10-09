---
title: Interfejs sieciowy tooreset aaaHow dla maszyny Wirtualnej systemu Windows Azure | Dokumentacja firmy Microsoft
description: Pokazuje, jak tooreset interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Jak tooreset interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Nie można połączyć z tooMicrosoft maszyny wirtualnej systemu Windows Azure (VM), po wyłączeniu hello domyślnego interfejsu sieciowego (NIC) lub ręcznie ustawia statyczny adres IP dla karty sieciowej hello. W tym artykule opisano, jak tooreset hello interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure, która rozwiąże problem połączenia zdalnego hello.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Resetuj interfejsu sieciowego

### <a name="for-classic-vms"></a>Klasycznych maszyn wirtualnych

sieci tooreset interfejsu, wykonaj następujące kroki:

1.  Przejdź toohello [portalu Azure]( https://ms.portal.azure.com).
2.  Wybierz **maszyn wirtualnych (klasyczne)**.
3.  Wybierz hello wpływ maszyny wirtualnej.
4.  Wybierz **adresów IP**.
5.  Jeśli hello **przydziału prywatnego adresu IP** nie jest **statycznych**, zmień ją za**statycznych**.
6.  Zmień hello **adres IP** tooanother adresu IP, dostępnym w hello podsieci.
7.  Wybierz opcję Zapisz.
8.  Witaj maszyny wirtualnej zostanie uruchomiony ponownie tooinitialize hello nowy system toohello karty Sieciowej.
9.  Spróbuj tooRDP tooyour maszyny. W przypadku powodzenia można zmienić hello prywatnego adresu IP address wstecz toohello oryginalnej, jeśli chcesz. W przeciwnym razie można zachować. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Dla maszyn wirtualnych wdrożonych w modelu grupy zasobów

1.  Przejdź toohello [portalu Azure]( https://ms.portal.azure.com).
2.  Wybierz hello wpływ maszyny wirtualnej.
3.  Wybierz **interfejsy sieciowe**.
4.  Wybierz powitalne skojarzoną z interfejsem sieciowym z komputera
5.  Wybierz **konfiguracje adresów IP**.
6.  Wybierz hello IP. 
7.  Jeśli hello **przydziału prywatnego adresu IP** nie jest **statycznych**, zmień ją za**statycznych**.
8.  Zmień hello **adres IP** tooanother adresu IP, dostępnym w hello podsieci.
9. Witaj maszyny wirtualnej zostanie uruchomiony ponownie tooinitialize hello nowy system toohello karty Sieciowej.
10. Spróbuj tooRDP tooyour maszyny. W przypadku powodzenia można zmienić hello prywatnego adresu IP address wstecz toohello oryginalnej, jeśli chcesz. W przeciwnym razie można zachować. 

## <a name="delete-hello-unavailable-nics"></a>Usuń hello niedostępny kart sieciowych
Po można maszyny toohello pulpitu zdalnego, należy usunąć hello starego kart sieciowych tooavoid hello potencjalny problem:

1.  Otwórz Menedżera urządzeń.
2.  Wybierz **widoku** > **Pokaż ukryte urządzenia**.
3.  Wybierz **karty sieciowe**. 
4.  Sprawdź, czy karty hello jako "Karta sieciowa Microsoft Hyper-V".
5.  Może pojawić się niedostępne karty, który jest niedostępny. Kliknij prawym przyciskiem myszy kartę hello, a następnie wybierz Odinstaluj.

    ![Obraz powitania hello karty Sieciowej](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Tylko odinstalować hello kart niedostępny hello o nazwie "Karta sieciowa Microsoft Hyper-V". Po odinstalowaniu żadnego hello innych kart ukryte, może to spowodować dodatkowe problemy.
    >
    >

6.  Teraz wszystkie karty niedostępny powinny zostać wyczyszczone z systemu.