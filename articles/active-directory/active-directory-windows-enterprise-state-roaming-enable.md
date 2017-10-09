---
title: "aaaEnable roamingu stanu przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące ustawień roamingu stanu przedsiębiorstwa na urządzeniach z systemem Windows. Roamingu stanu przedsiębiorstwa udostępnia użytkownikom środowisko unified na ich urządzeniach z systemem Windows i skraca czas hello potrzebne do skonfigurowania nowego urządzenia."
services: active-directory
keywords: "roaming, chmury systemu windows, jak stanu przedsiębiorstwa tooenable roamingu stanu przedsiębiorstwa"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Włączanie roamingu stanu przedsiębiorstwa w usłudze Azure Active Directory
Roamingu stanu przedsiębiorstwa jest dostępne tooany organizacji z subskrypcją Premium usługi Azure Active Directory (Azure AD). Aby uzyskać więcej informacji na temat tooget subskrypcji usługi Azure AD, zobacz hello [stronę produktu usługi Azure AD](https://azure.microsoft.com/services/active-directory).

Po włączeniu roamingu stanu przedsiębiorstwa, organizacja będzie automatycznie otrzymać licencji dla subskrypcji bezpłatnych, ograniczonej tooAzure Rights Management. Ta bezpłatna subskrypcja jest ograniczona tooencrypting i odszyfrowywania ustawienia przedsiębiorstwa i dane aplikacji synchronizowane przez hello roamingu stanu przedsiębiorstwa usługi; Musisz mieć subskrypcję płatną toouse hello pełnego zestawu funkcji usługi Azure Rights Management.

Po uzyskaniu subskrypcji usługi Azure AD Premium, wykonaj te kroki tooenable, roamingu stanu przedsiębiorstwa:

1. Toohello logowania klasycznego portalu Azure.
2. Po lewej stronie powitania, wybierz **usługi ACTIVE DIRECTORY**, a następnie wybierz katalog hello, dla której ma zostać tooenable roamingu stanu przedsiębiorstwa.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Przejdź toohello **Konfiguruj** kartę w górnej części hello.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Przewiń w dół strony hello i wybierz **użytkownicy mogą SYNCHRONIZOWAĆ ustawienia i dane aplikacji przedsiębiorstwa**, a następnie kliknij przycisk **ZAPISAĆ**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Dla systemu Windows 10 ustawień tooroam urządzenia z hello roamingu stanu przedsiębiorstwa usługi urządzenia hello musi uwierzytelnić przy użyciu tożsamości usługi Azure AD. W przypadku urządzeń, które są przyłączone do tooAzure AD głównej logowania użytkownika hello jest tożsamości hello Azure AD, dlatego dodatkowa konfiguracja nie jest wymagane. Dla urządzeń, które korzysta z katalogu Active tradycyjnych, lokalnie hello administrator IT musi [połączyć hello tooAzure urządzeń przyłączonych do domeny AD dla systemu Windows 10 napotyka](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Synchronizacji magazynu danych
Roamingu stanu przedsiębiorstwa danych znajduje się w co najmniej jednej [regiony platformy Azure](https://azure.microsoft.com/regions/) czy najlepiej wyrównana z hello kraj/region wartość ustawiona w hello wystąpienia usługi Azure Active Directory. Dane roamingu stanu przedsiębiorstwa jest podzielona na partycje oparte na trzech głównych regionach geograficznych: Ameryce Północnej, regionie oraz APAC. Roamingu stanu przedsiębiorstwa danych dla dzierżawcy hello jest lokalnie znajdują się w tym regionie geograficznym hello i nie są replikowane w regionach.  Na przykład klienci, którzy mają ich tooone zestaw wartości kraj/region EMEA krajów, takie jak "Francja" lub "Zambii" będzie mieć swoje dane hostowanej w jednym lub hello regiony platformy Azure w Europie.  Klienci, którzy ustaw wartość ich kraj/region w usłudze Azure AD tooone krajów Ameryka Północna, takie jak "Stanów Zjednoczonych" lub "Kanada" będzie mieć swoje dane hostowanej w co najmniej jednej hello regiony platformy Azure w ramach hello Stanów Zjednoczonych.  Klienci, którzy ustaw wartość ich kraj/region w usłudze Azure AD tooone APAC krajów, takie jak "Australia" lub "Nowa Zelandia" będzie mieć swoje dane hostowanej w co najmniej jednej hello regiony platformy Azure w Azji.  Ameryki Południowej innych krajów i Antarktyka danych będzie obsługiwana w co najmniej jeden regiony platformy Azure w ramach hello Stanów Zjednoczonych.  wartość kraj/region Hello jest ustawiony jako część hello procesu tworzenia katalogu usługi Azure AD i nie można zmodyfikować później. 

Aby uzyskać więcej informacji na temat lokalizacji magazynu danych, założyć zgłoszenie [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Zarządzanie roamingu stanu przedsiębiorstwa
Administratorzy globalni usługi Azure AD można włączyć i wyłączyć roamingu stanu przedsiębiorstwa w hello klasycznego portalu Azure.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Administratorzy globalni mogą ograniczyć grup zabezpieczeń toospecific synchronizacji ustawień.

Administratorzy globalni można również wyświetlić raport o stanie synchronizacji urządzenia użytkownika, wybierając określonego użytkownika w wystąpieniu usługi Active Directory hello **użytkowników** liście i klikając **urządzeń** kartę i wybraniu widoku **Urządzeń Synchronizowanie ustawień i danych aplikacji przedsiębiorstwa**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Przechowywanie danych
TooAzure zsynchronizowane dane za pośrednictwem roamingu stanu przedsiębiorstwa zostaną zachowane przez czas nieokreślony, chyba że wykonywana jest operacja usuwania ręczne lub danych hello zagrożona jest określone toobe starych. 

**Jawne usuwanie:** hello dane są usuwane, gdy administrator Azure Usuwa użytkownika lub katalogu lub administrator żąda jawnie, czy dane są usuwane toobe.

* **Usunięcie użytkownika**: po usunięciu użytkownika w usłudze Azure AD, konto użytkownika hello roaming danych zostanie oznaczona do usunięcia i zostanie usunięta między 90 dni too180. 
* **Usuwanie katalogu**: usunięcie całego katalogu w usłudze Azure AD jest natychmiastowego działania. Wszystkie dane ustawienia hello skojarzone z których katalogu zostanie oznaczona do usunięcia i zostanie usunięty między 90 dni too180. 
* **Na żądanie usunięcia**: hello Azure AD administrator chce toomanually usunięcia danych określonego użytkownika lub danych ustawień, Witaj, Administratorze można założyć zgłoszenie [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/). 

**Usuwanie danych starych**: dane, które nie była używana dla jednego roku ("Witaj okres przechowywania") będzie traktowana jako przestarzały i mogą zostać usunięte z platformy Azure. okres przechowywania Hello jest toochange podmiotu, ale nie będzie mniejsza niż 90 dni. Witaj stare dane mogą być określonych aplikacji systemu Windows/ustawienia lub wszystkich ustawień dla użytkownika. Na przykład:

* Jeśli kolekcja określone ustawienia dostępu do żadnych urządzeń (np. aplikacja zostanie usunięty z urządzenia hello lub grupy ustawień, takich jak "Motywu" jest wyłączona dla wszystkich urządzeń użytkownika), a następnie tej kolekcji zostanie nieodświeżone po upływie okresu przechowywania hello i może być usunięte. 
* Jeśli użytkownik wyłączył ustawienia synchronizacji na wszystkich swoich urządzeniach, następnie Brak hello ustawienia danych jest niedostępny i wszystkich hello ustawienia danych dla tego użytkownika zostanie nieodświeżone i mogą zostać usunięte po upływie okresu przechowywania hello. 
* Jeśli katalog usługi Azure AD Witaj, Administratorze wyłącza roamingu stanu przedsiębiorstwa na powitania cały katalog, następnie wszyscy użytkownicy w tym katalogu zostanie zatrzymana, ustawienia synchronizacji, a wszystkie dane ustawienia dla wszystkich użytkowników będzie nieodświeżone i mogą zostać usunięte po upływie okresu przechowywania hello. 

**Odzyskiwanie danych usunięte**: zasady przechowywania danych hello nie jest konfigurowalne. Po hello dane zostaną trwale usunięte, nie będzie możliwe do odzyskania. Jednak ważne jest toonote, który hello danych ustawień zostaną usunięte tylko z platformy Azure, nie hello urządzeniu użytkownika końcowego. Dowolne urządzenie połączenie dalszej toohello roamingu stanu przedsiębiorstwa usługi, ustawienia hello ponownie zostaną zsynchronizowane i przechowywane na platformie Azure.

## <a name="related-topics"></a>Powiązane tematy
* [Opis roamingu stanu przedsiębiorstwa](active-directory-windows-enterprise-state-roaming-overview.md)
* [Ustawienia i dane mobilne — często zadawane pytania](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Ustawienia zasad i zarządzania urządzeniami Przenośnymi dla ustawień synchronizacji grupy](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Informacje dotyczące ustawień roamingu systemu Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Rozwiązywanie problemów](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
