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
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)


## <a name="task-3-configure-administrative-group"></a>Zadanie 3: Konfigurowanie grupy administracyjnej
W tym zadaniu konfiguracji grupy administracyjnej tworzenia w katalogu usługi Azure AD. Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*. Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny toohello domeny zarządzanej. Na komputerach przyłączonych do domeny ta grupa jest dodawana toohello grupy Administratorzy. Ponadto Członkowie tej grupy można użyć maszyny zdalnie przyłączonych toodomain tooconnect pulpitu zdalnego.

> [!NOTE]
> Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa hello domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services. W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę hello i nie będą dostępne toousers w ramach dzierżawy hello. Można jednak użyć hello specjalnej grupy administracyjne utworzone w tej konfiguracji tooperform zadań niektóre czynności uprzywilejowane. Tych operacji zalicza się dołączenie komputerów domeny toohello, należącego do grupy administracyjnej toohello na komputerach przyłączonych do domeny i konfigurowania zasad grupy.
>

Witaj Kreator automatycznie tworzy grupy administracyjnej hello w katalogu usługi Azure AD. Ta grupa jest nazywany "Administratorzy usługi AAD kontrolera domeny". Jeśli istnieje już grupa o tej nazwie w katalogu usługi Azure AD, Kreator hello wybiera tej grupy. Można skonfigurować przy użyciu hello członkostwa w grupie **grupy administratorów** strony kreatora.

1. członkostwo w grupie tooconfigure, kliknij przycisk **Administratorzy kontrolera domeny usługi AAD**.

    ![Konfigurowanie członkostwa w grupie](./media/getting-started/domain-services-blade-admingroup.png)

2. Kliknij przycisk hello **dodawać członków** przycisk tooadd użytkowników z grupy administrator toohello katalogu usługi Azure AD.

3. Gdy wszystko będzie gotowe, kliknij przycisk **OK** toomove na toohello **Podsumowanie** hello kreatora.

4. Na powitania **Podsumowanie** hello kreatora przejrzyj ustawienia konfiguracji hello hello domeny zarządzanej. Możesz wrócić krok tooany hello kreatora toomake zmian, jeśli to konieczne. Gdy wszystko będzie gotowe, kliknij przycisk **OK** toocreate hello nowego zarządzanego domeny.

    ![Podsumowanie](./media/getting-started/domain-services-blade-summary.png)

5. Zostanie wyświetlone powiadomienie, że pokazuje hello postęp wdrażania usług domenowych Azure AD. Kliknij powiadomienie hello toosee szczegółowe postępu hello wdrożenia.

    ![Powiadomienie — wdrożenie w toku](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Zapewnij domeny zarządzanej
Proces inicjowania obsługi administracyjnej domeny zarządzanej Hello może potrwać godzinę tooan.

1. Podczas wdrożenia jest w toku, możesz wyszukać frazę "usługi domeny" w hello **wyszukiwania zasobów** pola wyszukiwania. Wybierz **usług domenowych Azure AD** z hello wyników wyszukiwania. Witaj **usług domenowych Azure AD** bloku wymieniono hello domeny zarządzanej, która jest inicjowana.

    ![Znajdź zainicjowanie obsługi domeny zarządzanej](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Kliknij nazwę hello toosee domeny (na przykład "contoso100.com") hello zarządzane więcej szczegółów na temat hello domeny.

    ![Usług domenowych — stan inicjowania obsługi](./media/getting-started/domain-services-provisioning-state.png)

3. Witaj **omówienie** karcie są wyświetlane tej domeny hello jest aktualnie aprowizowany. Nie można skonfigurować hello domeny zarządzanej, dopóki nie jest w pełni zaaprowizowanym. Może potrwać godzinę tooan Twojego toobe domeny zarządzanej, w pełni zaaprowizowanym.

    ![Usługi domenowe — karta Przegląd podczas hello stan inicjowania obsługi ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Gdy domeny zarządzanej hello jest w pełni zaaprowizowanym, hello **omówienie** karta przedstawia stan domen hello jako **systemem**.

    ![Usługi Domain Services — karta Przegląd po pełnej aprowizacji](./media/getting-started/domain-services-provisioned.png)

5. Na powitania **właściwości** kartę, zobacz dwa adresy IP, w której domeny są dostępne dla sieci wirtualnej hello kontrolerów.

    ![Usługi domenowe — karta właściwości po w pełni zaaprowizowanym](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Następny krok
[Zadanie 4: aktualizowanie ustawień DNS hello hello sieci wirtualnej platformy Azure](active-directory-ds-getting-started-dns.md)
