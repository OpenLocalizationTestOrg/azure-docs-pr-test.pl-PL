---
title: "Usług domenowych Azure Active Directory: Wprowadzenie | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu portalu Azure (wersja zapoznawcza)"
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
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a>Włączanie usługi Azure Active Directory Domain Services przy użyciu portalu Azure (wersja zapoznawcza)


## <a name="before-you-begin"></a>Przed rozpoczęciem
Zapoznaj się z tematem [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md) (Zagadnienia dotyczące sieci w usłudze Azure Active Directory Domain Services).


## <a name="task-2-configure-network-settings"></a>Zadanie 2: Konfigurowanie ustawień sieciowych
Następne zadanie konfiguracji to aby utworzyć sieć wirtualną platformy Azure i dedykowanych podsieci w niej. Usługi Azure Active Directory Domain Services w tej podsieci możesz włączyć w sieci wirtualnej. Może również wybierają istniejącej sieci wirtualnej i Utwórz dedykowane podsieć w niej.

1. Kliknij przycisk **sieci wirtualnej** do wybrania sieci wirtualnej.
2. Na **sieci wirtualnej wybierz** bloku, zobacz wszystkie istniejące sieci wirtualne. Zostanie wyświetlony tylko sieci wirtualnych, które należą do grupy zasobów i lokalizacja platformy Azure, wybranego na **podstawy** strony kreatora.

3. Wybierz sieć wirtualną, w którym można włączyć usługi domenowe Azure AD. Kliknij przycisk **Utwórz nowy**, aby utworzyć nową sieć wirtualną. Zdecydowanie zaleca się za pomocą dedykowanego podsieci dla usług domenowych Azure AD. W przypadku wybrania istniejącej sieci wirtualnej, [Utwórz dedykowane podsieć przy użyciu rozszerzenia sieci wirtualnych](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , a następnie wybierz tej podsieci. 

    ![Wybierz sieć wirtualną](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Kliknij przycisk **podsieci** pobrania dedykowanych podsieci w tej sieci wirtualnej, w którym można włączyć nowe domeny zarządzanej. W **Utwórz podsieć** bloku, określ nazwę dla tej podsieci, a następnie kliknij przycisk **OK** po zakończeniu. Na przykład utworzyć podsieć o nazwie "DomainServices", dzięki czemu można łatwo dla innych administratorów zrozumieć, co jest wdrażana w obrębie podsieci.

    ![Wybierz podsieć w sieci wirtualnej](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Wskazówki dotyczące wybierania podsieci**
  > 1. Użyj dedykowanych podsieci dla usług domenowych Azure AD. Nie należy wdrażać innych maszyn wirtualnych do tej podsieci. Ta konfiguracja umożliwia konfigurowanie grup zabezpieczeń sieci (NSG) dla maszyn wirtualnych/obciążeń bez przerywania Twojej domeny zarządzanej. Aby uzyskać więcej informacji, zobacz [sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Nie zaznaczaj podsieci bramy do wdrażania usług domenowych Azure AD, ponieważ nie jest obsługiwana konfiguracja.
  3. Upewnij się, że wybrane podsieci ma wystarczającą ilość miejsca dostępnego adresu — co najmniej 3 – 5 dostępnych adresów IP.
  >

5. Gdy wszystko będzie gotowe, kliknij przycisk **OK** można przenieść do **grupy administratorów** stronie kreatora.


## <a name="next-step"></a>Następny krok
[Zadanie 3: Konfigurowanie grupy administracyjnej i włączyć usługi domenowe Azure AD](active-directory-ds-getting-started-admingroup.md)
