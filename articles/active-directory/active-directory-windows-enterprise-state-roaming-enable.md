---
title: "Włącz Roaming stanu przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące ustawień roamingu stanu przedsiębiorstwa na urządzeniach z systemem Windows. Roamingu stanu przedsiębiorstwa udostępnia użytkownikom środowisko unified na ich urządzeniach z systemem Windows i skraca czas potrzebny na konfigurowanie nowego urządzenia."
services: active-directory
keywords: "roaming, chmury systemu windows, jak włączyć roamingu stanu przedsiębiorstwa stanu przedsiębiorstwa"
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
ms.openlocfilehash: 77d75f4a647e44f27cd9ba8db5286f1456c3ac66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Włączanie roamingu stanu przedsiębiorstwa w usłudze Azure Active Directory
Roamingu stanu przedsiębiorstwa jest dostępne dla każdej organizacji z subskrypcją Premium usługi Azure Active Directory (Azure AD). Aby uzyskać więcej informacji na temat sposobu uzyskania subskrypcji usługi Azure AD, zobacz [stronę produktu usługi Azure AD](https://azure.microsoft.com/services/active-directory).

Po włączeniu roamingu stanu przedsiębiorstwa, organizacja będzie automatycznie otrzymać licencji dla subskrypcji bezpłatnych, ograniczonej do usługi Azure Rights Management. Bezpłatna subskrypcja jest ograniczona do szyfrowania i odszyfrowywania ustawienia przedsiębiorstwa i dane aplikacji synchronizowane przez usługę roamingu stanu przedsiębiorstwa; musi mieć płatną subskrypcję, aby użyć pełnego zestawu funkcji usługi Azure Rights Management.

Po uzyskaniu subskrypcji usługi Azure AD Premium, wykonaj następujące kroki, aby włączyć roamingu stanu przedsiębiorstwa:

1. Zaloguj się do klasycznego portalu Azure.
2. Po lewej stronie, wybierz **usługi ACTIVE DIRECTORY**, a następnie wybierz katalog, dla którego chcesz włączyć roamingu stanu przedsiębiorstwa.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Przejdź do **Konfiguruj** na górnym pasku.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Przewiń w dół strony i wybierz **użytkownicy mogą SYNCHRONIZOWAĆ ustawienia i dane aplikacji przedsiębiorstwa**, a następnie kliknij przycisk **ZAPISAĆ**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Urządzenia Windows 10 są przekazywane ustawień w usłudze roamingu stanu przedsiębiorstwa urządzenie musi uwierzytelnić przy użyciu tożsamości usługi Azure AD. W przypadku urządzeń, które dołączyły do usługi Azure AD tożsamość usługi Azure AD jest podstawowy identyfikator logowania użytkownika, więc dodatkowa konfiguracja nie jest wymagane. W przypadku urządzeń korzystających z usługi Active Directory w tradycyjnych, lokalnie, administrator IT musi [łączenie urządzeń przyłączonych do domeny do usługi Azure AD dla systemu Windows 10 napotyka](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Synchronizacji magazynu danych
Roamingu stanu przedsiębiorstwa danych znajduje się w co najmniej jednej [regiony platformy Azure](https://azure.microsoft.com/regions/) najlepiej jest wyrównywany o wartości kraj/region w wystąpieniu usługi Azure Active Directory. Dane roamingu stanu przedsiębiorstwa jest podzielona na partycje oparte na trzech głównych regionach geograficznych: Ameryce Północnej, regionie oraz APAC. Roamingu stanu przedsiębiorstwa danych dla dzierżawy znajduje się lokalnie z region geograficzny, a nie są replikowane w regionach.  Na przykład klienci, którzy mają ich kraj/region ma wartość jednego z krajów EMEA, takich jak "Francja" lub "Zambii" będzie mieć swoje dane hostowanych w jedną lub regionów platformy Azure w Europie.  Klienci, którzy ustaw wartość ich kraj/region w usłudze Azure AD do jednego z krajów Ameryki Północnej, takie jak "Stanów Zjednoczonych" lub "Kanada" będzie mieć swoje dane przechowywane w co najmniej jeden regiony platformy Azure w Stanach Zjednoczonych.  Klienci, którzy ustaw wartość ich kraj/region w usłudze Azure AD do jednego z innych krajów APAC, takie jak "Australia" lub "Nowa Zelandia" będzie mieć swoje dane hostowanej w co najmniej jednej regiony platformy Azure w Azji.  Ameryki Południowej innych krajów i Antarktyka danych będzie obsługiwana w co najmniej jeden regiony platformy Azure w Stanach Zjednoczonych.  Wartość kraju/regionu jest ustawiony jako część procesu tworzenia katalogu usługi Azure AD i nie można zmodyfikować później. 

Aby uzyskać więcej informacji na temat lokalizacji magazynu danych, założyć zgłoszenie [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Zarządzanie roamingu stanu przedsiębiorstwa
Administratorzy globalni usługi Azure AD można włączyć i wyłączyć roamingu stanu przedsiębiorstwa w klasycznym portalu Azure.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Administratorzy globalni mogą ograniczyć synchronizacja ustawień w określonych grupach zabezpieczeń.

Administratorzy globalni można również wyświetlić raport o stanie synchronizacji urządzenia użytkownika, wybierając określonego użytkownika w wystąpieniu usługi Active Directory **użytkowników** liście i klikając **urządzeń** kartę i wybraniu widoku **urządzeń Synchronizowanie ustawień i danych aplikacji przedsiębiorstwa**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Przechowywanie danych
Danych synchronizowane na platformie Azure przy użyciu roamingu stanu przedsiębiorstwa zostaną zachowane przez czas nieokreślony, chyba że wykonywana jest operacja usuwania ręcznie lub w danych zostanie uznane za przestarzałe. 

**Jawne usuwanie:** dane są usuwane, gdy administrator Azure Usuwa użytkownika lub katalogu lub administrator jawnie żąda danych ma zostać usunięty.

* **Usunięcie użytkownika**: po usunięciu użytkownika w usłudze Azure AD, konto użytkownika mobilnego danych zostanie oznaczona do usunięcia i zostanie usunięta między 90 na 180 dni. 
* **Usuwanie katalogu**: usunięcie całego katalogu w usłudze Azure AD jest natychmiastowego działania. Wszystkie dane ustawienia skojarzone z których katalogu zostanie oznaczona do usunięcia i zostanie usunięty między 90 na 180 dni. 
* **Na żądanie usunięcia**: Jeśli administrator usługi Azure AD chce ręcznie usunąć dane i ustawienia danych określonego użytkownika, administrator może założyć zgłoszenie [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/). 

**Usuwanie danych starych**: dane, które nie była używana dla jednego roku ("okres przechowywania") będzie traktowana jako przestarzały i mogą zostać usunięte z platformy Azure. Okres przechowywania może ulec zmianie, ale nie będzie mniejsza niż 90 dni. Stare dane mogą być określonych aplikacji systemu Windows/ustawienia lub wszystkich ustawień dla użytkownika. Na przykład:

* Jeśli kolekcja określone ustawienia dostępu do żadnych urządzeń (np. aplikacja zostanie usunięty z urządzenia lub grupy ustawień, takich jak "Motywu" jest wyłączona dla wszystkich urządzeń użytkownika), a następnie tej kolekcji zostanie nieodświeżone po upływie okresu przechowywania i mogą zostać usunięte. 
* Jeśli użytkownik wyłączył ustawienia synchronizacji na wszystkich swoich urządzeniach, następnie żadne dane ustawienia jest niedostępny i wszystkich danych ustawień dla tego użytkownika zostanie nieodświeżone i mogą zostać usunięte po upływie okresu przechowywania. 
* Jeśli administrator katalogu usługi Azure AD wyłącza roamingu stanu przedsiębiorstwa dla całego katalogu, a następnie wszyscy użytkownicy w tym katalogu zostanie zatrzymana, ustawienia synchronizacji, a wszystkie dane ustawienia dla wszystkich użytkowników będzie nieodświeżone i mogą zostać usunięte po upływie okresu przechowywania. 

**Odzyskiwanie danych usunięte**: nie konfiguruje się z zasadami przechowywania danych. Gdy dane zostaną trwale usunięte, nie będzie możliwe do odzyskania. Jest jednak należy pamiętać, że dane ustawień tylko zostaną usunięte z platformy Azure, a nie na urządzeniu użytkownika końcowego. Dowolne urządzenie później połączenie z usługą roamingu stanu przedsiębiorstwa, ustawienia ponownie zostaną zsynchronizowane i przechowywane na platformie Azure.

## <a name="related-topics"></a>Powiązane tematy
* [Opis roamingu stanu przedsiębiorstwa](active-directory-windows-enterprise-state-roaming-overview.md)
* [Ustawienia i dane mobilne — często zadawane pytania](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Ustawienia zasad i zarządzania urządzeniami Przenośnymi dla ustawień synchronizacji grupy](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Informacje dotyczące ustawień roamingu systemu Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Rozwiązywanie problemów](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
