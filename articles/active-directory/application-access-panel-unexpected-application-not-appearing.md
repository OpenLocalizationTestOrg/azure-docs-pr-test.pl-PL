---
title: "aaaAn przypisane aplikacji nie jest wyświetlane w panelu dostępu hello | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z powodu aplikacji nie jest wyświetlane w panelu dostępu hello"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="d33cf-103">Przypisane aplikacji nie jest wyświetlane na powitania panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="d33cf-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="d33cf-104">Hello Panel dostępu jest oparte na sieci web portalu, który umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory (Azure AD) tooview i rozpocząć aplikacje oparte na chmurze tego hello administratora usługi Azure AD ma udzielić dostępu do.</span><span class="sxs-lookup"><span data-stu-id="d33cf-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="d33cf-105">Te aplikacje są skonfigurowane w imieniu użytkownika hello w portalu usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="d33cf-106">Aplikacja Hello musi być prawidłowo skonfigurowane i przypisane toohello użytkownika lub grupy hello użytkownika jest członkiem grupy aplikacji hello toosee w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="d33cf-107">Typ Hello aplikacje, które użytkownik może być widoczny spadek hello następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="d33cf-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="d33cf-108">Aplikacje pakietu Office 365</span><span class="sxs-lookup"><span data-stu-id="d33cf-108">Office 365 Applications</span></span>

-   <span data-ttu-id="d33cf-109">Aplikacje firmy Microsoft i innych firm skonfigurowaną na podstawie federacyjnego logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="d33cf-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="d33cf-110">Aplikacje oparte na hasłach logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="d33cf-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="d33cf-111">Aplikacje z istniejącymi rozwiązaniami do logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="d33cf-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="d33cf-112">Ogólne problemy toocheck najpierw</span><span class="sxs-lookup"><span data-stu-id="d33cf-112">General issues toocheck first</span></span>

