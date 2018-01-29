---
title: "Jak uzyskać dzierżawę usługi Azure AD | Microsoft Docs"
description: "Jak uzyskać dzierżawę usługi Azure Active Directory w celu rejestracji i tworzenia aplikacji."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 5874e6ce7d19c5106bc88ce9ff7fddd1842e0c3b
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2017
---
# <a name="how-to-get-an-azure-active-directory-tenant"></a>Jak uzyskać dzierżawę usługi Azure Active Directory
W usłudze Azure Active Directory (Azure AD) [dzierżawa](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) reprezentuje organizację.  Jest to dedykowane wystąpienie usługi Azure AD, którą organizacja otrzymuje i której zostaje właścicielem po zarejestrowaniu się w usłudze w chmurze firmy Microsoft, takiej jak platforma Azure, usługa Microsoft Intune czy usługa Office 365.  Każda dzierżawa usługi Azure AD jest unikatowa i oddzielona od innych dzierżaw usługi Azure AD.  

Dzierżawa gromadzi użytkowników w firmie i informacje o nich — hasła, dane profilu użytkownika, uprawnienia i tak dalej.  Zawiera także grupy, aplikacje i inne informacje dotyczące organizacji i jej zabezpieczeń.

Aby umożliwić użytkownikom usługi Azure AD zalogowanie się do Twojej aplikacji, musisz zarejestrować aplikację w dzierżawie.  Publikowanie aplikacji w dzierżawie usługi Azure AD jest **całkowicie bezpłatne**.  W rzeczywistości większość deweloperów tworzy kilka dzierżaw i aplikacji do celów testowych, związanych z programowaniem, przeprowadzaniem badań oraz w ramach etapu przejściowego.  Organizacje, które zarejestrują się i będą korzystać z aplikacji, mogą opcjonalnie zakupić licencje, jeśli chcą skorzystać z zaawansowanych funkcji katalogów.

Jak uzyskać dzierżawę usługi Azure AD?  Procedura może przebiegać nieco inaczej, jeśli:

* [Masz istniejącą subskrypcję usługi Office 365](#use-an-existing-office-365-subscription)
* [Masz istniejącą subskrypcję platformy Azure skojarzoną z kontem Microsoft](#use-an-msa-azure-subscription)
* [Masz istniejącą subskrypcję platformy Azure skojarzoną z kontem organizacyjnym](#use-an-organizational-azure-subscription)
* [Nie masz żadnej z powyższych subskrypcji i chcesz rozpocząć od zera](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Korzystanie z istniejącej subskrypcji usługi Office 365
Jeśli masz istniejącą subskrypcję usługi Office 365, masz już dzierżawę usługi Azure AD. Możesz zalogować się w witrynie [Azure Portal](https://portal.azure.com) za pomocą danych konta usługi O365 i rozpocząć korzystanie z usługi Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Korzystanie z subskrypcji platformy Azure dla konta Microsoft
Jeśli Twoje indywidualne konto Microsoft zostało wcześniej zarejestrowane w celu uzyskania subskrypcji platformy Azure, masz już dzierżawę.  Kiedy logujesz się w witrynie [Azure Portal](https://portal.azure.com), następuje automatyczne logowanie do domyślnej dzierżawy. Możesz korzystać z tej dzierżawy zgodnie z własnymi potrzebami, ale warto utworzyć konto administratora organizacyjnego.

W tym celu wykonaj poniższe kroki.  Możesz też utworzyć nową dzierżawę i utworzyć administratora w tej dzierżawie, postępując według podobnej procedury.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com) na swoje indywidualne konto.
2. Przejdź do sekcji „Azure Active Directory” (na lewym pasku nawigacyjnym, w obszarze **Więcej usług**).
3. Powinno nastąpić automatyczne zalogowanie do domyślnego katalogu. Jeśli tak się nie stanie, możesz przełączyć katalogi, klikając nazwę konta w prawym górnym rogu.
4. W sekcji **Szybkie zadania** wybierz opcję **Dodaj użytkownika**.
5. W formularzu Dodawanie użytkownika podaj następujące dane:

   * Nazwa: (wybierz odpowiednią wartość).
   * Nazwa użytkownika: (wybierz nazwę użytkownika dla tego administratora).
   * Profil: (podaj odpowiednie wartości dla pól Imię, Nazwisko, Stanowisko i Dział).
   * Rola: administrator globalny.
6. Po ukończeniu pracy z formularzem Dodawanie użytkownika i otrzymaniu tymczasowego hasła dla nowego użytkownika administracyjnego pamiętaj o zapisaniu hasła. Jest to konieczne, ponieważ w celu zmiany hasła trzeba zalogować się za pomocą danych nowego użytkownika. Używając alternatywnego adresu e-mail, możesz również wysłać hasło bezpośrednio do użytkownika.
7. Kliknij opcję **Utwórz**, aby utworzyć nowego użytkownika.
8. Aby zmienić hasło tymczasowe, zaloguj się na stronie [https://login.microsoftonline.com](https://login.microsoftonline.com), używając nowego konta użytkownika, i zmień hasło, gdy pojawi się stosowny monit.

## <a name="use-an-organizational-azure-subscription"></a>Korzystanie z organizacyjnej subskrypcji platformy Azure
Jeśli konto organizacyjne zostało wcześniej zarejestrowane w celu uzyskania subskrypcji platformy Azure, masz już dzierżawę.  W witrynie [Azure Portal](https://portal.azure.com) należy wyszukać dzierżawę po przejściu do sekcji „Więcej usług” i „Azure Active Directory”.  Z tej dzierżawy możesz korzystać zależnie od potrzeb.

## <a name="start-from-scratch"></a>Rozpoczynanie od zera
Jeśli wszystkie powyższe informacje są dla Ciebie mało zrozumiałe, nie przejmuj się. Po prostu odwiedź witrynę [Azure Portal](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory), aby utworzyć nowy katalog usługi Azure AD. Po zakończeniu tego procesu będziesz dysponować własną dzierżawą usługi Azure AD wraz z nazwą domeny wybraną podczas rejestracji.  W witrynie [Azure Portal](https://portal.azure.com) możesz odnaleźć swoją dzierżawę, przechodząc do obszaru **Azure Active Directory** na panelu nawigacyjnym po lewej stronie.
