---
title: 'Azure Active Directory Domain Services: Tworzenie lub wybieranie sieci wirtualnej | Microsoft Docs'
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Tworzenie lub wybieranie sieci wirtualnej dla usługi Azure Active Directory Domain Services
## <a name="before-you-begin"></a>Przed rozpoczęciem
Odwołuje się zbyt[sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Zadanie 2. Tworzenie sieci wirtualnej platformy Azure
następne zadanie konfiguracji Hello jest toocreate sieci wirtualnej platformy Azure i podsieci w niej. Usługi Azure Active Directory Domain Services w tej podsieci możesz włączyć w sieci wirtualnej. Jeśli masz istniejącą sieć wirtualną wolisz toouse, możesz pominąć ten krok.

> [!NOTE]
> Upewnij się, że hello Azure sieci wirtualnej, Utwórz lub wybierz toouse z usług domenowych Azure Active Directory należy tooan region platformy Azure, który jest obsługiwany przez usługi Azure Active Directory Domain Services. tooascertain hello regiony platformy Azure, w których jest dostępna usług domenowych Azure Active Directory, zobacz [usług Azure według regionu](https://azure.microsoft.com/regions/#services/).
>
>Zanotuj nazwę hello hello tooensure sieci wirtualnej, wybierz hello właściwą sieć, po włączeniu usług domenowych Azure Active Directory w kolejnym kroku konfiguracji.


toocreate sieci wirtualnej platformy Azure w której ma zostać tooenable Azure Active Directory Domain Services, wykonaj te instrukcje konfiguracji:

1. Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Wybierz w okienku po lewej stronie powitania **sieci**.

    ![Węzeł sieci](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Witaj **sieci wirtualnych** zostanie otwarte okno.
3. W okienku zadań hello u dołu okna hello powitania kliknij **nowy**.

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. Kliknij opcję **Usługi sieciowe**, a następnie wybierz pozycję **Sieć wirtualna**.

    ![Sieć wirtualna — szybkie tworzenie](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. toocreate sieci wirtualnej, kliknij przycisk **szybkie tworzenie**.

6. Określ **nazwa** dla wirtualnej sieci i rozważyć następujący hello:
    * Możesz wybrać tooconfigure **przestrzeni adresów** lub **maksymalna liczba maszyn wirtualnych** dla tej sieci.
    * Możesz pozostawić hello **serwera DNS** ustawienie jako **Brak** teraz. Należy zaktualizować ustawienia hello, po włączeniu usług domenowych Azure Active Directory.
7. W hello **lokalizacji** listy rozwijanej wybierz obsługiwany region platformy Azure.  
    tooascertain hello regiony platformy Azure, w których jest dostępna usług domenowych Azure Active Directory, zobacz [usług Azure według regionu](https://azure.microsoft.com/regions/#services/).
8. toocreate sieci wirtualnej, kliknij przycisk **utworzyć sieć wirtualną**.

    ![Tworzenie sieci wirtualnej dla usługi Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. Po utworzeniu sieci wirtualnej, wybierz nazwę hello hello sieci wirtualnej, a następnie kliknij hello **Konfiguruj** kartę.

    ![Tworzenie podsieci](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. W obszarze **przestrzeniami adresów sieci wirtualnej**, kliknij przycisk **Dodaj podsieć**, a następnie określ podsieć o nazwie hello **AaddsSubnet**.

    ![Tworzenie podsieci dla usługi Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate hello podsieci, kliknij przycisk **zapisać**.


## <a name="next-step"></a>Następny krok
[Zadanie 3. Włączanie usług Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)
