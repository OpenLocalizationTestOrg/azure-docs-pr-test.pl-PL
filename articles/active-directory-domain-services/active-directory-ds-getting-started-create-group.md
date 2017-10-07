---
title: "Azure Active Directory Domain Services: Utwórz grupę Administratorzy DC hello Azure AD | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure"
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure
W tym artykule opisano i przedstawiono hello zadania konfiguracyjne, które są wymagane dla Ciebie tooenable Azure usług domenowych Active Directory (Azure AD DS) dla dzierżawy usługi Azure Active Directory (Azure AD).

> [!NOTE]
> [**Zamiast tego spróbuj nowe środowisko portalu hello Azure (wersja zapoznawcza)**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Zadanie 1: Tworzenie grupy Administratorzy DC hello Azure AD
pierwszym zadaniem Hello jest toocreate grupy administracyjnej w dzierżawie usługi Azure AD. Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*. Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny toohello zarządzanych usług domenowych Azure Active Directory domeny. Na komputerach przyłączonych do domeny ta grupa jest dodawana toohello grupy Administratorzy. Ponadto Członkowie tej grupy można użyć maszyny zdalnie przyłączonych toodomain tooconnect pulpitu zdalnego.  

> [!NOTE]
> Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa hello domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services. W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę hello i nie będą dostępne toousers w ramach dzierżawy hello. Można jednak użyć hello specjalnej grupy administracyjne utworzone w tej konfiguracji tooperform zadań niektóre czynności uprzywilejowane. Tych operacji zalicza się dołączenie komputerów domeny toohello, należącego do grupy administracyjnej toohello na komputerach przyłączonych do domeny i konfigurowania zasad grupy.
>

W tym zadaniu konfiguracji tworzenia grupy administracyjnej hello i Dodaj jeden lub więcej użytkowników w grupie toohello katalogu. toocreate hello grupy administracyjnej dla usługi Azure Active Directory Domain Services, hello następujące:

1. Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. W okienku po lewej stronie powitania wybierz hello **usługi Active Directory** przycisku.
3. Wybierz hello dzierżawy usługi Azure AD (katalog) dla której ma zostać tooenable Azure Active Directory Domain Services. Można utworzyć tylko jedną domenę dla każdego katalogu usługi Azure AD.

    ![Wybierz katalog usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Na powitania **katalogu podglądu** kliknij przycisk hello **grup** kartę.
5. Kliknij grupę dzierżawcy tooyour usługi Azure AD, w okienku zadań hello u dołu okna hello hello tooadd **Dodaj grupę**.

    ![przycisk Dodaj grupę Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. W hello **Dodaj grupę** okna dialogowego Utwórz grupę o nazwie **Administratorzy kontrolera domeny usługi AAD**, a następnie ustaw **typ grupy** za**zabezpieczeń**.

   > [!WARNING]
   > tooenable dostępu w swojej domenie zarządzanych usług domenowych Azure Active Directory, utworzyć grupę o tej nazwie dokładne.
   >
   >

    ![okno dialogowe Dodawanie grupy Hello](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. W hello **opis** wprowadź opis, który umożliwia innym toounderstand, że ta grupa przyznaje uprawnienia administracyjne w ramach usług domenowych Azure Active Directory.
8. Po utworzeniu grupy powitania kliknij tooview Nazwa grupy hello jego właściwości.
9. tooadd użytkowników jako członków grupy hello u dołu okna hello powitania kliknij hello **Dodaj członków** przycisku.

    ![Dodawanie przycisku członków grupy](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. W hello **dodawać członków** okno dialogowe hello Wybierz użytkowników, którzy powinny być członkami tej grupy, a następnie kliknij ikonę znacznika wyboru hello na powitania prawy dolny.

    ![Dodaj grupę tooadministrators użytkowników](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Następny krok
[Zadanie 2: Tworzenie lub Wybieranie sieci wirtualnej platformy Azure](active-directory-ds-getting-started-vnet.md)
