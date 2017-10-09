---
title: "aaaHow aplikacje pojawiają się na panelu dostępu hello | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z niemożnością aplikacji pojawia się w hello panelu dostępu"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="77e59-103">Jak aplikacje pojawiają się na powitania panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="77e59-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="77e59-104">Hello Panel dostępu jest oparte na sieci web portalu, który umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory (Azure AD) tooview i rozpocząć aplikacje oparte na chmurze tego hello administratora usługi Azure AD ma udzielić dostępu do.</span><span class="sxs-lookup"><span data-stu-id="77e59-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="77e59-105">Te aplikacje są skonfigurowane w imieniu użytkownika hello w portalu usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="77e59-106">Witaj, Administratorze można udostępnić użytkownika toohello aplikacji hello bezpośrednio lub tooa grupę, którą użytkownik wchodzi w skład powodujące aplikacji hello znajdujących się w panelu dostępu hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77e59-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="77e59-107">Ogólne problemy toocheck najpierw</span><span class="sxs-lookup"><span data-stu-id="77e59-107">General issues toocheck first</span></span>

-   <span data-ttu-id="77e59-108">Jeśli aplikacja właśnie został usunięty przez użytkownika lub grupy hello użytkownik jest członkiem, spróbuj toosign i wylogowywanie ponownie do panelu dostępu użytkownika powitania po kilku minutach toosee usunięcie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="77e59-109">Jeśli licencji właśnie został usunięty z użytkownik lub grupa hello użytkownik jest członkiem to może zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy toobe zmiany wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="77e59-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="77e59-110">Zezwalaj na dodatkowy czas przed zalogowaniem się do hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="77e59-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="77e59-111">Toousers aplikacji powiązanych tooassigning problemów</span><span class="sxs-lookup"><span data-stu-id="77e59-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="77e59-112">Użytkownik może być widoczny aplikacji na ich panelu dostępu ponieważ one była wcześniej przypisane tooit.</span><span class="sxs-lookup"><span data-stu-id="77e59-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="77e59-113">Poniżej przedstawiono niektóre toocheck sposobów:</span><span class="sxs-lookup"><span data-stu-id="77e59-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="77e59-114">Sprawdź, czy użytkownik jest przypisany toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="77e59-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="77e59-115">Sprawdź, czy użytkownik jest objętych licencją powiązane toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="77e59-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="77e59-116">Sprawdź, czy użytkownik jest przypisany toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="77e59-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="77e59-117">toocheck Jeśli użytkownik jest przypisany toohello aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="77e59-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="77e59-118">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="77e59-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="77e59-119">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="77e59-120">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="77e59-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="77e59-121">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="77e59-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="77e59-122">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77e59-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="77e59-123">**Wyszukiwanie** hello nazwy aplikacji hello jest zagrożona.</span><span class="sxs-lookup"><span data-stu-id="77e59-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="77e59-124">Kliknij przycisk **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="77e59-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="77e59-125">Określ, czy toosee użytkownikowi przypisano toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77e59-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="77e59-126">Jeśli użytkownik hello tooremove z aplikacji hello **kliknij wiersz hello** hello użytkownika i wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="77e59-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="77e59-127">Sprawdź, czy użytkownik jest objętych licencją powiązane toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="77e59-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="77e59-128">toocheck użytkownika przypisane licencje, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="77e59-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="77e59-129">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="77e59-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="77e59-130">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="77e59-131">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="77e59-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="77e59-132">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="77e59-133">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="77e59-133">click **All users**.</span></span>

6.  <span data-ttu-id="77e59-134">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="77e59-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="77e59-135">Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="77e59-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="77e59-136">Jeśli użytkownik hello jest tooan przypisanej licencji pakietu Office to włączenie tooappear aplikacji pierwszej strony pakietu Office na panelu dostępu hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77e59-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="77e59-137">Toogroups aplikacji powiązanych tooassigning problemów</span><span class="sxs-lookup"><span data-stu-id="77e59-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="77e59-138">Użytkownik może być widoczny aplikacji na ich Panel dostępu, ponieważ są one częścią grupy przypisanej do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="77e59-139">Poniżej przedstawiono niektóre toocheck sposobów:</span><span class="sxs-lookup"><span data-stu-id="77e59-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="77e59-140">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="77e59-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="77e59-141">Sprawdź, czy użytkownik jest członkiem grupy przypisane tooa licencji</span><span class="sxs-lookup"><span data-stu-id="77e59-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="77e59-142">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="77e59-142">Check a user’s group memberships</span></span>

<span data-ttu-id="77e59-143">toocheck członkostwa w grupie, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="77e59-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="77e59-144">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="77e59-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="77e59-145">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="77e59-146">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="77e59-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="77e59-147">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="77e59-148">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="77e59-148">click **All users**.</span></span>

6.  <span data-ttu-id="77e59-149">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="77e59-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="77e59-150">Kliknij przycisk **grup.**</span><span class="sxs-lookup"><span data-stu-id="77e59-150">click **Groups.**</span></span>

8.  <span data-ttu-id="77e59-151">Określ, czy toosee użytkownika jest częścią grupy przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77e59-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="77e59-152">Jeśli chcesz, aby tooremove hello użytkownika z grupy hello **kliknij wiersz hello** hello grupy i wybierz opcję Usuń.</span><span class="sxs-lookup"><span data-stu-id="77e59-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="77e59-153">Sprawdź, czy użytkownik jest członkiem grupy przypisane tooa licencji</span><span class="sxs-lookup"><span data-stu-id="77e59-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="77e59-154">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="77e59-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="77e59-155">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="77e59-156">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="77e59-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="77e59-157">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="77e59-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="77e59-158">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="77e59-158">click **All users**.</span></span>

6.  <span data-ttu-id="77e59-159">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="77e59-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="77e59-160">Kliknij przycisk **grup.**</span><span class="sxs-lookup"><span data-stu-id="77e59-160">click **Groups.**</span></span>

8.  <span data-ttu-id="77e59-161">Kliknij wiersz hello określonej grupy.</span><span class="sxs-lookup"><span data-stu-id="77e59-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="77e59-162">Kliknij przycisk **licencji** toosee grupy hello licencji, do której przypisany tooit.</span><span class="sxs-lookup"><span data-stu-id="77e59-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="77e59-163">Jeśli grupa hello jest tooan przypisanej licencji pakietu Office może to włączenie niektórych tooappear aplikacji pierwszej strony pakietu Office na panelu dostępu hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77e59-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="77e59-164">Jeśli te kroki rozwiązywania problemów nie hello rozwiązać problem hello</span><span class="sxs-lookup"><span data-stu-id="77e59-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="77e59-165">Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:</span><span class="sxs-lookup"><span data-stu-id="77e59-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="77e59-166">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="77e59-166">Correlation error ID</span></span>

-   <span data-ttu-id="77e59-167">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="77e59-167">UPN (user email address)</span></span>

-   <span data-ttu-id="77e59-168">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="77e59-168">Tenant ID</span></span>

-   <span data-ttu-id="77e59-169">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="77e59-169">Browser type</span></span>

-   <span data-ttu-id="77e59-170">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="77e59-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="77e59-171">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="77e59-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="77e59-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77e59-172">Next steps</span></span>
[<span data-ttu-id="77e59-173">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77e59-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
