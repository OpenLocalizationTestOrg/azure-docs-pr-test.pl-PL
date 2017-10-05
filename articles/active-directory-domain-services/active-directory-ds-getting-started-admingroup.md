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
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a>Włączanie usługi Azure Active Directory Domain Services przy użyciu portalu Azure (wersja zapoznawcza)


## <a name="task-3-configure-administrative-group"></a>Zadanie 3: Konfigurowanie grupy administracyjnej
W tym zadaniu konfiguracji grupy administracyjnej tworzenia w katalogu usługi Azure AD. Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*. Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny do domeny zarządzanej. Na komputerach przyłączonych do domeny ta grupa jest dodawane do grupy Administratorzy. Ponadto Członkowie tej grupy służy pulpitu zdalnego do łączności zdalnej dla komputerów przyłączonych do domeny.

> [!NOTE]
> Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services. W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę i nie są udostępniane użytkownikom w ramach dzierżawy. Jednak można użyć specjalnej grupy administracyjne utworzone w ramach tego zadania konfiguracji można wykonać pewne operacje uprzywilejowane. Tych operacji zalicza się przyłączanie komputerów do domeny, należą do tej grupy administracyjnej na komputerach przyłączonych do domeny i konfigurowania zasad grupy.
>

Kreator automatycznie tworzy grupy administracyjnej w katalogu usługi Azure AD. Ta grupa jest nazywany "Administratorzy usługi AAD kontrolera domeny". Jeśli istnieje już grupa o tej nazwie w katalogu usługi Azure AD, Kreator wybierze tej grupy. Można skonfigurować przy użyciu członkostwa w grupie **grupy administratorów** strony kreatora.

1. Kliknij, aby skonfigurować członkostwo w grupie **Administratorzy kontrolera domeny usługi AAD**.

    ![Konfigurowanie członkostwa w grupie](./media/getting-started/domain-services-blade-admingroup.png)

2. Kliknij przycisk **dodawać członków** przycisk, aby dodać użytkowników z katalogu usługi Azure AD do grupy administratorów.

3. Gdy wszystko będzie gotowe, kliknij przycisk **OK** można przenieść do **Podsumowanie** stronie kreatora.

4. Na **Podsumowanie** strony kreatora należy przejrzeć ustawienia konfiguracji dla domeny zarządzanej. Można przejść wstecz do dowolnego kroku kreatora, aby wprowadzić zmiany, jeśli to konieczne. Gdy wszystko będzie gotowe, kliknij przycisk **OK** do utworzenia nowej domeny zarządzanej.

    ![Podsumowanie](./media/getting-started/domain-services-blade-summary.png)

5. Zostanie wyświetlone powiadomienie, że będzie wyświetlany postęp wdrażania usług domenowych Azure AD. Kliknij powiadomienie, aby wyświetlić szczegółowe informacje o postępie dla wdrożenia.

    ![Powiadomienie — wdrożenie w toku](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Zapewnij domeny zarządzanej
Proces inicjowania obsługi administracyjnej domeny zarządzanej może potrwać do godziny.

1. Gdy wdrożenie jest w toku, możesz wyszukać "usługi domeny", w **wyszukiwania zasobów** pola wyszukiwania. Wybierz **usług domenowych Azure AD** z wyników wyszukiwania. **Usług domenowych Azure AD** bloku wymieniono domeny zarządzanej, która jest inicjowana.

    ![Znajdź zainicjowanie obsługi domeny zarządzanej](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Kliknij nazwę domeny zarządzanej (na przykład "contoso100.com"), aby zobaczyć więcej szczegółów dotyczących domeny.

    ![Usług domenowych — stan inicjowania obsługi](./media/getting-started/domain-services-provisioning-state.png)

3. **Omówienie** kartę pokazuje, że domena jest aktualnie aprowizowany. Nie można skonfigurować domeny zarządzanej, dopóki nie jest w pełni zaaprowizowanym. Może potrwać do godziny dla domeny zarządzanej być w pełni obsługiwany.

    ![Usługi domenowe — karta Przegląd w stanie inicjowania obsługi administracyjnej ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Gdy domeny zarządzanej jest w pełni zaaprowizowanym, **omówienie** stan wyświetlany na karcie domeny jako **systemem**.

    ![Usługi Domain Services — karta Przegląd po pełnej aprowizacji](./media/getting-started/domain-services-provisioned.png)

5. Na **właściwości** kartę, zobacz dwa adresy IP, w której domeny kontrolery są dostępne dla sieci wirtualnej.

    ![Usługi domenowe — karta właściwości po w pełni zaaprowizowanym](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Następny krok
[Zadanie 4. Aktualizowanie ustawień usługi DNS dla sieci wirtualnej platformy Azure](active-directory-ds-getting-started-dns.md)
