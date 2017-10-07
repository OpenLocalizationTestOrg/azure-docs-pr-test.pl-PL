---
title: "aaaMultiple adresów IP dla maszyn wirtualnych platformy Azure - Portal | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP tooa maszynę wirtualną przy użyciu hello portalu Azure | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Przypisz maszyn toovirtual adresów IP w wielu przy użyciu hello portalu Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
W tym artykule opisano, jak toocreate maszynę wirtualną (VM) za pośrednictwem hello Azure Resource Manager deployment model przy użyciu hello portalu Azure. Wiele adresów IP nie można przypisać tooresources został utworzony za pomocą hello klasycznego modelu wdrażania. więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP

Jeśli chcesz toocreate maszyny Wirtualnej z wielu adresów IP lub statycznego prywatnego adresu IP, należy utworzyć ją przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure hello. Jak kliknij hello programu PowerShell lub interfejsu wiersza polecenia Opcje u góry hello toolearn tego artykułu. Można utworzyć Maszynę wirtualną z jednego dynamicznego prywatnego adresu IP i (opcjonalnie) jeden publiczny adres IP za pomocą portalu hello, wykonując następujące kroki hello hello [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) lub [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-portal.md) artykuły. Po utworzeniu hello maszyny Wirtualnej, można zmienić typu adresu IP hello z dynamicznego toostatic i dodawania dodatkowych adresów IP przy użyciu portalu hello, wykonując kroki w hello [tooa maszyn wirtualnych adresów IP dodać](#add) sekcji tego artykułu.

## <a name="add"></a>Dodaj tooa adresów IP maszyny Wirtualnej

Wykonując kroki hello, które należy wykonać, można dodać prywatnych i publicznych tooa adresy IP karty Sieciowej. Witaj przykłady w hello następujące sekcje założono, że już istnieje Maszynę wirtualną z konfiguracji adresów IP hello trzech opisanych w hello [scenariusza](#Scenario) w tym artykule, ale nie jest to wymagane wykonanie.

### <a name="coreadd"></a>Podstawowe kroki

1. Przeglądaj toohello portalu Azure w https://portal.azure.com i zaloguj do niego, jeśli to konieczne.
2. W portalu powitania kliknij **więcej usług** > typ *maszyn wirtualnych* w hello pola filtru, a następnie kliknij przycisk **maszyn wirtualnych**.
3. W hello **maszyn wirtualnych** bloku, kliknij przycisk hello maszyna wirtualna ma tooadd IP adresów do. Kliknij przycisk **interfejsy sieciowe** w wyświetlonym bloku maszyny wirtualnej hello oraz sieci a następnie wybierz pozycję hello interfejsu mają tooadd hello IP adresów do. W przykładzie hello w hello poniższej ilustracji, hello karty Sieciowej o nazwie *myNIC* z hello maszyny Wirtualnej o nazwie *myVM* wybrano:

    ![Interfejs sieciowy](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. W hello wyświetlonym bloku dla hello należy wybrać kartę Sieciową, kliknij przycisk **konfiguracje adresów IP**.

Zakończenie hello kroków w jednej z kolejnych sekcjach hello, na podstawie typu hello adresu IP ma tooadd.

### <a name="add-a-private-ip-address"></a>**Dodaj prywatnego adresu IP**

Wykonaj hello następujące kroki tooadd prywatny adres IP:

1. Zakończenie hello etapami hello [podstawowe kroki](#coreadd) sekcji tego artykułu.
2. Kliknij pozycję **Dodaj**. W hello **konfiguracji IP dodać** bloku, zostanie wyświetlone, utworzyć konfigurację IP o nazwie *IPConfig 4* z *10.0.0.7* jako *statycznych* prywatnego adresu IP adresów, a następnie kliknij przycisk **OK**.

    > [!NOTE]
    > Podczas dodawania statycznego adresu IP, należy określić nieużywanych, prawidłowy adres na powitania hello podsieci, karta sieciowa jest połączona z. Jeśli adres hello, którą wybierzesz nie jest dostępny, hello portalu zostaną wyświetlone X hello adresu IP, a będziesz potrzebować tooselect innego.

3. Po kliknięciu przycisku OK spowoduje zamknięcie bloku hello i zobaczysz hello nowej konfiguracji IP na liście. Kliknij przycisk **OK** tooclose hello **konfiguracji IP dodać** bloku.
4. Możesz kliknąć **Dodaj** tooadd dodatkowe konfiguracje adresów IP, lub zamknij wszystkie otwarte bloków toofinish dodawanie adresów IP.
5. Dodaj hello prywatnego adresu IP dotyczy systemu operacyjnego maszyny Wirtualnej toohello, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.

### <a name="add-a-public-ip-address"></a>Dodaj publiczny adres IP

Publiczny adres IP jest dodawany przez skojarzenie publicznego tooeither zasobów adresu IP nowej konfiguracji IP lub istniejącej konfiguracji adresu IP.

> [!NOTE]
> Publiczne adresy IP ma nominalnego opłatą. więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.
> 

### <a name="create-public-ip"></a>Utwórz zasób publicznego adresu IP

Publiczny adres IP jest jedno ustawienie zasobu publicznego adresu IP. Jeśli masz zasobu publicznego adresu IP, który nie jest obecnie skojarzony tooan konfigurację adresu IP, który ma konfiguracji adresów IP tooan tooassociate, Pomiń hello następujące kroki i czynności hello w jednym z hello kolejnych sekcjach, ile potrzebujesz. Jeśli nie masz dostępnych zasób publicznego adresu IP, wykonaj powitania po toocreate kroki, co:

1. Przeglądaj toohello portalu Azure w https://portal.azure.com i zaloguj do niego, jeśli to konieczne.
3. W portalu powitania kliknij **nowy** > **sieci** > **publicznego adresu IP**.
4. W hello **tworzenie publicznego adresu IP** bloku, zostanie wyświetlone, wprowadź **nazwa**, wybierz pozycję **przypisywania adresów IP** typu **subskrypcji**, **Grupy zasobów**, a **lokalizacji**, następnie kliknij przycisk **Utwórz**, jak pokazano na poniższej ilustracji hello:

    ![Utwórz zasób publicznego adresu IP](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Pełne hello kroków w jednym z hello sekcjach tooassociate hello publicznej konfiguracji adresu IP zasobu tooan IP.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Skojarz hello publicznej konfiguracji adresu IP zasobu tooa nowego adresu IP

1. Zakończenie hello etapami hello [podstawowe kroki](#coreadd) sekcji tego artykułu.
2. Kliknij pozycję **Dodaj**. W hello **konfiguracji IP dodać** bloku, zostanie wyświetlone, utworzyć konfigurację IP o nazwie *IPConfig 4*. Włącz hello **publicznego adresu IP** i wybierz istniejący, dostępne publicznego zasobu adresu IP z hello **wybierz publiczny adres IP** wyświetlonym bloku.

    Po wybraniu hello zasobu publicznego adresu IP, kliknij przycisk **OK** i bloku hello zostanie zamknięte. Jeśli nie masz istniejącego publicznego adresu IP, możesz utworzyć jedną, wykonując kroki hello hello [Utwórz zasób publiczny adres IP](#create-public-ip) sekcji tego artykułu. 

3. Przejrzyj hello nową konfigurację IP. Mimo że jawnie nie został przypisany prywatny adres IP, co zostało automatycznie przypisany toohello konfiguracji adresów IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP.
4. Możesz kliknąć **Dodaj** tooadd dodatkowe konfiguracje adresów IP, lub zamknij wszystkie otwarte bloków toofinish dodawanie adresów IP.
5. Dodaj hello prywatnego adresu IP adres toohello maszyny Wirtualnej systemu operacyjnego, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP address toohello systemu operacyjnego.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Skojarz hello publicznej konfiguracji adresu IP zasobu tooan istniejącego adresu IP

1. Zakończenie hello etapami hello [podstawowe kroki](#coreadd) sekcji tego artykułu.
2. Kliknij pozycję konfiguracji adresu IP hello ma tooadd hello publicznego adresu IP adres zasób.
3. W bloku IPConfig hello jest wyświetlana, kliknij **adres IP**.
4. W hello **wybierz publiczny adres IP** bloku, zostanie wyświetlone, wybierz publiczny adres IP.
5. Kliknij przycisk **zapisać** i bloki hello zostanie zamknięte. Jeśli nie masz istniejącego publicznego adresu IP, możesz utworzyć jedną, wykonując kroki hello hello [Utwórz zasób publiczny adres IP](#create-public-ip) sekcji tego artykułu.
3. Przejrzyj hello nową konfigurację IP.
4. Możesz kliknąć **Dodaj** tooadd dodatkowe konfiguracje adresów IP, lub zamknij wszystkie otwarte bloków toofinish dodawanie adresów IP. Nie należy dodawać hello publicznego adresu IP address toohello systemu operacyjnego.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
