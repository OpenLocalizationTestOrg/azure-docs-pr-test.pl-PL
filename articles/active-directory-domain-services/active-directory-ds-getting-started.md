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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)
W tym artykule opisano, jak tooenable Azure usług domenowych Active Directory (Azure AD DS) za pomocą hello portalu Azure.


Witaj toolaunch **usług włączyć domenowych Azure AD** pełną, Kreator hello następujące kroki:

1. Przejdź toohello [portalu Azure](https://portal.azure.com).
2. W okienku po lewej stronie powitania kliknij **nowy**.
3. W hello **nowy** bloku, typ **usług domenowych w usłudze** na powitania pasek wyszukiwania.

    ![Wyszukaj usług domenowych w usłudze](./media/getting-started/search-domain-services.png)

4. Kliknij przycisk tooselect **usług domenowych Azure AD** z listy hello sugestie dotyczące wyszukiwania. Na powitania **usług domenowych Azure AD** bloku, kliknij przycisk hello **Utwórz** przycisku.

    ![Blok usług domenowych](./media/getting-started/domain-services-blade.png)

5. Witaj **usług włączyć domenowych Azure AD** uruchomić kreatora.


## <a name="task-1-configure-basic-settings"></a>Zadanie 1: Konfigurowanie ustawień podstawowych
W hello **podstawy** strony kreatora hello, można określić hello domeny DNS dla domeny zarządzanej hello. Możesz również hello grupy zasobów i powinny zostać wdrożone domeny zarządzanej hello toowhich lokalizacji platformy Azure.

![Skonfiguruj podstawy](./media/getting-started/domain-services-blade-basics.png)

1. Wybierz hello **nazwy domeny DNS** dla domeny zarządzanej.

   * Domyślna nazwa domeny Hello hello katalogu (z **. onmicrosoft.com** sufiks) jest określony, domyślnie.

   * Możesz również wpisać w niestandardowej nazwy domeny. W tym przykładzie hello niestandardowa nazwa domeny jest *contoso100.com*.

     > [!WARNING]
     > Prefiks nazwy domeny określonej Hello (na przykład *contoso100* w hello *contoso100.com* nazwa domeny) musi zawierać więcej niż 15 znaków. Nie można utworzyć domeny zarządzanej z prefiksem dłuższa niż 15 znaków.
     >
     >

2. Upewnij się, tym hello domeny DNS wybrana dla hello zarządzane domeny nie istnieje już w sieci wirtualnej hello. W szczególności, sprawdź, czy:

   * Masz już domenę z hello tą samą nazwą domeny DNS w sieci wirtualnej hello.

   * Hello sieci wirtualnej, w którym planujesz domeny zarządzanej hello tooenable ma połączenie VPN z siecią lokalną. W tym scenariuszu, upewnij się, nie masz domenę z hello tą samą nazwą domeny DNS w sieci lokalnej.

   * Masz istniejącą usługę w chmurze o tej nazwie na powitania sieci wirtualnej.

3. Wybierz hello **sieć wirtualna typu**. Domyślnie program hello **Resource Manager** wybrano typ sieci wirtualnej. Zaleca się używanie tego typu sieci wirtualnej dla wszystkich nowo utworzony domen zarządzanych.

4. Wybierz hello Azure **subskrypcji** w którym chcesz domeny zarządzanej hello toocreate.

5. Wybierz hello **grupy zasobów** domeny zarządzanej hello toowhich powinna należeć. Można wybrać obu hello **Utwórz nowy** lub **Użyj istniejącego** grupy zasobów hello tooselect opcje.

6. Wybierz hello Azure **lokalizacji** w hello, które można utworzyć domeny zarządzanej. Na powitania **sieci** strony kreatora hello Zobacz sieci tylko wirtualne, które należy lokalizacji toohello wybrano.

7. Gdy wszystko będzie gotowe, kliknij przycisk **OK** toomove na toohello **sieci** hello kreatora.


## <a name="next-step"></a>Następny krok
[Task 2: configure network settings (Zadanie 2. Konfigurowanie ustawień sieciowych)](active-directory-ds-getting-started-network.md)
