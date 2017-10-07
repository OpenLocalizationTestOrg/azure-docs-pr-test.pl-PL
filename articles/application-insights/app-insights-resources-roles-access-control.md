---
title: "aaaResources, ról i kontroli dostępu w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Właściciele, współautorzy i czytelnicy wgląd w organizacji."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Zasoby, ról i kontroli dostępu w usłudze Application Insights
Można kontrolować, kto ma odczytywanie i aktualizowanie danych tooyour dostępu na platformie Azure [usługi Application Insights][start], za pomocą [kontroli dostępu opartej na rolach w systemie Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Przypisywanie dostępu toousers w hello **grupy zasobów lub subskrypcji** toowhich zasobu aplikacji należy - nie w zasobie hello, sama. Przypisz hello **współautora składników usługi Application Insights** roli. Dzięki temu uniform kontroli dostępu tooweb testy i alerty wraz z zasobu aplikacji. [Dowiedz się więcej](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Zasoby, grup i subskrypcji
Pierwszy, definicje:

* **Zasób** — wystąpienie usługi Microsoft Azure. Zasób usługi Application Insights gromadzi, analizuje i wyświetla hello danych telemetrycznych wysłanych z aplikacji.  Inne typy zasobów platformy Azure obejmują aplikacje sieci web, bazy danych i maszyn wirtualnych.
  
    Otwórz zasobów toosee hello [Azure Portal][portal], zaloguj się i kliknij pozycję wszystkie zasoby. toofind zasób typu część nazwy w polu filtru hello.
  
    ![Lista zasobów platformy Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Grupa zasobów** ] [ group] -tooone grupy należy co zasób. Grupa to wygodny sposób toomanage powiązanych zasobów, szczególnie w przypadku kontroli dostępu. Na przykład do jednego zasobu grupy można umieścić w aplikacji sieci Web, aplikacji hello toomonitor zasobu usługi Application Insights i tookeep zasobów magazynu wyeksportowane dane.

    ![Kliknij przycisk Przeglądaj, grupy zasobów, a następnie wybierz grupę](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Subskrypcja** ](https://manage.windowsazure.com) -toouse Application Insights lub innych zasobów platformy Azure, możesz zarejestrować się w tooan subskrypcji platformy Azure. Każda grupa zasobów należy tooone subskrypcji platformy Azure, które wybierz pakiet ceny i, jeśli jest subskrypcji organizacji wybrać hello członków i uprawnień dostępu.
* [**Konto Microsoft** ] [ account] — Witaj nazwy użytkownika i hasła, użyj toosign w tooMicrosoft Azure subskrypcji, XBox Live, Outlook.com i innych usług firmy Microsoft.

## <a name="access"></a>Kontroli dostępu w grupie zasobów hello
Jest ważne toounderstand w zasobie toohello dodanie utworzone dla aplikacji, czy też oddzielić zasoby ukryte alerty i analiz sieci web. Są one dołączone toohello tego samego [grupy zasobów](#resource-group) jako aplikacji. Może również umieszczono innymi usługami Azure w nim, takich jak magazyny lub witryn sieci Web.

![Zasoby w usłudze Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

toocontrol dostęp do toothese zasobów, dlatego zalecane jest aby:

* Kontrola dostępu na powitania **grupy zasobów lub subskrypcji** poziom.
* Przypisz hello **współautora Application Insights składnika** toousers roli. Umożliwia im testy sieci web tooedit, alerty i zasobów usługi Application Insights, bez konieczności podawania tooany dostępu do innych usług w grupie hello.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide dostęp tooanother użytkownika
Musisz mieć subskrypcję toohello praw właściciela lub grupy zasobów hello.

Witaj, użytkownik musi mieć [Account Microsoft][account], ani uzyskiwać dostępu do tootheir [Account Microsoft organizacji](../active-directory/sign-up-organization.md). Możesz podać tooindividuals dostępu, a także toouser grup zdefiniowanych w usłudze Azure Active Directory.

#### <a name="navigate-toohello-resource-group"></a>Przejdź toohello grupy zasobów
Dodaj użytkownika hello istnieje.

![W bloku zasobów aplikacji otwórz Essentials, otwórz hello grupy zasobów, a wybierz ustawienia/użytkowników. Kliknij pozycję Add (Dodaj).](./media/app-insights-resources-roles-access-control/01-add-user.png)

Lub może do góry innego poziomu i dodać toohello użytkownika hello subskrypcji.

#### <a name="select-a-role"></a>Wybierz rolę
![Wybierz rolę do hello nowego użytkownika.](./media/app-insights-resources-roles-access-control/03-role.png)

| Rola | W grupie zasobów hello |
| --- | --- |
| Właściciel |Można zmienić wszystko, w tym dostępu użytkownika |
| Współautor |Można edytować wszystko, w tym wszystkie zasoby |
| Współautor Insights składnika aplikacji |Można edytować zasobów usługi Application Insights, testy sieci web i alerty |
| Czytelnik |Można wyświetlać, ale nie zmienia sytuacji |

"Edycja" obejmuje tworzenie, usuwanie i aktualizowanie:

* Zasoby
* Testy sieci Web
* Alerty
* Eksport ciągły

#### <a name="select-hello-user"></a>Wybierz użytkownika hello

Jeśli hello użytkownika, które mają nie znajduje się w katalogu hello, możesz poprosić każda osoba z kontem Microsoft.
(Jeśli korzystają z usług takich jak Outlook.com, OneDrive, Windows Phone lub XBox Live, mają konta Microsoft.)

## <a name="related-content"></a>Zawartość pokrewna

* [Oparta na rolach kontrola dostępu na platformie Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
