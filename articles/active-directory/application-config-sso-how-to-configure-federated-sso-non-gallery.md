---
title: "aaaHow tooconfigure federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii niestandardowych, które mają toointegrate z usługą Azure AD"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="cb0a6-103">Jak tooconfigure federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="cb0a6-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="cb0a6-104">tooconfigure aplikacji z systemem innym niż galerii, potrzebujesz toohave usługi Azure AD premium oraz aplikacja hello obsługuje SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="cb0a6-105">Aby uzyskać więcej informacji o wersji usługi Azure AD, odwiedź stronę [cennik usługi Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="cb0a6-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="cb0a6-106">Omówienie kroków wymaganych</span><span class="sxs-lookup"><span data-stu-id="cb0a6-106">Overview of steps required</span></span>
<span data-ttu-id="cb0a6-107">Poniżej znajduje się wysokiego poziomu omówienie hello kroki wymagane tooconfigure federacyjne logowanie jednokrotne z systemem innym niż galerii (np. niestandardowe) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="cb0a6-108">Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="cb0a6-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="cb0a6-109">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="cb0a6-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="cb0a6-110">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="cb0a6-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="cb0a6-111">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="cb0a6-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="cb0a6-112">Przypisywanie użytkowników toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="cb0a6-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="cb0a6-113">Konfigurowanie aplikacji pojedynczego logowania jednokrotnego toonon galerii</span><span class="sxs-lookup"><span data-stu-id="cb0a6-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="cb0a6-114">tooconfigure logowanie jednokrotne dla aplikacji, która nie znajduje się w galerii Azure AD hello, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="cb0a6-115">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cb0a6-116">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cb0a6-117">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cb0a6-118">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cb0a6-119">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="cb0a6-120">Kliknij przycisk **Non galerii aplikacji** w hello **dodać własną aplikację** sekcji</span><span class="sxs-lookup"><span data-stu-id="cb0a6-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="cb0a6-121">Wprowadź nazwę aplikacji hello hello w hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="cb0a6-122">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="cb0a6-123">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="cb0a6-124">Wybierz **na języku SAML logowania jednokrotnego** w hello **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="cb0a6-125">Wprowadź wartości hello wymagane w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="cb0a6-126">Te wartości należy uzyskać od dostawcy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="cb0a6-127">Aplikacja hello tooconfigure jako logowanie Jednokrotne zainicjowane przez dostawców tożsamości, wprowadź hello adres URL odpowiedzi i hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="cb0a6-128">**Opcjonalnie:** aplikacji hello tooconfigure jako logowanie Jednokrotne zainicjowane SP, hello znaku w adresie URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="cb0a6-129">W hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="cb0a6-130">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="cb0a6-131">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="cb0a6-132">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-132">click **Add attribute**.</span></span> <span data-ttu-id="cb0a6-133">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="cb0a6-134">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-134">Click **Save.**</span></span> <span data-ttu-id="cb0a6-135">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="cb0a6-136">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="cb0a6-137">Ponadto ma Azure AD adresy URL i certyfikatu wymaganego dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="cb0a6-138">Przypisywanie użytkowników toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="cb0a6-139">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="cb0a6-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="cb0a6-140">tooselect hello identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="cb0a6-141">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cb0a6-142">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cb0a6-143">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cb0a6-144">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cb0a6-145">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="cb0a6-146">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cb0a6-147">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="cb0a6-148">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cb0a6-149">W obszarze hello **atrybuty użytkownika** zaznacz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="cb0a6-150">Hello zaznaczoną opcję musi mieć wartość oczekiwana hello toomatch użytkownika hello tooauthenticate aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="cb0a6-151">[! Uwaga} usługi Azure AD wybierz format hello atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="cb0a6-152">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="cb0a6-153">atrybuty użytkownika tooadd, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="cb0a6-154">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="cb0a6-155">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-155">click **Add attribute**.</span></span> <span data-ttu-id="cb0a6-156">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="cb0a6-157">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-157">Click **Save.**</span></span> <span data-ttu-id="cb0a6-158">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="cb0a6-159">Pobieranie metadanych usługi Azure AD hello lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="cb0a6-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="cb0a6-160">metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="cb0a6-161">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cb0a6-162">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cb0a6-163">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cb0a6-164">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cb0a6-165">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="cb0a6-166">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cb0a6-167">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="cb0a6-168">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cb0a6-169">Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="cb0a6-170">W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="cb0a6-171">Usługi Azure AD nie udostępnia metadane hello tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="cb0a6-172">można pobrać metadanych Hello jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="cb0a6-173">Przypisywanie użytkowników toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="cb0a6-173">Assign users toohello application</span></span>

<span data-ttu-id="cb0a6-174">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="cb0a6-175">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="cb0a6-176">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cb0a6-177">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cb0a6-178">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cb0a6-179">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="cb0a6-180">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="cb0a6-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cb0a6-181">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="cb0a6-182">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cb0a6-183">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="cb0a6-184">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="cb0a6-185">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="cb0a6-186">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="cb0a6-187">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="cb0a6-188">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="cb0a6-189">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="cb0a6-190">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="cb0a6-191">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="cb0a6-192">Po krótkim czasie użytkownicy hello, wybranych będą mogli toolaunch te aplikacje przy użyciu hello metod opisanych w sekcji Opis rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="cb0a6-193">Dostosowywanie oświadczeń SAML hello wysyłane tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="cb0a6-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="cb0a6-194">toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb0a6-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb0a6-195">Next steps</span></span>
[<span data-ttu-id="cb0a6-196">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="cb0a6-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
