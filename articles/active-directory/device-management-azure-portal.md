---
title: "portal Azure — Witaj aaaManaging urządzeń przy użyciu wersji zapoznawczej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello urządzeń toomanage portalu Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>Zarządzanie urządzeniami za pomocą hello Azure portal — wersja zapoznawcza

>[!NOTE]
>Ta funkcja jest obecnie w wersji zapoznawczej. Można przygotować toorevert lub Usuń wszystkie zmiany. Funkcja Hello jest dostępna w żadnych subskrypcji usługi Azure Active Directory (Azure AD) w publicznej wersji zapoznawczej. Gdy funkcja hello staje się ogólnie dostępna, niektórych aspektów funkcji hello mogą jednak wymagać subskrypcję usługi Azure Active Directory premium.


Z zarządzania urządzeniami w usłudze Azure Active Directory (Azure AD) można zapewnić, że użytkownicy uzyskują dostęp do zasobów z urządzeń, które spełniają standardy zabezpieczeń i zgodności. 

W tym temacie:

- Przyjęto założenie, że czytelnik zna hello [wprowadzenie toodevice zarządzania w usłudze Azure Active Directory](device-management-introduction.md)

- Zapewnia możliwość hello o informacji na temat zarządzania urządzeniami przy użyciu portalu Azure


toomanage urządzenia w portalu Azure hello, należy tooclick **urządzeń** w hello **Zarządzaj** sekcji hello hello **usługi Azure Active Directory** bloku.

