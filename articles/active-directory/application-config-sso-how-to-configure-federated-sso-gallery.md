---
title: "Jak skonfigurować federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować federacyjne logowanie jednokrotne dla istniejącej aplikacji usługi Azure AD galerii i zacząć szybko przy użyciu samouczki"
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
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="d49e5-103">Jak skonfigurować federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d49e5-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="d49e5-104">Wszystkie aplikacje w galerii Azure AD włączone możliwości przedsiębiorstwa pojedynczego logowania ma dostępne samouczek krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="d49e5-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="d49e5-105">Dostęp można uzyskać [lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="d49e5-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="d49e5-106">Omówienie kroków wymaganych</span><span class="sxs-lookup"><span data-stu-id="d49e5-106">Overview of steps required</span></span>
<span data-ttu-id="d49e5-107">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="d49e5-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="d49e5-108">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d49e5-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="d49e5-109">Skonfiguruj wartości metadanych aplikacji w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="d49e5-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="d49e5-110">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d49e5-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="d49e5-111">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d49e5-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="d49e5-112">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="d49e5-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="d49e5-113">Przypisywanie użytkowników do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d49e5-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="d49e5-114">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d49e5-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="d49e5-115">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d49e5-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="d49e5-116">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="d49e5-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="d49e5-117">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d49e5-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d49e5-118">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d49e5-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d49e5-119">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d49e5-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d49e5-120">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="d49e5-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="d49e5-121">W **wprowadź nazwę** pole tekstowe z **Dodaj z galerii** wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="d49e5-122">Wybierz aplikację, którą chcesz skonfigurować pod kątem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d49e5-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="d49e5-123">Przed dodaniem aplikacji, można zmienić jego nazwę z **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d49e5-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="d49e5-124">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d49e5-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="d49e5-125">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="d49e5-126">Konfigurowanie rejestracji jednokrotnej dla aplikacji z galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="d49e5-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="d49e5-127">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d49e5-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="d49e5-128">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **współadministrator**.</span><span class="sxs-lookup"><span data-stu-id="d49e5-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="d49e5-129">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d49e5-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d49e5-130">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d49e5-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d49e5-131">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d49e5-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d49e5-132">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="d49e5-133">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d49e5-134">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d49e5-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="d49e5-135">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d49e5-136">Wybierz **na języku SAML logowania jednokrotnego** z **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d49e5-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="d49e5-137">Wprowadź wymagane wartości w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="d49e5-138">Te wartości należy uzyskać od dostawcy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="d49e5-139">Aby skonfigurować aplikację jako logowanie Jednokrotne zainicjowane SP, zaloguj się na adres URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d49e5-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="d49e5-140">Dla pewnych aplikacji identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d49e5-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="d49e5-141">Aby skonfigurować aplikację jako logowanie Jednokrotne zainicjowane IdP, adres URL odpowiedzi jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d49e5-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="d49e5-142">Dla pewnych aplikacji identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="d49e5-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="d49e5-143">**Opcjonalnie:** kliknij **Pokaż zaawansowane ustawienia adresu URL** Jeśli chcesz zobaczyć wartości innych niż wymagana.</span><span class="sxs-lookup"><span data-stu-id="d49e5-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="d49e5-144">W **atrybuty użytkownika**, wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d49e5-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="d49e5-145">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d49e5-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="d49e5-146">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="d49e5-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="d49e5-147">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="d49e5-147">click **Add attribute**.</span></span> <span data-ttu-id="d49e5-148">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d49e5-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="d49e5-149">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-149">Click **Save.**</span></span> <span data-ttu-id="d49e5-150">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d49e5-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="d49e5-151">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  dokumentacji dostępu na temat konfigurowania rejestracji jednokrotnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="d49e5-152">Ponadto ma metadanych adresy URL i certyfikatu wymagane do konfiguracji logowania jednokrotnego do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="d49e5-153">Kliknij przycisk **zapisać** Aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="d49e5-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="d49e5-154">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="d49e5-155">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d49e5-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="d49e5-156">Aby wybrać identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d49e5-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="d49e5-157">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d49e5-158">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d49e5-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d49e5-159">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d49e5-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d49e5-160">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d49e5-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d49e5-161">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="d49e5-162">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d49e5-163">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d49e5-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d49e5-164">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d49e5-165">W obszarze **atrybuty użytkownika** wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d49e5-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="d49e5-166">Wybrana opcja musi być zgodna z oczekiwaną wartością w aplikacji w celu uwierzytelnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d49e5-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="d49e5-167">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="d49e5-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="d49e5-168">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="d49e5-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="d49e5-169">Aby dodać atrybuty użytkownika, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d49e5-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="d49e5-170">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="d49e5-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="d49e5-171">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="d49e5-171">click **Add attribute**.</span></span> <span data-ttu-id="d49e5-172">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d49e5-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="d49e5-173">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d49e5-173">Click **Save**.</span></span> <span data-ttu-id="d49e5-174">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d49e5-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="d49e5-175">Pobieranie metadanych usługi Azure AD lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="d49e5-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="d49e5-176">Aby pobrać metadanych aplikacji lub certyfikatu z usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d49e5-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="d49e5-177">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d49e5-178">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d49e5-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d49e5-179">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d49e5-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d49e5-180">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d49e5-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d49e5-181">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="d49e5-182">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d49e5-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="d49e5-183">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d49e5-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d49e5-184">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d49e5-185">Przejdź do **certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="d49e5-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="d49e5-186">W zależności od tego, jakie aplikacji wymaga Konfigurowanie logowania jednokrotnego zobaczysz opcję, aby pobrać metadane XML albo certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d49e5-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="d49e5-187">Usługi Azure AD nie udostępnia adresu URL można pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="d49e5-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="d49e5-188">Można pobrać metadanych jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="d49e5-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="d49e5-189">Przypisywanie użytkowników do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d49e5-189">Assign users to the application</span></span>

<span data-ttu-id="d49e5-190">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d49e5-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="d49e5-191">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d49e5-192">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d49e5-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d49e5-193">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d49e5-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d49e5-194">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d49e5-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d49e5-195">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d49e5-196">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="d49e5-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d49e5-197">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="d49e5-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="d49e5-198">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d49e5-199">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="d49e5-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d49e5-200">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="d49e5-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d49e5-201">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d49e5-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d49e5-202">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="d49e5-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="d49e5-203">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="d49e5-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="d49e5-204">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="d49e5-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="d49e5-205">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="d49e5-206">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="d49e5-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="d49e5-207">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d49e5-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="d49e5-208">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji za pomocą metod opisanych w sekcji Opis rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d49e5-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="d49e5-209">Dostosowywanie oświadczeń SAML wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d49e5-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="d49e5-210">Aby dowiedzieć się, jak dostosować oświadczeń atrybutów SAML wysyłanych do aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d49e5-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d49e5-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d49e5-211">Next steps</span></span>
[<span data-ttu-id="d49e5-212">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="d49e5-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



