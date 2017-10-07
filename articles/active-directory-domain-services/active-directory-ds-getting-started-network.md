---
title: "Usług domenowych Azure Active Directory: Wprowadzenie | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)


## <a name="before-you-begin"></a>Przed rozpoczęciem
Odwołuje się zbyt[sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Zadanie 2: Konfigurowanie ustawień sieciowych
następne zadanie konfiguracji Hello jest toocreate sieci wirtualnej platformy Azure i dedykowanych podsieci w niej. Usługi Azure Active Directory Domain Services w tej podsieci możesz włączyć w sieci wirtualnej. Może również wybierają istniejącej sieci wirtualnej i Utwórz podsieć hello dedykowanego w niej.

1. Kliknij przycisk **sieci wirtualnej** tooselect sieci wirtualnej.
2. Na powitania **sieci wirtualnej wybierz** bloku, zobacz wszystkie istniejące sieci wirtualne. Zostanie wyświetlony tylko hello sieci wirtualne, które należy toohello lokalizacji i grupy zasobów platformy Azure wybranego na powitania **podstawy** strony kreatora.

3. Wybierz sieć wirtualną hello, w którym można włączyć usługi domenowe Azure AD. Kliknij przycisk **Utwórz nowy**, jeśli wolisz toocreate nowej sieci wirtualnej. Zdecydowanie zaleca się za pomocą dedykowanego podsieci dla usług domenowych Azure AD. W przypadku wybrania istniejącej sieci wirtualnej, [Utwórz dedykowane podsieć przy użyciu rozszerzenia sieci wirtualnych hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , a następnie wybierz tej podsieci. 

    ![Wybierz sieć wirtualną](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Kliknij przycisk **podsieci** toopick hello dedykowanych podsieci w tej sieci wirtualnej w ramach których tooenable nowego zarządzanego domeny. W hello **Utwórz podsieć** bloku, określ nazwę hello podsieci, a następnie kliknij przycisk **OK** po zakończeniu. Na przykład utworzyć podsieć o nazwie hello "DomainServices", dzięki czemu toounderstand innych administratorów co to jest wdrażana w obrębie podsieci hello.

    ![Wybierz podsieć w sieci wirtualnej hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Wskazówki dotyczące wybierania podsieci**
  > 1. Użyj dedykowanych podsieci dla usług domenowych Azure AD. Nie należy wdrażać innych podsieci toothis maszyn wirtualnych. Taka konfiguracja pozwala tooconfigure sieciowych grup zabezpieczeń (NSG) dla maszyn wirtualnych/obciążeń bez przerywania Twojej domeny zarządzanej. Aby uzyskać więcej informacji, zobacz [sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Nie zaznaczaj hello podsieci bramy do wdrażania usług domenowych Azure AD, ponieważ nie jest obsługiwana konfiguracja.
  3. Upewnij się, że wybrane podsieci hello jest wystarczająca ilość miejsca dostępnego adresu — co najmniej 3 – 5 dostępnych adresów IP.
  >

5. Gdy wszystko będzie gotowe, kliknij przycisk **OK** toomove na toohello **grupy administratorów** hello kreatora.


## <a name="next-step"></a>Następny krok
[Zadanie 3: Konfigurowanie grupy administracyjnej i włączyć usługi domenowe Azure AD](active-directory-ds-getting-started-admingroup.md)
