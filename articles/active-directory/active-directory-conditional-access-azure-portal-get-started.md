---
title: "aaaGet korzystania z dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Testowanie dostępu warunkowego za pomocą warunku lokalizacji."
services: active-directory
keywords: "tooapps dostępu warunkowego, dostępu warunkowego z usługą Azure AD, bezpieczny dostęp do zasobów toocompany, zasady dostępu warunkowego"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Rozpoczynanie pracy z dostępu warunkowego w usłudze Azure Active Directory

Dostęp warunkowy jest możliwość usługi Azure Active Directory, umożliwiającą możesz toodefine warunki na jakich autoryzowani użytkownicy mają dostęp do Twojej aplikacji. 

Ten temat zawiera instrukcje dotyczące testowania dostępu warunkowego na podstawie warunku lokalizacji w danym środowisku.  


## <a name="scenario-description"></a>Opis scenariusza

Jednym z typowych wymagań w wielu organizacjach jest tooonly wymusić uwierzytelnianie wieloskładnikowe dla tooapps dostępu, który nie jest wykonywane z hello firmowego intranetu. Z usługą Azure Active Directory można łatwo realizację tego celu, konfigurując zasady dostępu warunkowego na podstawie lokalizacji. W tym temacie przedstawiono szczegółowe instrukcje dotyczące konfigurowania pokrewnych zasad. Witaj wykorzystanie zasad [zaufanych adresów IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish między próbami dostępu z firmowej hello na wszystkich innych lokalizacji w intranecie i.


## <a name="prerequisites"></a>Wymagania wstępne

Hello scenariusz opisany w tym temacie przyjęto założenie, że znasz hello pojęcia opisane w [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).

tootest tego scenariusza należy:

- Tworzenie użytkownika testowego 

- Przypisz użytkownika testowego toohello licencji Azure AD Premium

- Konfigurowanie zarządzanych aplikacji i przypisz użytkownika tooit użytkownika testowego

- Skonfiguruj listę zaufanych adresów IP

Aby uzyskać więcej informacji na temat zaufanych adresów IP, zobacz [zaufanych adresów IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>Kroki konfiguracji zasad

**tooconfigure zasady dostępu warunkowego, czy:**

1. W portalu Azure na lewy pasek nawigacyjny hello hello kliknij **usługi Azure Active Directory**. 

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. Na powitania **usługi Azure Active Directory** bloku w hello **Zarządzaj** kliknij **dostępu warunkowego**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. Na powitania **dostępu warunkowego** bloku, tooopen hello **nowy** bloku na powitania narzędzi u góry hello kliknij **Dodaj**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. Na powitania **nowy** bloku w hello **nazwa** tekstowym, wpisz nazwę zasady.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. W hello **przypisania** kliknij **użytkowników i grup**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. Na powitania **użytkowników i grup** blok, wykonaj następujące kroki hello:

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. Kliknij przycisk **Wybierz użytkowników i grupy**.

    b. Kliknij pozycję **Wybierz**.

    c. Na powitania **wybierz** bloku, wybierz użytkownika testowego, a następnie kliknij przycisk **wybierz**.

    d. Na powitania **użytkowników i grup** bloku, kliknij przycisk **gotowe**.

7. Na powitania **nowy** bloku, tooopen hello **aplikacji w chmurze** bloku w hello **przypisania** kliknij **aplikacji w chmurze**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. Na powitania **aplikacji w chmurze** blok, wykonaj następujące kroki hello:

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. Kliknij przycisk **Wybierz aplikacje**.

    b. Kliknij pozycję **Wybierz**.

    c. Na powitania **wybierz** bloku, wybierz aplikacji w chmurze, a następnie kliknij przycisk **wybierz**.

    d. Na powitania **aplikacji w chmurze** bloku, kliknij przycisk **gotowe**.

9. Na powitania **nowy** bloku, tooopen hello **warunki** bloku w hello **przypisania** kliknij **warunki**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. Na powitania **warunki** bloku, tooopen hello **lokalizacje** bloku, kliknij przycisk **lokalizacje**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. Na powitania **lokalizacje** blok, wykonaj następujące kroki hello:

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. W obszarze **Konfiguruj**, kliknij przycisk **tak**.

    b. W obszarze **Include**, kliknij przycisk **wszystkie lokalizacje**.

    c. Kliknij przycisk **wykluczyć**, a następnie kliknij przycisk **wszystkich zaufanych adresów IP**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. Kliknij przycisk **Gotowe**.

12. Na powitania **warunki** bloku, kliknij przycisk **gotowe**.

13. Na powitania **nowy** bloku, tooopen hello **Grant** bloku w hello **formanty** kliknij **Grant**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. Na powitania **Grant** blok, wykonaj następujące kroki hello:

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. Wybierz **wymusić uwierzytelnianie wieloskładnikowe**.

    b. Kliknij pozycję **Wybierz**.

15. Na powitania **nowy** bloku, w obszarze **Włącz zasady**, kliknij przycisk **na**.

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. Na powitania **nowy** bloku, kliknij przycisk **Utwórz**.


## <a name="testing-hello-policy"></a>Zasady testowania hello

tootest zasad, powinien uzyskiwać dostęp aplikacji z urządzenia który: 

1. Ma adres IP, który mieści się w sieci skonfigurowanych zaufanych adresów IP 

1. Ma adres IP, który nie znajduje się w sieci skonfigurowanych zaufanych adresów IP

Uwierzytelnianie wieloskładnikowe powinny być wymagana tylko podczas próby połączenia zostało utworzone z urządzenia, które nie znajduje się w sieci skonfigurowanych zaufanych adresów IP. 


## <a name="next-steps"></a>Następne kroki

Jeśli chcesz toolearn więcej informacji na temat dostępu warunkowego, zobacz [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).

