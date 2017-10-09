---
title: "dostęp do aplikacji Sklep internetowy toouse aaaHow | Dokumentacja firmy Microsoft"
description: "Włączanie samoobsługi aplikacji dostępu tooallow użytkowników toofind własne aplikacje"
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
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="9ebab-103">Jak uzyskać dostęp do aplikacji Sklep internetowy toouse</span><span class="sxs-lookup"><span data-stu-id="9ebab-103">How toouse self-service application access</span></span>

<span data-ttu-id="9ebab-104">Zanim użytkownicy mogą odnajdować własnym aplikacji z ich panel dostępu, należy tooenable **dostęp do aplikacji Sklep internetowy** tooany aplikacji, że chcesz tooself użytkowników tooallow — odnajdywania i zażądać dostępu do.</span><span class="sxs-lookup"><span data-stu-id="9ebab-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="9ebab-105">Ta funkcja jest to doskonały sposób toosave czas i pieniądze jako grupa IT i zdecydowanie zaleca się jako część wdrożenia nowoczesnych aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ebab-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="9ebab-106">Za pomocą tej funkcji, można:</span><span class="sxs-lookup"><span data-stu-id="9ebab-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="9ebab-107">Zezwala użytkownikom na własnym odnajdywanie aplikacji hello [panelu dostępu aplikacji](https://myapps.microsoft.com/) bez bothering hello IT grupy.</span><span class="sxs-lookup"><span data-stu-id="9ebab-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="9ebab-108">Dodaj tych użytkowników tooa wstępnie skonfigurowane grupy, aby zobaczyć, kto żąda dostępu, usunięcie dostępu i zarządzanie rolami hello przypisane toothem.</span><span class="sxs-lookup"><span data-stu-id="9ebab-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="9ebab-109">Opcjonalnie dopuszczają zatwierdzająca firm żądań dostępu do aplikacji tooapprove hello grupa IT nie ma.</span><span class="sxs-lookup"><span data-stu-id="9ebab-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="9ebab-110">Opcjonalnie skonfiguruj się too10 osób, które może zatwierdzić dostęp toothis aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ebab-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="9ebab-111">Opcjonalnie Zezwalaj zatwierdzająca firm tooset hello hasła użytkownicy ci mogą używać toosign w aplikacji toohello z hello firm zatwierdzająca [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="9ebab-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="9ebab-112">Opcjonalnie automatycznie przypisywać bezpośrednio roli aplikacji tooan przypisanych użytkowników samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="9ebab-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="9ebab-113">Włączanie samoobsługi aplikacji dostępu tooallow użytkowników toofind własne aplikacje</span><span class="sxs-lookup"><span data-stu-id="9ebab-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="9ebab-114">Dostęp do aplikacji Sklep internetowy jest doskonałym sposobem tooallow użytkowników tooself — odnajdywanie aplikacji, opcjonalnie zezwolić na dostęp tooapprove grupy biznesowej hello toothose aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ebab-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="9ebab-115">Możesz zezwolić hello biznesowa grupy toomanage hello poświadczeń przypisanych użytkowników toothose jednokrotnego hasła w aplikacji bezpośrednio w ich panele dostępu.</span><span class="sxs-lookup"><span data-stu-id="9ebab-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="9ebab-116">tooenable samoobsługi aplikacji dostępu tooan aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ebab-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ebab-117">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="9ebab-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9ebab-118">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ebab-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ebab-119">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ebab-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ebab-120">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ebab-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ebab-121">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ebab-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="9ebab-122">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ebab-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ebab-123">Wybierz aplikację hello tooenable samoobsługi dostępu toofrom hello listy.</span><span class="sxs-lookup"><span data-stu-id="9ebab-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="9ebab-124">Po załadowaniu aplikacji hello, kliknij przycisk **samoobsługi** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ebab-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ebab-125">tooenable dostęp do aplikacji Sklep internetowy dla tej aplikacji, Włącz hello **użytkownicy aplikacji toothis dostępu toorequest?** Przełącz zbyt**tak.**</span><span class="sxs-lookup"><span data-stu-id="9ebab-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="9ebab-126">Następnie tooselect hello grupy toowhich użytkowników, którzy żądają dostępu do aplikacji toothis powinny zostać dodane, kliknij przycisk Dalej etykiety toohello hello selektora **toowhich grupy należy przypisać użytkownicy dodani?** i wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="9ebab-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="9ebab-127">**Opcjonalnie:** w razie potrzeby toorequire zatwierdzenia firm przed użytkownicy mogą uzyskiwać dostęp, należy ustawić hello **wymagają zatwierdzenia przed udzieleniem im dostępu do aplikacji toothis?** Przełącz zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="9ebab-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="9ebab-128">**Opcjonalnie: dla aplikacji za pomocą hasła jednokrotnego na tylko** w razie potrzeby tooallow tych firm osób zatwierdzających toospecify hello haseł, które są wysyłane toothis aplikacji dla zatwierdzonych użytkowników ustawić hello **tooset osób zatwierdzających Zezwalaj hasła użytkownika dla tej aplikacji?**  Przełącz zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="9ebab-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="9ebab-129">**Opcjonalnie:** toospecify hello biznesowe osoby zatwierdzające mogą tooapprove dostępu toothis aplikacji, kliknij przycisk Dalej etykiety toohello hello selektora **użytkowników, którzy mają tooapprove dostępu toothis aplikacji?** tooselect w górę too10 biznesowe poszczególnych osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="9ebab-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="9ebab-130">Grupy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="9ebab-130">Groups are not supported.</span></span>

13. <span data-ttu-id="9ebab-131">**Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz, aby tooassign roli tooa zatwierdzonych użytkowników samoobsługi, kliknij przycisk Dalej toohello selektora hello **toowhich roli należy przypisać użytkowników na tym aplikacji?**  tooselect hello roli toowhich powinien być przypisany tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9ebab-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="9ebab-132">Kliknij przycisk hello **zapisać** przycisk u góry hello hello toofinish bloku.</span><span class="sxs-lookup"><span data-stu-id="9ebab-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="9ebab-133">Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić tootheir [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk hello **+ Dodaj** przycisk toofind hello aplikacji toowhich włączono Dostęp z samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="9ebab-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="9ebab-134">Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="9ebab-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="9ebab-135">Można włączyć wiadomość e-mail z informacją, gdy użytkownik zażąda dostępu tooan aplikację, która wymaga zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="9ebab-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="9ebab-136">Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że możesz określić wiele osób zatwierdzających, wszelkie jedna osoba zatwierdzająca może zatwierdzić dostęp toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ebab-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ebab-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ebab-137">Next steps</span></span>
[<span data-ttu-id="9ebab-138">Konfigurowanie usługi Azure Active Directory do zarządzania grupami samoobsługi</span><span class="sxs-lookup"><span data-stu-id="9ebab-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