![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>Konfiguruj ustawienia urządzeń

toomanage swoje urządzenia za pomocą hello portalu Azure, potrzebują toobe zarejestrowany lub przyłączony tooAzure AD. Jako administrator Aby precyzyjnie zdefiniować hello proces rejestracji i dołączenie urządzeń przez skonfigurowanie ustawienia urządzenia hello.

![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/22.png)


Blok ustawień urządzenia Hello umożliwia tooconfigure:

- **Użytkownicy mogą przyłączać urządzenia tooAzure AD** — to ustawienie włącza tooselect hello użytkowników, którzy może dołączać urządzenia tooAzure AD. Domyślnie Hello **wszystkich**.

- **Urządzeniach przyłączonych do kolejnych administratorów lokalnych na usługi Azure AD** — możesz wybrać hello użytkowników, którzy mają prawa administratora lokalnego na urządzeniu. Użytkowników dodanych, w tym miejscu są dodawane toohello *Administratorzy urządzenia* roli w usłudze Azure AD. Administratorzy globalni w usłudze Azure AD i właścicielom urządzeń mają prawa administratora lokalnego domyślnie. Ta opcja jest dostępna za pośrednictwem produktów, takich jak Azure AD Premium lub Enterprise Mobility Suite (EMS) hello możliwości wersji premium. 

- **Użytkownicy mogą zarejestrować swoje urządzenia w usłudze Azure AD** — należy tooconfigure to ustawienie tooallow urządzeń toobe zarejestrowany z usługą Azure AD. W przypadku wybrania **Brak**, urządzenia nie są dozwolone tooregister, jeśli nie są one usługi Azure AD przyłączone lub hybrydowego przyłączonych do usługi Azure AD. Rejestrowanie w usłudze Microsoft Intune lub zarządzania urządzeniami przenośnymi (MDM) dla usługi Office 365 wymaga rejestracji. Jeśli skonfigurowano którąś z tych usług **wszystkie** jest zaznaczone i **Brak** nie jest dostępna.

- **Wymagaj uwierzytelniania wieloskładnikowego toojoin urządzeń** — możesz wybrać, czy użytkownicy są wymagane tooprovide drugiego uwierzytelniania dwuskładnikowego toojoin ich tooAzure urządzenia AD. Domyślnie Hello **nr**. Firma Microsoft zaleca, wymagając uwierzytelniania wieloskładnikowego podczas rejestrowania urządzenia. Przed włączeniem uwierzytelniania wieloskładnikowego dla tej usługi, pamiętaj, że skonfigurowano uwierzytelnianie wieloskładnikowe dla użytkowników hello, które rejestrują swoje urządzenia. Aby uzyskać więcej informacji dotyczących usług różnych uwierzytelnianie wieloskładnikowe platformy Azure, zobacz [wprowadzenie do korzystania z usługi Azure Multi-Factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md). 

- **Maksymalna liczba urządzeń** — to ustawienie włącza tooselect hello maksymalną liczbę urządzeń, które użytkownik może mieć w usłudze Azure AD. Jeśli użytkownik osiągnie ten limit przydziału, nie są być stanie tooadd dodatkowych urządzeń dopóki jedna lub więcej hello istniejące urządzenia zostaną usunięte. Oferta urządzenia Hello jest liczony dla wszystkich urządzeń, które są usługi Azure AD przyłączone lub usługi Azure AD, w obecnie zarejestrowany. Witaj, wartość domyślna to **20**.

- **Użytkownicy mogą synchronizować ustawienia i dane aplikacji na urządzeniach** — domyślnie to ustawienie ma wartość zbyt**Brak**. Wybranie określonych użytkowników lub grup lub wszystkich umożliwia toosync danych aplikacji i ustawień użytkownika hello na ich urządzeniach z systemem Windows 10. Dowiedz się więcej informacji na temat sposobu synchronizacji działa w systemie Windows 10.
Ta opcja jest dostępna za pośrednictwem produktów, takich jak Azure AD Premium lub Enterprise Mobility Suite (EMS) hello możliwości premium.
 
    ![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>Znajdź urządzenia

Jako administrator w hello portalu Azure, masz dwie opcje toolocate zarejestrowane i urządzeniach przyłączonych do:

- **Wszystkie urządzenia** w hello **Zarządzaj** sekcji hello **urządzeń** bloku  

    ![Wszystkie urządzenia](./media/device-management-azure-portal/41.png)


- **Urządzenia** w hello **Zarządzaj** sekcji **użytkownika** bloku
 
    ![Wszystkie urządzenia](./media/device-management-azure-portal/43.png)



Obie opcje można uzyskać widoku tooa który:


- Umożliwia toosearch urządzeń przy użyciu nazwy wyświetlanej hello jako filtr.

- Udostępnia szczegółowy przegląd urządzeń zarejestrowanych i połączone

- Umożliwia tooperform typowych zadań zarządzania dla urządzenia
   

![Wszystkie urządzenia](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>Zadania dotyczące zarządzania urządzeniami

Jako administrator, można zarządzać hello zarejestrowany lub urządzenia do miejsca pracy. Ta sekcja zawiera informacje o typowych zadań zarządzania dla urządzenia.


**Zarządzanie urządzeniem Intune** — Jeśli jesteś administratorem usługi Intune, możesz zarządzać urządzeniami oznaczona jako **Microsoft Intune**. Administrator może zobaczyć dodatkowe urządzenia 

![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/31.png)


**Włączanie / wyłączanie urządzeń usługi Azure AD**

tooenable lub wyłącz urządzenie, należy toobe administratorem globalnym w usłudze Azure AD. Wyłączenie urządzenia zapobiega urządzenia podczas uzyskiwania dostępu do zasobów usługi Azure AD.  toodisable hello urządzenia, możesz kliknąć przycisk *...* Kliknij urządzenie hello, aby uzyskać dodatkowe szczegóły.

 
![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/33.png)

Wyłączenie urządzenia zmieni stan hello w hello **włączone** kolumny zbyt**nr**.

![Wyłącz urządzenia](./media/device-management-azure-portal/32.png)


**Usuwanie urządzenia z systemem Azure AD** -toodelete urządzenie, należy toobe administratorem globalnym w usłudze Azure AD.  
Usuwanie urządzenia:
 
- Zapobiega urządzenia podczas uzyskiwania dostępu do zasobów usługi Azure AD 

- Usuwa wszystkie szczegóły, które są dołączone toohello urządzenia, na przykład, klucze funkcji BitLocker dla urządzeń z systemem Windows  

- Reprezentuje nieodwracalny działania i nie jest zalecane, chyba że jest to wymagane

Jeśli urządzenie jest zarządzane przez inny urząd zarządzania (np. Microsoft Intune), upewnij się, czy urządzenie hello, zostały wyczyszczone / wycofane przed usunięciem hello urządzenia w usłudze Azure AD.

Możesz wybrać "..." toodelete hello urządzenie lub urządzenia hello, aby uzyskać więcej informacji, kliknij polecenie
 
![Usuwanie urządzenia](./media/device-management-azure-portal/34.png)


**Wyświetl lub skopiuj identyfikator urządzenia** — można użyć szczegóły identyfikator urządzenia identyfikator tooverify hello urządzenia na urządzeniu hello lub podczas rozwiązywania problemów przy użyciu programu PowerShell. tooaccess hello kopiowania kliknij przycisk hello urządzenia.

![Wyświetl identyfikator urządzenia](./media/device-management-azure-portal/35.png)
  

**Wyświetl lub skopiować klucze funkcji BitLocker** — Jeśli jesteś administratorem, możesz wyświetlić hello kopiowania funkcji BitLocker kluczy lub toorecover użytkowników toohelp ich zaszyfrowanego dysku. Klucze te są dostępne tylko dla urządzeń z systemem Windows, które są szyfrowane i ich kluczy przechowywanych w usłudze Azure AD. Możesz skopiować te klucze podczas uzyskiwania dostępu do szczegółów hello urządzenia.
 
![Wyświetl klucze funkcji BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>Dzienniki inspekcji


działania urządzenia Hello są dostępne za pośrednictwem hello Dzienniki aktywności. Obejmuje to wyzwalane przez usługę rejestracji urządzeń hello lub przez użytkownika hello działania:

- Tworzenie urządzenia i dodawanie użytkowników/właścicieli na urządzeniu hello

- Zmiany ustawień toodevice

- Urządzenie operacji, takich jak usuwanie lub aktualizowanie urządzenia
 
Twoje toohello punktu wejścia inspekcja danych jest **dzienniki inspekcji** w hello **działania** sekcji hello **urządzeń* bloku.

![Dzienniki inspekcji](./media/device-management-azure-portal/61.png)


Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:

- Witaj Data i godzina wystąpienia hello

- obiekty docelowe Hello

- Witaj inicjatora / aktora (który) działania

- działanie Hello, (co)

![Dzienniki inspekcji](./media/device-management-azure-portal/63.png)

Można dostosować widok listy hello klikając **kolumn** hello w pasku narzędzi.
 
![Dzienniki inspekcji](./media/device-management-azure-portal/64.png)


toonarrow dół hello zgłoszone poziom tooa danych czy działa dla Ciebie, dane można filtrować hello inspekcji przy użyciu hello następujące pola:

- Catergory
- Typ zasobu działania
- Działanie
- Zakres dat
- docelowy
- Zainicjowane przez (aktora)

Ponadto filtry toohello można wyszukiwać określone wpisy.

![Dzienniki inspekcji](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie toodevice zarządzania w usłudze Azure Active Directory](device-management-introduction.md)



