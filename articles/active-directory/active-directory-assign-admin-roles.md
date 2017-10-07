---
title: "aaaAssigning ról administratora w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Rolę administratora może być toocreate używane lub Edytuj użytkowników, Przypisz role administracyjne, resetowanie haseł użytkowników, zarządzanie licencjami użytkowników lub Zarządzanie domenami. Użytkownik, któremu przypisano rolę administratora ma hello te same uprawnienia we wszystkich toowhich usługi w chmurze zostały zasubskrybowane przez organizację."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: b96350c7264e6ad3620272e015ed9756b512dc4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Przypisywanie ról administratorów w usłudze Azure Active Directory
> [!div class="op_single_selector"]
> * [Witryna Azure Portal]()
> * [Klasyczna witryna Azure Portal](active-directory-assign-admin-roles.md)
>
>

Użyj oddzielnych Administratorzy toodesignate usługi Azure Active Directory (Azure AD) dla różnych funkcji. Administratorzy można dostęp do wybranych funkcji hello portalu Azure lub klasycznego portalu Azure i, w zależności od ich roli, zostanie toocreate może być lub Edytuj użytkowników, Przypisz role administracyjne tooothers, resetowanie haseł użytkowników, zarządzanie licencjami użytkowników i zarządzanie domenach, między innymi. Użytkownik, któremu przypisano rolę administratora będzie miał hello we wszystkich toowhich usługi w chmurze hello zostały zasubskrybowane przez organizację, niezależnie od tego, czy przypisanie roli hello w portalu usługi Office 365 hello lub hello klasycznego portalu Azure lub przy użyciu tych samych uprawnień Moduł Hello Azure AD PowerShell firmy Microsoft.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Aby uzyskać jak tooassign ról administratorów w usłudze Azure AD Witaj, Administratorze Centrum, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md).


dostępne są następujące role administratora Hello:

* **Administrator rozliczeń**: dokonuje zakupów, zarządza subskrypcjami, zarządza biletami pomocy technicznej i monitoruje kondycję usługi.

* **Administrator zgodności**: użytkownicy z tą rolą mają uprawnienia zarządzania w ramach hello Office 365 zabezpieczeń & Centrum zgodności i Centrum administracyjnego programu Exchange. Więcej informacji na "[o rolach administratora usługi Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)."

* **Administrator dostępu warunkowego**: użytkownicy z tą rolą mają hello możliwości toomanage usługi Azure Active Directory dostępu warunkowego ustawienia.

