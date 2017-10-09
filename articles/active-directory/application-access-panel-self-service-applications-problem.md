---
title: "za pomocą dostępu do aplikacji Sklep internetowy aaaProblem | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z dostępem powiązanych aplikacji usługi tooself problemów"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="6dc20-103">Problem za pomocą dostępu do aplikacji Sklep internetowy</span><span class="sxs-lookup"><span data-stu-id="6dc20-103">Problem using self-service application access</span></span>

<span data-ttu-id="6dc20-104">Dostęp do aplikacji Sklep internetowy jest doskonałym sposobem tooallow użytkowników tooself — odnajdywanie aplikacji, opcjonalnie zezwolić na dostęp tooapprove grupy biznesowej hello toothose aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6dc20-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="6dc20-105">Możesz zezwolić hello biznesowa grupy toomanage hello poświadczeń przypisanych użytkowników toothose jednokrotnego hasła w aplikacji bezpośrednio w ich panele dostępu.</span><span class="sxs-lookup"><span data-stu-id="6dc20-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="6dc20-106">Zanim użytkownicy mogą odnajdować własnym aplikacji z ich panel dostępu, należy tooenable **dostęp do aplikacji Sklep internetowy** tooany aplikacji, że chcesz tooself użytkowników tooallow — odnajdywania i zażądać dostępu do.</span><span class="sxs-lookup"><span data-stu-id="6dc20-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="6dc20-107">Ogólne problemy toocheck najpierw</span><span class="sxs-lookup"><span data-stu-id="6dc20-107">General issues toocheck first</span></span>

-   <span data-ttu-id="6dc20-108">Upewnij się, że poprawnie skonfigurowano dostęp do aplikacji Sklep internetowy.</span><span class="sxs-lookup"><span data-stu-id="6dc20-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="6dc20-109">Zobacz "Jak tooconfigure samoobsługi aplikacji dostępu".</span><span class="sxs-lookup"><span data-stu-id="6dc20-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="6dc20-110">Upewnij się, że została hello użytkownikowi lub grupie dostęp do aplikacji Sklep internetowy toorequest włączone.</span><span class="sxs-lookup"><span data-stu-id="6dc20-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="6dc20-111">Upewnij się, że hello odwiedzania hello odpowiednie miejsce dostępu do aplikacji Sklep internetowy.</span><span class="sxs-lookup"><span data-stu-id="6dc20-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="6dc20-112">Użytkownicy mogą przechodzić tootheir [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk hello **+ Dodaj** przycisk toofind hello aplikacji toowhich włączono samoobsługi dostępu.</span><span class="sxs-lookup"><span data-stu-id="6dc20-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="6dc20-113">Jeśli dostęp do aplikacji Sklep internetowy niedawno został skonfigurowany, ponów toosign i wylogowywanie do panelu dostępu użytkownika hello po kilku minutach toosee Jeśli pojawiły hello zmian samoobsługi dostępu.</span><span class="sxs-lookup"><span data-stu-id="6dc20-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="6dc20-114">Jak uzyskać dostęp do aplikacji Sklep internetowy tooconfigure</span><span class="sxs-lookup"><span data-stu-id="6dc20-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="6dc20-115">tooenable samoobsługi aplikacji dostępu tooan aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6dc20-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="6dc20-116">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="6dc20-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6dc20-117">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="6dc20-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6dc20-118">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="6dc20-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6dc20-119">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6dc20-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6dc20-120">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6dc20-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="6dc20-121">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="6dc20-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="6dc20-122">Wybierz aplikację hello tooenable samoobsługi dostępu toofrom hello listy.</span><span class="sxs-lookup"><span data-stu-id="6dc20-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="6dc20-123">Po załadowaniu aplikacji hello, kliknij przycisk **samoobsługi** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6dc20-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6dc20-124">tooenable dostęp do aplikacji Sklep internetowy dla tej aplikacji, Włącz hello **użytkownicy aplikacji toothis dostępu toorequest?** Przełącz zbyt**tak.**</span><span class="sxs-lookup"><span data-stu-id="6dc20-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="6dc20-125">Następnie tooselect hello grupy toowhich użytkowników, którzy żądają dostępu do aplikacji toothis powinny zostać dodane, kliknij przycisk Dalej etykiety toohello hello selektora **toowhich grupy należy przypisać użytkownicy dodani?** i wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="6dc20-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="6dc20-126">**Opcjonalnie:** w razie potrzeby toorequire zatwierdzenia firm przed użytkownicy mogą uzyskiwać dostęp, należy ustawić hello **wymagają zatwierdzenia przed udzieleniem im dostępu do aplikacji toothis?** Przełącz zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="6dc20-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="6dc20-127">**Opcjonalnie: dla aplikacji za pomocą hasła jednokrotnego na tylko** w razie potrzeby tooallow tych firm osób zatwierdzających toospecify hello haseł, które są wysyłane toothis aplikacji dla zatwierdzonych użytkowników ustawić hello **tooset osób zatwierdzających Zezwalaj hasła użytkownika dla tej aplikacji?**  Przełącz zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="6dc20-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="6dc20-128">**Opcjonalnie:** toospecify hello biznesowe osoby zatwierdzające mogą tooapprove dostępu toothis aplikacji, kliknij przycisk Dalej etykiety toohello hello selektora **użytkowników, którzy mają tooapprove dostępu toothis aplikacji?** tooselect w górę too10 biznesowe poszczególnych osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="6dc20-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="6dc20-129">Grupy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6dc20-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="6dc20-130">**Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz, aby tooassign roli tooa zatwierdzonych użytkowników samoobsługi, kliknij przycisk Dalej toohello selektora hello **toowhich roli należy przypisać użytkowników na tym aplikacji?**  tooselect hello roli toowhich powinien być przypisany tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6dc20-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="6dc20-131">Kliknij przycisk hello **zapisać** przycisk u góry hello hello toofinish bloku.</span><span class="sxs-lookup"><span data-stu-id="6dc20-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="6dc20-132">Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić tootheir [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk hello **+ Dodaj** przycisk toofind hello aplikacji toowhich włączono Dostęp z samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="6dc20-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="6dc20-133">Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6dc20-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="6dc20-134">Można włączyć wiadomość e-mail z informacją, gdy użytkownik zażąda dostępu tooan aplikację, która wymaga zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="6dc20-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="6dc20-135">Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że możesz określić wiele osób zatwierdzających, wszelkie jedna osoba zatwierdzająca może zatwierdzić dostęp toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6dc20-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="6dc20-136">Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu hello</span><span class="sxs-lookup"><span data-stu-id="6dc20-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="6dc20-137">Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:</span><span class="sxs-lookup"><span data-stu-id="6dc20-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="6dc20-138">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="6dc20-138">Correlation error ID</span></span>

-   <span data-ttu-id="6dc20-139">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="6dc20-139">UPN (user email address)</span></span>

-   <span data-ttu-id="6dc20-140">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="6dc20-140">TenantID</span></span>

-   <span data-ttu-id="6dc20-141">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="6dc20-141">Browser type</span></span>

-   <span data-ttu-id="6dc20-142">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="6dc20-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="6dc20-143">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="6dc20-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dc20-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6dc20-144">Next steps</span></span>
[<span data-ttu-id="6dc20-145">Konfigurowanie usługi Azure Active Directory do zarządzania grupami samoobsługi</span><span class="sxs-lookup"><span data-stu-id="6dc20-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