-   <span data-ttu-id="d33cf-113">Jeśli aplikacja właśnie dodano użytkownika tooa, spróbuj toosign i wylogowywanie ponownie do panelu dostępu użytkownika powitania po kilku minutach toosee Jeśli dodawana jest aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="d33cf-114">Jeśli licencji właśnie został usunięty z użytkownik lub grupa hello użytkownik jest członkiem to może zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy toobe zmiany wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="d33cf-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="d33cf-115">Zezwalaj na dodatkowy czas przed zalogowaniem się do hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="d33cf-116">Problemy konfiguracji tooapplication pokrewne</span><span class="sxs-lookup"><span data-stu-id="d33cf-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="d33cf-117">Aplikacja może być wyświetlana w panelu dostępu użytkownika, ponieważ nie został prawidłowo skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="d33cf-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="d33cf-118">Poniżej przedstawiono kilka sposobów, można rozwiązywać problemy dotyczące powiązanych tooapplication konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="d33cf-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="d33cf-119">Jak tooconfigure federacyjne logowanie jednokrotne dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="d33cf-120">Jak tooconfigure federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="d33cf-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="d33cf-121">Jak tooconfigure hasła pojedynczy aplikacji logowania jednokrotnego w galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="d33cf-122">Jak tooconfigure hasła pojedynczego logowania do aplikacji dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="d33cf-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="d33cf-123">Jak tooconfigure federacyjne logowanie jednokrotne dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="d33cf-124">Wszystkie aplikacje w galerii Azure AD hello włączone możliwości przedsiębiorstwa rejestracji jednokrotnej ma dostępne samouczek krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="d33cf-125">Dostęp można uzyskać hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="d33cf-126">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="d33cf-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="d33cf-127">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="d33cf-128">Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="d33cf-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="d33cf-129">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="d33cf-130">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d33cf-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="d33cf-131">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="d33cf-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="d33cf-132">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="d33cf-133">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-134">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="d33cf-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="d33cf-135">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-136">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-137">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-138">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="d33cf-139">W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** , nazwa typu hello aplikacji hello sekcji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="d33cf-140">Wybierz aplikację hello ma tooconfigure dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="d33cf-141">Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="d33cf-142">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="d33cf-143">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="d33cf-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="d33cf-144">Konfigurowanie rejestracji jednokrotnej dla aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="d33cf-145">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-146">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-147">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-148">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-149">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-150">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d33cf-151">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-152">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d33cf-153">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-154">Wybierz **na języku SAML logowania jednokrotnego** z hello **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="d33cf-155">Wprowadź wartości hello wymagane w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="d33cf-156">Te wartości należy uzyskać od dostawcy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="d33cf-157">Aplikacja hello tooconfigure jako logowanie Jednokrotne zainicjowane SP, hello logowania na adres URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d33cf-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="d33cf-158">Dla pewnych aplikacji hello identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d33cf-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="d33cf-159">Aplikacja hello tooconfigure jako zainicjował IdP SSO hello adres URL odpowiedzi jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d33cf-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="d33cf-160">Dla pewnych aplikacji hello identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d33cf-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="d33cf-161">**Opcjonalnie:** kliknij **Pokaż zaawansowane ustawienia adresu URL** Jeśli chcesz toosee hello — wymagane wartości.</span><span class="sxs-lookup"><span data-stu-id="d33cf-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="d33cf-162">W hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="d33cf-163">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="d33cf-164">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="d33cf-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="d33cf-165">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-165">click **Add attribute**.</span></span> <span data-ttu-id="d33cf-166">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="d33cf-167">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-167">click **Save.**</span></span> <span data-ttu-id="d33cf-168">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="d33cf-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="d33cf-169">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="d33cf-170">Ponadto ma hello metadane z adresów URL i certyfikatu wymaganego toosetup rejestracji Jednokrotnej z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="d33cf-171">Kliknij przycisk **zapisać** toosave hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="d33cf-172">Przypisywanie użytkowników toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="d33cf-173">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="d33cf-174">tooselect hello identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-175">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-176">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-177">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-178">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-179">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d33cf-180">Jeśli nie ma aplikacji hello ma tooshow tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-181">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d33cf-182">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-183">W obszarze hello **atrybuty użytkownika** zaznacz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="d33cf-184">Hello zaznaczoną opcję musi mieć wartość oczekiwana hello toomatch użytkownika hello tooauthenticate aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="d33cf-185">Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="d33cf-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="d33cf-186">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="d33cf-187">atrybuty użytkownika tooadd, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="d33cf-188">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="d33cf-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="d33cf-189">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-189">click **Add attribute**.</span></span> <span data-ttu-id="d33cf-190">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="d33cf-191">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-191">click **Save.**</span></span> <span data-ttu-id="d33cf-192">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="d33cf-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="d33cf-193">Pobieranie metadanych usługi Azure AD hello lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="d33cf-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="d33cf-194">metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-195">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-196">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-197">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-198">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-199">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d33cf-200">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-201">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d33cf-202">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-203">Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="d33cf-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="d33cf-204">W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="d33cf-205">Usługi Azure AD nie udostępnia metadane hello tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d33cf-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="d33cf-206">można pobrać metadanych Hello jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="d33cf-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="d33cf-207">Jak tooconfigure federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="d33cf-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="d33cf-208">tooconfigure aplikacji z systemem innym niż galerii, potrzebujesz toohave usługi Azure AD premium oraz aplikacja hello obsługuje SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="d33cf-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="d33cf-209">Aby uzyskać więcej informacji o wersji usługi Azure AD, odwiedź stronę [cennik usługi Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="d33cf-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="d33cf-210">Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="d33cf-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="d33cf-211">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="d33cf-212">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d33cf-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="d33cf-213">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="d33cf-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="d33cf-214">Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="d33cf-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="d33cf-215">tooconfigure logowanie jednokrotne dla aplikacji, która nie znajduje się w galerii Azure AD hello, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-216">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-217">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-218">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-219">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-220">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="d33cf-221">Kliknij przycisk **Non galerii aplikacji** w hello **dodać własną aplikację** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="d33cf-222">Wprowadź nazwę aplikacji hello hello w hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="d33cf-223">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="d33cf-224">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="d33cf-225">Wybierz **na języku SAML logowania jednokrotnego** w hello **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="d33cf-226">Wprowadź wartości hello wymagane w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="d33cf-227">Te wartości należy uzyskać od dostawcy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="d33cf-228">Aplikacja hello tooconfigure jako logowanie Jednokrotne zainicjowane przez dostawców tożsamości, wprowadź hello adres URL odpowiedzi i hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d33cf-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="d33cf-229">**Opcjonalnie:** aplikacji hello tooconfigure jako logowanie Jednokrotne zainicjowane SP, hello znaku w adresie URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d33cf-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="d33cf-230">W hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="d33cf-231">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="d33cf-232">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="d33cf-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="d33cf-233">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-233">click **Add attribute**.</span></span> <span data-ttu-id="d33cf-234">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="d33cf-235">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-235">Click **Save.**</span></span> <span data-ttu-id="d33cf-236">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="d33cf-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="d33cf-237">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="d33cf-238">Ponadto ma Azure AD adresy URL i certyfikatu wymaganego dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="d33cf-239">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="d33cf-240">tooselect hello identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-241">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-242">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-243">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-244">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-245">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d33cf-246">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-247">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d33cf-248">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-249">W obszarze hello **atrybuty użytkownika** zaznacz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="d33cf-250">Hello zaznaczoną opcję musi mieć wartość oczekiwana hello toomatch użytkownika hello tooauthenticate aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="d33cf-251">Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="d33cf-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="d33cf-252">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="d33cf-253">atrybuty użytkownika tooadd, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="d33cf-254">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="d33cf-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="d33cf-255">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-255">click **Add attribute**.</span></span> <span data-ttu-id="d33cf-256">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="d33cf-257">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-257">Click **Save.**</span></span> <span data-ttu-id="d33cf-258">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="d33cf-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="d33cf-259">Pobieranie metadanych usługi Azure AD hello lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="d33cf-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="d33cf-260">metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-261">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-262">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-263">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-264">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-265">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d33cf-266">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-267">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d33cf-268">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-269">Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="d33cf-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="d33cf-270">W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="d33cf-271">Usługi Azure AD nie udostępnia metadane hello tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d33cf-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="d33cf-272">można pobrać metadanych Hello jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="d33cf-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="d33cf-273">Jak hasło tooconfigure logowanie jednokrotne dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="d33cf-274">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="d33cf-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="d33cf-275">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="d33cf-276">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="d33cf-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="d33cf-277">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d33cf-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="d33cf-278">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-279">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="d33cf-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="d33cf-280">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-281">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-282">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-283">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="d33cf-284">W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** , nazwa typu hello aplikacji hello sekcji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="d33cf-285">Wybierz aplikację hello ma tooconfigure dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="d33cf-286">Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="d33cf-287">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="d33cf-288">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="d33cf-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="d33cf-289">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="d33cf-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="d33cf-290">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-291">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-292">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-293">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-294">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-295">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d33cf-296">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-297">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d33cf-298">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-299">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="d33cf-300">[Przypisywanie użytkowników aplikacji toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="d33cf-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="d33cf-301">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="d33cf-302">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="d33cf-303">Jak hasło tooconfigure logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="d33cf-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="d33cf-304">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="d33cf-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="d33cf-305">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="d33cf-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="d33cf-306">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="d33cf-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="d33cf-307">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="d33cf-307">Add a non-gallery application</span></span>

<span data-ttu-id="d33cf-308">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-309">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="d33cf-310">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-311">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-312">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-313">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="d33cf-314">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="d33cf-315">Wprowadź nazwę aplikacji hello w hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d33cf-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="d33cf-316">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-316">Select **Add.**</span></span>

<span data-ttu-id="d33cf-317">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="d33cf-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="d33cf-318">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="d33cf-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="d33cf-319">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-320">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d33cf-321">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-322">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-323">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-324">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="d33cf-325">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-326">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d33cf-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d33cf-327">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-328">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="d33cf-329">Wprowadź hello **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="d33cf-330">Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="d33cf-331">Upewnij się, że hello logowania pola są widoczne na powitania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d33cf-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="d33cf-332">[Przypisywanie użytkowników aplikacji toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="d33cf-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="d33cf-333">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="d33cf-334">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="d33cf-335">Toousers aplikacji powiązanych tooassigning problemów</span><span class="sxs-lookup"><span data-stu-id="d33cf-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="d33cf-336">Użytkownik może nie być widoczny aplikacji na ich Panel dostępu, ponieważ nie zostały przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="d33cf-337">Poniżej przedstawiono niektóre toocheck sposobów:</span><span class="sxs-lookup"><span data-stu-id="d33cf-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="d33cf-338">Sprawdź, czy użytkownik jest przypisany toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="d33cf-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="d33cf-339">Jak tooassign bezpośrednio aplikację tooan użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="d33cf-340">Sprawdź, czy użytkownik jest przypisany licencji tooa powiązane toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="d33cf-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="d33cf-341">Jak tooassign użytkownika tooa licencji</span><span class="sxs-lookup"><span data-stu-id="d33cf-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="d33cf-342">Sprawdź, czy użytkownik jest przypisany toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="d33cf-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="d33cf-343">toocheck Jeśli użytkownik jest przypisany toohello aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-344">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d33cf-345">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-346">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-347">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-348">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="d33cf-349">**Wyszukiwanie** hello nazwy aplikacji hello jest zagrożona.</span><span class="sxs-lookup"><span data-stu-id="d33cf-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="d33cf-350">Kliknij przycisk **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="d33cf-351">Określ, czy toosee użytkownikowi przypisano toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="d33cf-352">Jeśli nie, wykonaj kroki hello "jak tooassign bezpośrednio aplikację tooan użytkownika" toodo tak.</span><span class="sxs-lookup"><span data-stu-id="d33cf-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="d33cf-353">Jak tooassign bezpośrednio aplikację tooan użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="d33cf-354">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-355">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="d33cf-356">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-357">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-358">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-359">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d33cf-360">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-361">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d33cf-362">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-363">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d33cf-364">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d33cf-365">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d33cf-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d33cf-366">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d33cf-367">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d33cf-368">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="d33cf-369">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d33cf-370">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="d33cf-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="d33cf-371">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d33cf-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="d33cf-372">Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="d33cf-373">Sprawdź, czy użytkownik jest objętych licencją powiązane toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="d33cf-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="d33cf-374">toocheck użytkownika przypisane licencje, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-375">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d33cf-376">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-377">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-378">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-379">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-379">click **All users**.</span></span>

6.  <span data-ttu-id="d33cf-380">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d33cf-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d33cf-381">Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="d33cf-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="d33cf-382">Jeśli użytkownik hello jest tooan przypisanej licencji pakietu Office to włączenie tooappear aplikacji pierwszej strony pakietu Office na panelu dostępu hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="d33cf-383">Jak tooassign użytkownika licencji</span><span class="sxs-lookup"><span data-stu-id="d33cf-383">How tooassign a user a license</span></span> 

<span data-ttu-id="d33cf-384">tooassign tooa licencji użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-385">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d33cf-386">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-387">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-388">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-389">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-389">click **All users**.</span></span>

6.  <span data-ttu-id="d33cf-390">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d33cf-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d33cf-391">Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="d33cf-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="d33cf-392">Kliknij przycisk hello **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="d33cf-393">Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="d33cf-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="d33cf-394">**Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów.</span><span class="sxs-lookup"><span data-stu-id="d33cf-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="d33cf-395">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="d33cf-396">Kliknij przycisk hello **przypisać** przycisk tooassign użytkownika toothis tych licencji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="d33cf-397">Toogroups aplikacji powiązanych tooassigning problemów</span><span class="sxs-lookup"><span data-stu-id="d33cf-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="d33cf-398">Użytkownik może być widoczny aplikacji na ich Panel dostępu, ponieważ są one częścią grupy przypisanej do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="d33cf-399">Poniżej przedstawiono niektóre toocheck sposobów:</span><span class="sxs-lookup"><span data-stu-id="d33cf-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="d33cf-400">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="d33cf-401">Jak tooassign tooa aplikacji grupy bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="d33cf-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="d33cf-402">Sprawdź, czy użytkownik jest częścią grupy przypisane tooa licencji</span><span class="sxs-lookup"><span data-stu-id="d33cf-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="d33cf-403">Jak tooassign tooa grupy licencji</span><span class="sxs-lookup"><span data-stu-id="d33cf-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="d33cf-404">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="d33cf-404">Check a user’s group memberships</span></span>

<span data-ttu-id="d33cf-405">toocheck członkostwa w grupie, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-406">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d33cf-407">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-408">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-409">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-410">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-410">click **All users**.</span></span>

6.  <span data-ttu-id="d33cf-411">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d33cf-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d33cf-412">Kliknij przycisk **grup**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-412">click **Groups**.</span></span>

8.  <span data-ttu-id="d33cf-413">Określ, czy toosee użytkownika jest częścią grupy przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="d33cf-414">Jeśli chcesz, aby tooremove hello użytkownika z grupy hello **kliknij wiersz hello** hello grupy i wybierz opcję Usuń.</span><span class="sxs-lookup"><span data-stu-id="d33cf-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="d33cf-415">Jak tooassign tooa aplikacji grupy bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="d33cf-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="d33cf-416">tooassign jeden lub więcej grup tooan aplikacji bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-417">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="d33cf-418">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-419">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-420">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33cf-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-421">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d33cf-422">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d33cf-423">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d33cf-424">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d33cf-425">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d33cf-426">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d33cf-427">Typ w hello **grupy Pełna nazwa** grupy hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d33cf-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d33cf-428">Umieść kursor nad hello **grupy** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d33cf-429">Kliknij przycisk hello wyboru dalej toohello grupy profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d33cf-430">**Opcjonalnie:** czy zbyt**dodać więcej niż jednej grupy**, typu w innym **grupy Pełna nazwa** do hello **wyszukiwanie według nazwy lub adresu e-mail** pole wyszukiwania, i kliknij przycisk tooadd wyboru hello toohello tej grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="d33cf-431">Po wybraniu grup kliknij hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d33cf-432">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** grupach bloku tooselect toohello tooassign roli zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="d33cf-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="d33cf-433">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybrane grupy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="d33cf-434">Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="d33cf-435">Sprawdź, czy użytkownik jest częścią grupy przypisane tooa licencji</span><span class="sxs-lookup"><span data-stu-id="d33cf-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="d33cf-436">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d33cf-437">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-438">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-439">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-440">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-440">click **All users**.</span></span>

6.  <span data-ttu-id="d33cf-441">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d33cf-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d33cf-442">Kliknij przycisk **grup**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-442">click **Groups**.</span></span>

8.  <span data-ttu-id="d33cf-443">Kliknij wiersz hello określonej grupy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="d33cf-444">Kliknij przycisk **licencji** toosee grupy hello licencji, do której przypisany tooit.</span><span class="sxs-lookup"><span data-stu-id="d33cf-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="d33cf-445">Jeśli grupa hello jest tooan przypisanej licencji pakietu Office może to włączenie niektórych tooappear aplikacji pierwszej strony pakietu Office na panelu dostępu hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33cf-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="d33cf-446">Jak tooassign tooa grupy licencji</span><span class="sxs-lookup"><span data-stu-id="d33cf-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="d33cf-447">tooassign tooa grupę licencji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d33cf-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="d33cf-448">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="d33cf-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d33cf-449">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d33cf-450">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d33cf-451">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="d33cf-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d33cf-452">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="d33cf-452">click **All groups**.</span></span>

6.  <span data-ttu-id="d33cf-453">**Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d33cf-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d33cf-454">Kliknij przycisk **licencji** toosee grupy hello licencji, do której obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="d33cf-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="d33cf-455">Kliknij przycisk hello **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d33cf-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="d33cf-456">Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="d33cf-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="d33cf-457">**Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów.</span><span class="sxs-lookup"><span data-stu-id="d33cf-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="d33cf-458">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="d33cf-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="d33cf-459">Kliknij przycisk hello **przypisać** przycisk tooassign grupy toothis tych licencji.</span><span class="sxs-lookup"><span data-stu-id="d33cf-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="d33cf-460">Może to zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy.</span><span class="sxs-lookup"><span data-stu-id="d33cf-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="d33cf-461">toodo to szybsze, należy wziąć pod uwagę tymczasowo przypisywanie licencji użytkownika toohello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="d33cf-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="d33cf-462">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d33cf-462">Next steps</span></span>
[<span data-ttu-id="d33cf-463">Dodaj nowy tooAzure użytkowników usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="d33cf-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

