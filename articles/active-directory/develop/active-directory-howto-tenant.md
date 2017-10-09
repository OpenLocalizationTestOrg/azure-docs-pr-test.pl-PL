---
title: "tooget aaaHow dzierżawa usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak tooget usługi Azure Active Directory dzierżawy dla rejestracji i tworzenia aplikacji."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
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
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Jak dzierżawcy tooget usługi Azure Active Directory
W usłudze Azure Active Directory (Azure AD) [dzierżawa](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) reprezentuje organizację.  Jest to dedykowane wystąpienie hello usługi Azure AD, który organizacja otrzymuje i której zostaje właścicielem po zarejestrowaniu się dla usługi w chmurze Microsoft Azure, Microsoft Intune lub usługi Office 365.  Każda dzierżawa usługi Azure AD jest unikatowa i oddzielona od innych dzierżaw usługi Azure AD.  

Dzierżawa gromadzi użytkowników hello w firmie i hello informacje o nich — hasła, dane profilu użytkownika, uprawnienia i tak dalej.  Zawiera także grup, aplikacji i inne informacje dotyczące tooan organizacji i jej zabezpieczeń.

tooallow toosign użytkowników usługi Azure AD w tooyour aplikacji, należy zarejestrować aplikację w dzierżawie.  Publikowanie aplikacji w dzierżawie usługi Azure AD jest **całkowicie bezpłatne**.  W rzeczywistości większość deweloperów utworzy kilka dzierżaw i aplikacji do celów testowych, związanych z programowaniem, przeprowadzaniem badań oraz w ramach etapu przejściowego.  Organizacje, które zarejestrują się i korzystać z aplikacji Opcjonalnie można wybrać toopurchase licencje, jeśli chcą tootake korzystać z zaawansowanych funkcji katalogów.

Jak uzyskać dzierżawę usługi Azure AD?  Witaj procedura może przebiegać nieco inaczej, jeśli użytkownik:

* [Masz istniejącą subskrypcję usługi Office 365](#use-an-existing-office-365-subscription)
* [Masz istniejącą subskrypcję platformy Azure skojarzoną z kontem Microsoft](#use-an-msa-azure-subscription)
* [Masz istniejącą subskrypcję platformy Azure skojarzoną z kontem organizacyjnym](#use-an-organizational-azure-subscription)
* [Nie masz żadnej z powyższych hello & mają toostart od podstaw](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Korzystanie z istniejącej subskrypcji usługi Office 365
Jeśli masz istniejącą subskrypcję usługi Office 365, masz już dzierżawę usługi Azure AD. Możesz zalogować się toohello [portalu Azure](https://portal.azure.com) z usługi O365 konta i rozpocząć korzystanie z usługi Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Korzystanie z subskrypcji platformy Azure dla konta Microsoft
Jeśli Twoje indywidualne konto Microsoft zostało wcześniej zarejestrowane w celu uzyskania subskrypcji platformy Azure, masz już dzierżawę.  Jeśli logujesz się toohello [Azure Portal](https://portal.azure.com), można automatycznie są rejestrowane w tooyour domyślną dzierżawę. Są wolne toouse Zobacz tej dzierżawy podczas dopasowania — można jednak toocreate konto administratora organizacyjnego.

toodo tak, wykonaj następujące kroki.  Alternatywnie mogą ma toocreate nową dzierżawę i utworzyć administratora w tej dzierżawie, postępując według podobnej procedury.

1. Zaloguj się do hello [Azure Portal](https://portal.azure.com) za pomocą indywidualnego konta
2. Przejdź do sekcji "Azure Active Directory" toohello hello portalu (znalezione w pasku nawigacyjnym po lewej stronie powitania, w obszarze **więcej usług**)
3. Użytkownik powinien automatycznie być zalogowany toohello "Katalog domyślny", jeśli nie można przełączyć katalogów, klikając nazwę konta w prawym górnym rogu hello.
4. Z hello **Szybkie zadania** wybierz **dodać użytkownika**.
5. W formularzu Dodawanie użytkownika Witaj, podaj poniższe informacje hello:

   * Nazwa: (wybierz odpowiednią wartość).
   * Nazwa użytkownika: (wybierz nazwę użytkownika dla tego administratora).
   * Profil: (podaj odpowiednie wartości hello imię, ostatni nazwy, stanowisko i działu)
   * Rola: administrator globalny.
6. Po ukończeniu hello formularzem Dodawanie użytkownika i odbierać hello tymczasowe hasło dla nowego użytkownika administracyjnego hello, można toorecord się, że to hasło trzeba będzie toologin przy użyciu tego nowego użytkownika w kolejności toochange hello hasła. Możesz również wysłać hasło hello bezpośrednio toohello użytkownika przy użyciu alternatywnego adresu e-mail.
7. Polecenie **Utwórz** toocreate hello nowego użytkownika.
8. toochange hello hasło tymczasowe, zaloguj się do [https://login.microsoftonline.com](https://login.microsoftonline.com) z tym użytkownikiem nowe konto i Zmień hasło hello na żądanie.

## <a name="use-an-organizational-azure-subscription"></a>Korzystanie z organizacyjnej subskrypcji platformy Azure
Jeśli konto organizacyjne zostało wcześniej zarejestrowane w celu uzyskania subskrypcji platformy Azure, masz już dzierżawę.  W hello [Azure Portal](https://portal.azure.com), po przejściu zbyt powinna być widoczna dzierżawa "Więcej usług" i "Azure Active Directory."  Jesteś toouse bezpłatne, który tej dzierżawy, jak widać dopasowania.

## <a name="start-from-scratch"></a>Rozpoczynanie od zera
Jeśli wszystkie powyższe hello tooyou informacje, nie martw się.  Po prostu odwiedź stronę [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign dla platformy Azure z nową organizację.  Po zakończeniu procesu hello będziesz mieć własną dzierżawę usługi Azure AD z nazwą domeny hello wybrana podczas logowania się.  W hello [Azure Portal](https://portal.azure.com), odnaleźć dzierżawę, przechodząc zbyt "Azure Active Directory" w nav. po lewej stronie powitania

W ramach procesu rejestracji na platformie Azure hello będzie wymagany tooprovide szczegóły karty kredytowej.  Możesz to zrobić bez obaw — nie będą naliczane opłaty ani za publikowanie aplikacji w usłudze Azure AD, ani za tworzenie nowych dzierżaw.