* **Administrator programu CRM usługi**: użytkownicy z tą rolą uprawnień globalnych w programie Microsoft CRM Online, gdy usługa hello jest obecny, oraz toomanage możliwości hello bilety obsługi i monitoruje kondycję usługi. Więcej informacji na [ról administratora o usługi Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administratorzy urządzenia**: użytkownicy z tą rolą stają się Administratorzy komputera lokalnego na wszystkich urządzeniach systemu Windows 10, które są przyłączone do tooAzure usługi Active Directory. Nie mają hello możliwości toomanage urządzeń obiektów w usłudze Azure Active Directory.

* **Czytniki katalogu**: jest starszych rolę, która jest tooapplications toobe przypisane, która nie obsługuje hello [Framework zgody](active-directory-integrating-applications.md). Nie powinna mieć przypisanej tooany użytkowników.

* **Konta synchronizacji katalogu**: nie używaj. Ta rola jest automatycznie przypisywana toohello usługi Azure AD Connect usługi i jest nie przeznaczone lub obsługiwane do innego użytku.

* **Składniki zapisywania katalogu**: jest starszych rolę, która jest tooapplications toobe przypisane, która nie obsługuje hello [Framework zgody](active-directory-integrating-applications.md). Nie powinna mieć przypisanej tooany użytkowników.

* **Administrator usługi Exchange**: użytkownicy z tą rolą uprawnień globalnych w programie Microsoft Exchange Online, gdy usługa hello jest obecna. Więcej informacji na [ról administratora o usługi Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrator globalny / Administrator firmy**: użytkownicy z tą rolą ma funkcje administracyjne tooall dostępu w usłudze Azure Active Directory, a także usług tego federate tooAzure usługi Active Directory, takie jak Exchange Online, SharePoint Online i Skype dla firm Online. Witaj osoby, która zarejestruje się dla dzierżawy usługi Azure Active Directory hello staje się administratorem globalnym. Tylko administratorzy globalni mogą przypisywać pozostałe role administratorów. Może istnieć więcej niż jeden administrator globalny w firmie. Administratorzy globalni mogą resetować hasła powitania dla każdego użytkownika i innych administratorów.

  > [!NOTE]
  > W interfejsu API Graph usługi Microsoft Azure AD Graph API i Azure AD PowerShell ta rola jest identyfikowane jako "Administrator firmy". Jest on "Administrator globalny" hello [portalu Azure](https://portal.azure.com).
  >
  >

* **Gość zapraszającej**: użytkowników w tej roli można zarządzać użytkownika zaproszeń do skorzystania z usługi Azure Active Directory B2B gościa, gdy ustawienia użytkownika "Zaprosić elementy członkowskie" hello ustawiono tooNo. Więcej informacji na temat współpracy B2B w [o Podgląd współpracy B2B usługi Azure AD hello](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). Nie ma inne uprawnienia.

* **Administrator usługi Intune**: użytkownicy z tą rolą uprawnień globalnych w programie Microsoft Intune Online, gdy usługa hello jest obecna. Ponadto tej roli zawiera hello możliwości toomanage użytkowników i urządzeń w kolejności tooassociate zasad, a także utworzyć i Zarządzaj grupami.

* **Skrzynki pocztowej administratora**: Ta rola jest używana tylko w ramach usługi Exchange Online obsługa poczty e-mail dla urządzeń Blackberry KRAWĘDZI. Jeśli Twoja organizacja nie korzysta z poczty e-mail usługi Exchange Online urządzeń Blackberry KRAWĘDZI, nie należy używać tej roli.

* **Warstwa obsługi 1 partnera**: nie używaj. Ta rola jest przestarzała i zostanie usunięte z usługi Azure AD w przyszłości hello. Ta rola jest przeznaczony dla niewielkiej liczby partnerów odsprzedaż firmy Microsoft i nie jest przeznaczona do użytku ogólnego.

* **Warstwy 2 w ramach partnera**: nie używaj. Ta rola jest przestarzała i zostanie usunięte z usługi Azure AD w przyszłości hello. Ta rola jest przeznaczony dla niewielkiej liczby partnerów odsprzedaż firmy Microsoft i nie jest przeznaczona do użytku ogólnego.

* **Administrator haseł / Administrator pomocy technicznej**: użytkownicy z tą rolą mogą resetowania haseł, zarządzanie żądaniami obsługi i monitoruje kondycję usługi. Administratorzy haseł mogą resetować hasła wyłącznie użytkowników i innych administratorów haseł.

  > [!NOTE]
  > W interfejsu API Graph usługi Microsoft Azure AD Graph API i Azure AD PowerShell ta rola jest identyfikowane jako "Administrator pomocy technicznej". Jest on "hasło administratora" hello [portalu Azure](https://portal.azure.com/).
  >
  >
  
* **Administrator usługi Power BI**: użytkownicy z tą rolą globalnych uprawnień w ramach usługi Microsoft Power BI, gdy usługa hello jest obecny, oraz toomanage możliwości hello bilety obsługi i monitoruje kondycję usługi. Więcej informacji na [ról administratora o usługi Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US).

* **Uprzywilejowany roli administratora**: użytkownicy z tą rolą mogą zarządzać przypisań ról w usłudze Azure Active Directory, a także w usłudze Azure AD Privileged Identity Management. Ponadto ta rola umożliwia zarządzanie wszystkich aspektów Privileged Identity Management.

* **Administrator zabezpieczeń**: użytkownicy z tą rolą mają wszystkie uprawnienia tylko do odczytu hello rolę czytelnika zabezpieczeń hello plus hello możliwości toomanage konfiguracji związanych z zabezpieczeniami usług: Azure Active Directory Identity Protection, platforma Azure Information Protection, Zarządzanie tożsamościami uprzywilejowanymi oraz zabezpieczeń usługi Office 365 i Centrum zgodności. Więcej informacji na temat uprawnień usługi Office 365 są dostępne pod adresem [uprawnień w programie Office 365 zabezpieczeń hello & Centrum zgodności](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Czytnik zabezpieczeń**: użytkownicy z tą rolą ma globalnego dostępu tylko do odczytu, w tym wszystkie informacje w usłudze Azure Active Directory, ochronę tożsamości, Zarządzanie tożsamościami uprzywilejowanymi, a także hello możliwości tooread usługi Azure Active Directory logowania Raporty i dzienników inspekcji. Rola Hello daje również uprawnienia tylko do odczytu w programie Office 365 zabezpieczeń & Centrum zgodności. Więcej informacji na temat uprawnień usługi Office 365 są dostępne pod adresem [uprawnień w programie Office 365 zabezpieczeń hello & Centrum zgodności](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Administrator obsługuje usługi**: użytkownicy z tą rolą mogą otworzyć żądania obsługi z firmą Microsoft dla usług Azure i usługi Office 365, a widoki hello Centrum pulpitu nawigacyjnego i komunikatów w portalu Azure hello usługi i portalu administracyjnego usługi Office 365. Więcej informacji na [ról administratora o usługi Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrator usługi SharePoint**: użytkownicy z tą rolą globalnych uprawnień w ramach programu Microsoft SharePoint Online, gdy usługa hello jest obecny, oraz toomanage możliwości hello bilety obsługi i monitoruje kondycję usługi. Więcej informacji na [ról administratora o usługi Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Skype dla firm / Administrator usługi Lync**: użytkownicy z tą rolą uprawnień globalnych w Microsoft Skype dla firm, gdy usługa hello jest obecny, a także zarządzać specyficzne dla usługi Skype atrybutów użytkownika w usłudze Azure Active Directory. Ponadto ten monitor i biletami pomocy technicznej toomanage rola przyznaje hello możliwości usługi kondycji. Więcej informacji na [ról administratora o usługi Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

  > [!NOTE]
  > W interfejsu API Graph usługi Microsoft Azure AD Graph API i Azure AD PowerShell ta rola jest identyfikowane jako "Administratora usługi Lync". Jest on "Skype dla firm administratora usługi" hello [portalu Azure](https://portal.azure.com/).
  >
  >

* **Administrator konta użytkownika**: użytkownicy z tą rolą mogą tworzyć i zarządzać wszystkimi aspektami użytkowników i grup. Ponadto ta rola obejmuje biletami pomocy technicznej toomanage możliwości hello i monitory usługi kondycji. Niektóre ograniczenia są stosowane. Na przykład ta rola nie zezwala na usuwanie administratora globalnego, a podczas umożliwia zmienianie haseł dla innych niż administratorzy, nie zezwala zmiana hasła dla administratorów globalnych lub innych uprzywilejowanych administratorów.

## <a name="administrator-permissions"></a>Uprawnienia administratora

### <a name="billing-administrator"></a>Administrator rozliczeń

| Możliwość | Nie można wykonać |
| --- | --- |
|<p>Wyświetlanie informacji o firmy i użytkownika</p><p>Zarządzanie biletami pomocy technicznej pakietu Office</p><p>Wykonywanie operacji rozliczeń i zakupów dla produktów pakietu Office</p> |<p>Resetowanie haseł użytkowników</p><p>Tworzenie i zarządzanie widokami użytkownika</p><p>Tworzenie, edycję, usuwanie użytkowników i grup i zarządzanie licencjami użytkowników</p><p>Zarządzanie domenami</p><p>Zarządzanie informacjami o firmy</p><p>Delegowanie ról administracyjnych tooothers</p><p>Używanie synchronizacji katalogów</p><p>Wyświetlanie dzienników inspekcji</p>|

### <a name="conditional-access-administrator"></a>Administrator dostępu warunkowego
| Możliwość | Nie można wykonać |
| --- | --- |
|<p>Wyświetlanie informacji o firmy i użytkownika</p><p>Zarządzanie ustawieniami dostępu warunkowego</p> |<p>Resetowanie haseł użytkowników</p><p>Tworzenie i zarządzanie widokami użytkownika</p><p>Tworzenie, edycję, usuwanie użytkowników i grup i zarządzanie licencjami użytkowników</p><p>Zarządzanie domenami</p><p>Zarządzanie informacjami o firmy</p><p>Delegowanie ról administracyjnych tooothers</p><p>Używanie synchronizacji katalogów</p><p>Wyświetlanie dzienników inspekcji</p>|

### <a name="global-administrator"></a>Administrator globalny
| Możliwość | Nie można wykonać |
| --- | --- |
|<p>Wyświetlanie informacji o firmy i użytkownika</p><p>Zarządzanie biletami pomocy technicznej pakietu Office</p><p>Wykonywanie operacji rozliczeń i zakupów dla produktów pakietu Office</p><p>Resetowanie haseł użytkowników</p><p>Resetowanie haseł innych administratorów</p><p>Tworzenie i zarządzanie widokami użytkownika</p><p>Tworzenie, edycję, usuwanie użytkowników i grup i zarządzanie licencjami użytkowników</p><p>Zarządzanie domenami</p><p>Zarządzanie informacjami o firmy</p><p>Delegowanie ról administracyjnych tooothers</p><p>Używanie synchronizacji katalogów</p><p>Włącz lub Wyłącz uwierzytelnianie wieloskładnikowe</p><p>Wyświetlanie dzienników inspekcji</p> |<p>Nie dotyczy</p>|

### <a name="password-administrator"></a>Administrator haseł
| Możliwość | Nie można wykonać |
| --- | --- |
| <p>Wyświetlanie informacji o firmy i użytkownika</p><p>Zarządzanie biletami pomocy technicznej pakietu Office</p><p>Resetowanie haseł użytkowników</p> <p>Resetowanie haseł innych administratorów</p>|<p>Wykonywanie operacji rozliczeń i zakupów dla produktów pakietu Office</p><p>Tworzenie i zarządzanie widokami użytkownika</p><p>Tworzenie, edycję, usuwanie użytkowników i grup i zarządzanie licencjami użytkowników</p><p>Zarządzanie domenami</p><p>Zarządzanie informacjami o firmy</p><p>Delegowanie ról administracyjnych tooothers</p><p>Używanie synchronizacji katalogów</p><p>Wyświetlanie raportów</p>|

### <a name="service-administrator"></a>Administrator usługi
| Możliwość | Nie można wykonać |
| --- | --- |
| <p>Wyświetlanie informacji o firmy i użytkownika</p><p>Zarządzanie biletami pomocy technicznej pakietu Office</p> |<p>Resetowanie haseł użytkowników</p><p>Wykonywanie operacji rozliczeń i zakupów dla produktów pakietu Office</p><p>Tworzenie i zarządzanie widokami użytkownika</p><p>Tworzenie, edycję, usuwanie użytkowników i grup i zarządzanie licencjami użytkowników</p><p>Zarządzanie domenami</p><p>Zarządzanie informacjami o firmy</p><p>Delegowanie ról administracyjnych tooothers</p><p>Używanie synchronizacji katalogów</p><p>Wyświetlanie dzienników inspekcji</p> |

### <a name="user-administrator"></a>Administrator użytkowników
| Możliwość | Nie można wykonać |
| --- | --- |
| <p>Wyświetlanie informacji o firmy i użytkownika</p><p>Zarządzanie biletami pomocy technicznej pakietu Office</p><p>Resetowanie haseł użytkowników z ograniczeniami.</p><p>Resetowanie haseł innych administratorów</p><p>Zresetować hasła innych użytkowników</p><p>Tworzenie i zarządzanie widokami użytkownika</p><p>Tworzenie, edycję, usuwanie użytkowników i grup i zarządzanie licencjami użytkowników z ograniczeniami. Użytkownik nie można usuwać administratorów globalnych ani tworzyć innych administratorów.</p> |<p>Wykonywanie operacji rozliczeń i zakupów dla produktów pakietu Office</p><p>Zarządzanie domenami</p><p>Zarządzanie informacjami o firmy</p><p>Delegowanie ról administracyjnych tooothers</p><p>Używanie synchronizacji katalogów</p><p>Włącz lub Wyłącz uwierzytelnianie wieloskładnikowe</p><p>Wyświetlanie dzienników inspekcji</p> |

### <a name="security-reader"></a>Czytnik zabezpieczeń
| W | Możliwość |
| --- | --- |
| Centrum ochrony tożsamości |Wszystkie raporty dotyczące zabezpieczeń i informacje o funkcjach zabezpieczeń ustawienia do odczytu<ul><li>Antyspamowy<li>Szyfrowanie<li>Zapobieganie utracie danych<li>Przed złośliwym oprogramowaniem<li>Advanced threat protection<li>Przed wyłudzaniem informacji<li>Reguły Mailflow |
| Privileged Identity Management |<p>Ma dostęp tylko do odczytu tooall informacje udostępniane w usłudze Azure AD PIM: zasady i raporty dla usługi Azure AD przypisań ról zabezpieczeń monitoruje i w hello przyszłości odczytać dane toopolicy dostępu i raporty dla scenariuszy oprócz przypisania roli usługi Azure AD.<p>**Nie można** utworzyć konto usługi Azure AD PIM lub wprowadzić tooit żadnych zmian. W portalu firmy usługi PIM lub za pomocą programu PowerShell ktoś jest w tej roli może aktywować dodatkowych ról (na przykład administrator globalny lub Administrator ról uprzywilejowanych), jeśli użytkownik hello jest kandydatem do nich. |
| <p>Kondycja usługi Office 365 monitora</p><p>Bezpieczeństwo usługi Office 365 i Centrum zgodności</p> |<ul><li>Przeczytaj alerty i zarządzaj nimi<li>Przeczytaj zasady zabezpieczeń<li>Odczytywanie analizy zagrożeń, Cloud App Discovery i kwarantanny w obszarze wyszukiwania i Zbadaj<li>Odczyt wszystkich raportów |

### <a name="security-administrator"></a>Administrator zabezpieczeń
| W | Możliwość |
| --- | --- |
| Centrum ochrony tożsamości |<ul><li>Wszystkie uprawnienia roli zabezpieczeń czytnika hello.<li>Ponadto hello tooperform możliwości wszystkie operacje IPC z wyjątkiem resetowanie haseł. |
| Privileged Identity Management |<ul><li>Wszystkie uprawnienia roli zabezpieczeń czytnika hello.<li>**Nie można** zarządzania członkostwa w roli usługi Azure AD lub ustawienia. |
| <p>Kondycja usługi Office 365 monitora</p><p>Bezpieczeństwo usługi Office 365 i Centrum zgodności |<ul><li>Wszystkie uprawnienia roli zabezpieczeń czytnika hello.<li>Można skonfigurować wszystkie ustawienia w funkcji Advanced Threat Protection hello (ochrony przed złośliwym oprogramowaniem i wirusami, złośliwy konfiguracji adresu URL, adres URL śledzenia itp.). |

## <a name="details-about-hello-global-administrator-role"></a>Szczegółowe informacje o roli administratora globalnego hello
administrator globalny Hello ma funkcje administracyjne tooall dostępu. Domyślnie program hello osoby, która zarejestruje się w celu uzyskania subskrypcji platformy Azure jest przypisany hello rolę administratora globalnego dla katalogu hello. Tylko administratorzy globalni mogą przypisywać pozostałe role administratorów.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd współpracownika jako administrator globalny

1. Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu dzierżawcy hello.

   ![Otwieranie Centrum administracyjnego usługi azure AD](./media/active-directory-assign-admin-roles/active-directory-admin-center.png)

2. Wybierz **użytkowników i grup &gt; wszyscy użytkownicy**

3. Znajdź użytkownika hello toodesignate jako administrator globalny i otwórz hello bloku dla tego użytkownika.

4. W bloku użytkownika hello, wybierz **roli katalogu**.
 
5. W bloku roli katalogu hello, wybierz hello **administratora globalnego** roli i Zapisz.

## <a name="assign-or-remove-administrator-roles"></a>Przypisywanie lub usuwanie ról administratora
toolearn tooassign ról administracyjnych tooa użytkownika w usłudze Azure Active Directory, zobacz temat [przypisać role tooadministrator w usłudze Azure Active Directory użytkownika](active-directory-users-assign-role-azure-portal.md).

## <a name="deprecated-roles"></a>Przestarzałe ról

nie należy używać Hello następujące role. One zostały przestarzałe i zostanie usunięte z usługi Azure AD w przyszłości hello.

* Administrator licencji ad hoc.
* Twórca zweryfikowano użytkownika wiadomości e-mail
* Dołącz do urządzenia
* Menedżerowie urządzeń
* Użytkownicy urządzeń
* Dołączanie urządzenia do miejsca pracy

## <a name="next-steps"></a>Następne kroki
* więcej informacji o toolearn, toochange Administratorzy subskrypcji platformy Azure, zobacz temat [jak tooadd lub zmień role administratora platformy Azure](../billing-add-change-azure-subscription-administrator.md)
* Zobacz toolearn więcej informacji na temat sposobu jest kontrolowany dostęp do zasobów na platformie Microsoft Azure [opis dostęp do zasobów na platformie Azure](active-directory-understanding-resource-access.md)
* Aby uzyskać więcej informacji dotyczących powiązań tooyour subskrypcji platformy Azure w usłudze Azure Active Directory, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Zarządzanie użytkownikami](active-directory-create-users.md)
* [Zarządzanie hasłami](active-directory-manage-passwords.md)
* [Zarządzanie grupami](active-directory-manage-groups.md)
