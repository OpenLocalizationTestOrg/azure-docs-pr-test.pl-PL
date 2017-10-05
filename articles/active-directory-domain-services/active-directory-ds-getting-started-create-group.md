---
title: "Azure Active Directory Domain Services: Utwórz grupę Administratorzy kontrolerów domeny usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Włączanie usług Azure Active Directory Domain Services przy użyciu klasycznej witryny Azure Portal"
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
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a>Włączanie usług Azure Active Directory Domain Services przy użyciu klasycznej witryny Azure Portal
W tym artykule opisano i przedstawiono zadania konfiguracji, które są wymagane, aby włączyć usługi Azure Active Directory Domain Services (Azure AD DS) dla dzierżawy usługi Azure Active Directory (Azure AD).

> [!NOTE]
> [**Zamiast tego spróbuj nowe środowisko portalu Azure (wersja zapoznawcza)**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a>Zadanie 1: Tworzenie grupy administratorów usługi Azure AD kontrolera domeny.
Pierwszym zadaniem jest tworzenie grupy administracyjnej w dzierżawie usługi Azure AD. Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*. Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny w domenie zarządzanych usług domenowych Azure Active Directory. Na komputerach przyłączonych do domeny ta grupa jest dodawane do grupy Administratorzy. Ponadto Członkowie tej grupy służy pulpitu zdalnego do łączności zdalnej dla komputerów przyłączonych do domeny.  

> [!NOTE]
> Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services. W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę i nie są udostępniane użytkownikom w ramach dzierżawy. Jednak można użyć specjalnej grupy administracyjne utworzone w ramach tego zadania konfiguracji można wykonać pewne operacje uprzywilejowane. Tych operacji zalicza się przyłączanie komputerów do domeny, należą do tej grupy administracyjnej na komputerach przyłączonych do domeny i konfigurowania zasad grupy.
>

W tym zadaniu konfiguracji tworzenia grupy administracyjnej i Dodaj jeden lub więcej użytkowników w katalogu do grupy. Aby utworzyć grupy administracyjnej dla usługi Azure Active Directory Domain Services, wykonaj następujące czynności:

1. Przejdź do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).
2. W lewym okienku wybierz przycisk **Active Directory**.
3. Wybierz dzierżawę usługi Azure AD (katalog), dla którego chcesz włączyć usługi Azure Active Directory Domain Services. Można utworzyć tylko jedną domenę dla każdego katalogu usługi Azure AD.

    ![Wybierz katalog usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Na **katalogu podglądu** kliknij przycisk **grup** kartę.
5. Aby dodać grupę do dzierżawy usługi Azure AD, w okienku zadań w dolnej części okna kliknij **Dodaj grupę**.

    ![Przycisk Dodaj grupę](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. W **Dodaj grupę** okna dialogowego Utwórz grupę o nazwie **Administratorzy kontrolera domeny usługi AAD**, a następnie ustaw **typ grupy** do **zabezpieczeń**.

   > [!WARNING]
   > Aby włączyć dostęp w swojej domenie zarządzanych usług domenowych Azure Active Directory, należy utworzyć grupę o tej nazwie dokładne.
   >
   >

    ![Okno dialogowe Dodawanie grupy](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. W **opis** wprowadź opis, który umożliwia użytkownikom zrozumienie, że ta grupa przyznaje uprawnienia administracyjne w ramach usług domenowych Azure Active Directory.
8. Po utworzeniu grupy, kliknij nazwę grupy, aby wyświetlić jego właściwości.
9. Aby dodać użytkowników jako członków grupy, w dolnej części okna kliknij pozycję **Dodaj członków** przycisku.

    ![Dodawanie przycisku członków grupy](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. W **dodawać członków** oknie dialogowym Wybierz użytkowników, którzy powinny być członkami tej grupy, a następnie kliknij ikonę znacznika wyboru w prawej dolnej części strony.

    ![Dodawanie użytkowników do grupy administratorów](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Następny krok
[Zadanie 2: Tworzenie lub Wybieranie sieci wirtualnej platformy Azure](active-directory-ds-getting-started-vnet.md)
