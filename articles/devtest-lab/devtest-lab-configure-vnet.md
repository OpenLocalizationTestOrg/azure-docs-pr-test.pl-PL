---
title: "aaaConfigure sieci wirtualnej w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure istniejącej sieci wirtualnej i podsieci i używać ich na maszynie wirtualnej z platformy Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs
Zgodnie z opisem w artykule hello [dodać maszyny Wirtualnej z laboratorium tooa artefakty](devtest-lab-add-vm-with-artifacts.md), podczas tworzenia maszyn wirtualnych w laboratorium, można określić skonfigurowanej sieci wirtualnej. Jeden scenariusz w ten sposób jest, jeśli potrzebujesz tooaccess zasobami sieci corpnet z maszyn wirtualnych przy użyciu hello sieci wirtualnej, który został skonfigurowany za pomocą usługi ExpressRoute i sieci VPN typu lokacja lokacja. Witaj poniższe sekcje przedstawiają sposób tooadd istniejącej sieci wirtualnej do ustawień sieci wirtualnej laboratorium, tak aby była dostępna toochoose podczas tworzenia maszyn wirtualnych.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Skonfiguruj sieć wirtualną dla laboratorium hello portalu Azure
Witaj kolejnych krokach objaśniono sposób przez procedurę dodawania istniejącego wirtualnego sieci (i podsieci) tooa laboratorium, dzięki czemu można użyć podczas tworzenia maszyny Wirtualnej w hello tego samego laboratorium. 

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello. 
4. W bloku hello laboratorium, wybierz **konfiguracji**.
5. W laboratorium hello **konfiguracji** bloku, wybierz opcję **sieci wirtualnych**.
6. Na powitania **sieci wirtualnych** bloku, wyświetlić listę sieci wirtualne skonfigurowane dla hello bieżącym laboratorium, a także hello domyślną sieć wirtualna, która jest tworzona dla laboratorium. 
7. Wybierz **+ Dodaj**.
   
    ![Dodaj istniejącego laboratorium tooyour sieci wirtualnej](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. Na powitania **sieci wirtualnej** bloku, wybierz opcję **[Wybierz sieć wirtualną]**.
   
    ![Wybierz istniejącą sieć wirtualną](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. Na powitania **sieci wirtualnej wybierz** bloku, wybierz hello żądanej sieci wirtualnej. Hello bloku pokazuje wszystkie sieci wirtualne hello, które są w obszarze hello sam region w subskrypcji hello jako hello laboratorium.  
10. Po wybraniu sieci wirtualnej, są zwracane toohello **sieci wirtualnej** kliknij podsieci hello liście hello u dołu hello hello bloku.

    ![Lista podsieci](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    Blok podsieci laboratorium Hello jest wyświetlany.

    ![Blok podsieci laboratorium](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Określ **Nazwa podsieci laboratorium**.
12. Wybierz tooallow toobe podsieci, używane w laboratorium tworzenia maszyny Wirtualnej, **używany podczas tworzenia maszyny wirtualnej**.
13. tooenable [udostępnionych publicznego adresu IP](devtest-lab-shared-ip.md), wybierz pozycję **Włącz udostępnione publicznego adresu IP**.
14. Wybierz tooallow publicznych adresów IP w podsieci, **pozwala publicznego adresu IP tworzenie**.
15. W hello **maksymalna maszyn wirtualnych dla użytkownika** Określ hello maksymalną maszyn wirtualnych dla poszczególnych użytkowników, dla każdej podsieci. Jeśli chcesz nieograniczoną liczbę maszyn wirtualnych, pozostaw to pole puste.
16. Wybierz **OK** tooclose hello podsieci laboratorium bloku.
17. Wybierz **zapisać** bloku sieci wirtualnej hello tooclose.
18. Teraz, gdy hello sieci wirtualnej jest skonfigurowany, można wybrać podczas tworzenia maszyny Wirtualnej. 
    toosee jak toocreate maszyny Wirtualnej i określ sieć wirtualną, zobacz artykuł toohello [dodać maszyny Wirtualnej z laboratorium tooa artefakty](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Następne kroki
Po dodaniu hello potrzeby sieci wirtualnej laboratorium tooyour hello następnym krokiem jest zbyt[Dodawanie maszyny Wirtualnej laboratorium tooyour](devtest-lab-add-vm-with-artifacts.md).

