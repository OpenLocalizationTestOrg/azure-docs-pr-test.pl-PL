---
title: "Przypisane aplikacji nie jest wyświetlane w panelu dostępu | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z powodu aplikacji nie jest wyświetlane w panelu dostępu"
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
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="a8784-103">Przypisane aplikacji nie jest wyświetlane w panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="a8784-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="a8784-104">Panel dostępu jest oparte na sieci web portalu, która pozwala użytkownikom przy użyciu konta służbowego w usłudze Azure Active Directory (Azure AD) do wyświetlania i uruchamiania aplikacji opartej na chmurze, czy administrator usługi Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="a8784-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="a8784-105">Te aplikacje są skonfigurowane w imieniu użytkownika w portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8784-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="a8784-106">Aplikacja musi prawidłowo skonfigurowane i przypisane do użytkownika lub grupy, których użytkownik jest członkiem, aby zobaczyć aplikację w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a8784-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="a8784-107">Typ aplikacji, które użytkownik może być widoczny można podzielić na następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="a8784-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="a8784-108">Aplikacje pakietu Office 365</span><span class="sxs-lookup"><span data-stu-id="a8784-108">Office 365 Applications</span></span>

-   <span data-ttu-id="a8784-109">Aplikacje firmy Microsoft i innych firm skonfigurowaną na podstawie federacyjnego logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a8784-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="a8784-110">Aplikacje oparte na hasłach logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a8784-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="a8784-111">Aplikacje z istniejącymi rozwiązaniami do logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a8784-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="a8784-112">Ogólne problemy, aby sprawdzić w pierwszej kolejności</span><span class="sxs-lookup"><span data-stu-id="a8784-112">General issues to check first</span></span>

-   <span data-ttu-id="a8784-113">Jeśli aplikacja właśnie został dodany do użytkownika, spróbuj zarejestrować i wylogowywanie ponownie do panelu dostępu użytkownika po kilku minutach aby zobaczyć, czy aplikacja jest dodany.</span><span class="sxs-lookup"><span data-stu-id="a8784-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="a8784-114">Jeśli licencji został właśnie usunięty ze użytkownika lub grupę, których użytkownik jest członkiem to może potrwać dłuższy czas, w zależności od rozmiaru i złożoności grupy zmian wprowadzanych.</span><span class="sxs-lookup"><span data-stu-id="a8784-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="a8784-115">Zezwalaj na dodatkowy czas przed zalogowaniem się do panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a8784-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="a8784-116">Problemy związane z konfiguracją aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-116">Problems related to application configuration</span></span>

<span data-ttu-id="a8784-117">Aplikacja może być wyświetlana w panelu dostępu użytkownika, ponieważ nie został prawidłowo skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="a8784-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="a8784-118">Poniżej przedstawiono kilka sposobów, można rozwiązywać problemy związane z konfiguracją aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a8784-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="a8784-119">Konfigurowanie federacyjnych rejestracji jednokrotnej dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="a8784-120">Jak skonfigurować federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a8784-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="a8784-121">Jak skonfigurować hasła pojedynczej logowania aplikacji dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="a8784-122">Jak skonfigurować hasła pojedynczej logowania aplikacji dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a8784-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="a8784-123">Konfigurowanie federacyjnych rejestracji jednokrotnej dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="a8784-124">Wszystkie aplikacje w galerii Azure AD włączone możliwości przedsiębiorstwa rejestracji jednokrotnej ma dostępne samouczek krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="a8784-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="a8784-125">Dostęp można uzyskać [lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="a8784-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="a8784-126">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="a8784-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a8784-127">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="a8784-128">Skonfiguruj wartości metadanych aplikacji w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="a8784-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="a8784-129">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="a8784-130">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="a8784-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="a8784-131">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="a8784-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="a8784-132">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="a8784-133">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-134">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="a8784-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a8784-135">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-136">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-137">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-138">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="a8784-139">W **wprowadź nazwę** pole tekstowe z **Dodaj z galerii** wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="a8784-140">Wybierz aplikację, którą chcesz skonfigurować pod kątem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a8784-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="a8784-141">Przed dodaniem aplikacji, można zmienić jego nazwę z **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a8784-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="a8784-142">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a8784-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="a8784-143">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="a8784-144">Konfigurowanie rejestracji jednokrotnej dla aplikacji z galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="a8784-145">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-146">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-147">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-148">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-149">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-150">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a8784-151">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-152">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a8784-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a8784-153">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-154">Wybierz **na języku SAML logowania jednokrotnego** z **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="a8784-155">Wprowadź wymagane wartości w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="a8784-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="a8784-156">Te wartości należy uzyskać od dostawcy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="a8784-157">Aby skonfigurować aplikację jako logowanie Jednokrotne zainicjowane SP, zaloguj się na adres URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="a8784-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="a8784-158">Dla pewnych aplikacji identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="a8784-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="a8784-159">Aby skonfigurować aplikację jako logowanie Jednokrotne zainicjowane IdP, adres URL odpowiedzi jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="a8784-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="a8784-160">Dla pewnych aplikacji identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="a8784-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="a8784-161">**Opcjonalnie:** kliknij **Pokaż zaawansowane ustawienia adresu URL** Jeśli chcesz zobaczyć wartości innych niż wymagana.</span><span class="sxs-lookup"><span data-stu-id="a8784-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="a8784-162">W **atrybuty użytkownika**, wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="a8784-163">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="a8784-164">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="a8784-164">To add an attribute:</span></span>

   1. <span data-ttu-id="a8784-165">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="a8784-165">click **Add attribute**.</span></span> <span data-ttu-id="a8784-166">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="a8784-167">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a8784-167">click **Save.**</span></span> <span data-ttu-id="a8784-168">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a8784-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="a8784-169">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  dokumentacji dostępu na temat konfigurowania rejestracji jednokrotnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="a8784-170">Ponadto ma metadanych adresy URL i certyfikatu wymagane do konfiguracji logowania jednokrotnego do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="a8784-171">Kliknij przycisk **zapisać** Aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="a8784-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="a8784-172">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="a8784-173">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="a8784-174">Aby wybrać identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-175">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-176">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-177">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-178">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-179">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a8784-180">Jeśli nie widzisz aplikacji ma być wyświetlane w tym miejscu, należy użyć **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-181">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a8784-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="a8784-182">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-183">W obszarze **atrybuty użytkownika** wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="a8784-184">Wybrana opcja musi być zgodna z oczekiwaną wartością w aplikacji w celu uwierzytelnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="a8784-185">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="a8784-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="a8784-186">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="a8784-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="a8784-187">Aby dodać atrybuty użytkownika, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="a8784-188">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="a8784-188">To add an attribute:</span></span>

   1. <span data-ttu-id="a8784-189">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="a8784-189">click **Add attribute**.</span></span> <span data-ttu-id="a8784-190">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="a8784-191">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a8784-191">click **Save.**</span></span> <span data-ttu-id="a8784-192">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a8784-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="a8784-193">Pobieranie metadanych usługi Azure AD lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="a8784-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="a8784-194">Aby pobrać metadanych aplikacji lub certyfikatu z usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-195">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-196">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-197">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-198">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-199">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a8784-200">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-201">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a8784-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="a8784-202">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-203">Przejdź do **certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="a8784-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="a8784-204">W zależności od tego, jakie aplikacji wymaga Konfigurowanie logowania jednokrotnego zobaczysz opcję, aby pobrać metadane XML albo certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a8784-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="a8784-205">Usługi Azure AD nie udostępnia adresu URL można pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="a8784-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="a8784-206">Można pobrać metadanych jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="a8784-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a8784-207">Jak skonfigurować federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a8784-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a8784-208">Aby skonfigurować aplikację z systemem innym niż galerii, musisz mieć usługi Azure AD premium, a aplikacja obsługuje SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="a8784-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="a8784-209">Aby uzyskać więcej informacji o wersji usługi Azure AD, odwiedź stronę [cennik usługi Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="a8784-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="a8784-210">Skonfiguruj wartości metadanych aplikacji w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="a8784-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="a8784-211">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="a8784-212">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="a8784-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="a8784-213">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="a8784-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="a8784-214">Skonfiguruj wartości metadanych aplikacji w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="a8784-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="a8784-215">Aby skonfigurować logowanie jednokrotne dla aplikacji, która nie znajduje się w galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-216">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-217">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-218">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-219">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-220">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="a8784-221">Kliknij przycisk **Non galerii aplikacji** w **dodać własną aplikację** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a8784-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="a8784-222">Wprowadź nazwę aplikacji w **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a8784-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="a8784-223">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a8784-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="a8784-224">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="a8784-225">Wybierz **na języku SAML logowania jednokrotnego** w **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="a8784-226">Wprowadź wymagane wartości w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="a8784-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="a8784-227">Te wartości należy uzyskać od dostawcy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="a8784-228">Aby skonfigurować aplikację jako SSO inicjowanych przez dostawców tożsamości, wprowadź adres URL odpowiedzi i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a8784-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="a8784-229">**Opcjonalnie:** Konfigurowanie aplikacji jako logowanie Jednokrotne zainicjowane SP, zaloguj się na adres URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="a8784-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="a8784-230">W **atrybuty użytkownika**, wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="a8784-231">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="a8784-232">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="a8784-232">To add an attribute:</span></span>

   1. <span data-ttu-id="a8784-233">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="a8784-233">click **Add attribute**.</span></span> <span data-ttu-id="a8784-234">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="a8784-235">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a8784-235">Click **Save.**</span></span> <span data-ttu-id="a8784-236">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a8784-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="a8784-237">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  dokumentacji dostępu na temat konfigurowania rejestracji jednokrotnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="a8784-238">Ponadto ma Azure AD adresy URL i certyfikatu wymaganego dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="a8784-239">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="a8784-240">Aby wybrać identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-241">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-242">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-243">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-244">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-245">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a8784-246">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-247">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a8784-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="a8784-248">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-249">W obszarze **atrybuty użytkownika** wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="a8784-250">Wybrana opcja musi być zgodna z oczekiwaną wartością w aplikacji w celu uwierzytelnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="a8784-251">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="a8784-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="a8784-252">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="a8784-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="a8784-253">Aby dodać atrybuty użytkownika, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="a8784-254">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="a8784-254">To add an attribute:</span></span>

   1. <span data-ttu-id="a8784-255">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="a8784-255">click **Add attribute**.</span></span> <span data-ttu-id="a8784-256">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8784-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="a8784-257">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a8784-257">Click **Save.**</span></span> <span data-ttu-id="a8784-258">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a8784-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="a8784-259">Pobieranie metadanych usługi Azure AD lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="a8784-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="a8784-260">Aby pobrać metadanych aplikacji lub certyfikatu z usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-261">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-262">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-263">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-264">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-265">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a8784-266">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-267">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a8784-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="a8784-268">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-269">Przejdź do **certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="a8784-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="a8784-270">W zależności od tego, jakie aplikacji wymaga Konfigurowanie logowania jednokrotnego zobaczysz opcję, aby pobrać metadane XML albo certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a8784-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="a8784-271">Usługi Azure AD nie udostępnia adresu URL można pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="a8784-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="a8784-272">Można pobrać metadanych jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="a8784-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="a8784-273">Jak skonfigurować hasło rejestracji jednokrotnej dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="a8784-274">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="a8784-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a8784-275">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="a8784-276">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a8784-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="a8784-277">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8784-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="a8784-278">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-279">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="a8784-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a8784-280">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-281">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-282">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-283">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="a8784-284">W **wprowadź nazwę** pole tekstowe z **Dodaj z galerii** wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="a8784-285">Wybierz aplikację, którą chcesz skonfigurować pod kątem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a8784-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="a8784-286">Przed dodaniem aplikacji, można zmienić jego nazwę z **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a8784-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="a8784-287">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a8784-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="a8784-288">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="a8784-289">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a8784-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="a8784-290">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-291">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-292">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-293">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-294">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-295">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a8784-296">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-297">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a8784-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a8784-298">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-299">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a8784-300">[Przypisywanie użytkowników do aplikacji](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="a8784-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="a8784-301">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a8784-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="a8784-302">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="a8784-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a8784-303">Jak skonfigurować hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a8784-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a8784-304">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="a8784-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a8784-305">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a8784-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="a8784-306">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a8784-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="a8784-307">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a8784-307">Add a non-gallery application</span></span>

<span data-ttu-id="a8784-308">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-309">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.</span><span class="sxs-lookup"><span data-stu-id="a8784-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="a8784-310">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-311">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-312">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-313">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="a8784-314">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="a8784-315">Wprowadź nazwę aplikacji w **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a8784-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="a8784-316">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="a8784-316">Select **Add.**</span></span>

<span data-ttu-id="a8784-317">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="a8784-318">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a8784-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="a8784-319">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-320">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a8784-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8784-321">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-322">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-323">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-324">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="a8784-325">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-326">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a8784-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a8784-327">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-328">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a8784-329">Wprowadź **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="a8784-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="a8784-330">Jest to adres URL, których użytkownicy wprowadzić swoją nazwę i hasło do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="a8784-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="a8784-331">Upewnij się, że logowanie pola są widoczne pod adresem URL.</span><span class="sxs-lookup"><span data-stu-id="a8784-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="a8784-332">[Przypisywanie użytkowników do aplikacji](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="a8784-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="a8784-333">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a8784-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="a8784-334">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="a8784-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="a8784-335">Problemy związane z przypisywaniem aplikacji dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="a8784-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="a8784-336">Użytkownik może nie być widoczny aplikacji na ich Panel dostępu, ponieważ nie są przypisane do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="a8784-337">Poniżej przedstawiono kilka sposobów, aby sprawdzić:</span><span class="sxs-lookup"><span data-stu-id="a8784-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="a8784-338">Sprawdź, czy użytkownik jest przypisany do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="a8784-339">Jak przypisać użytkownika bezpośrednio do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="a8784-340">Sprawdź, czy użytkownik jest przypisany do licencji związanych z aplikacją</span><span class="sxs-lookup"><span data-stu-id="a8784-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="a8784-341">Jak przypisać licencję do użytkownika</span><span class="sxs-lookup"><span data-stu-id="a8784-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="a8784-342">Sprawdź, czy użytkownik jest przypisany do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="a8784-343">Aby sprawdzić, czy użytkownik jest przypisany do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-344">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a8784-345">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-346">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-347">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-348">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="a8784-349">**Wyszukiwanie** nazwy w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="a8784-350">Kliknij przycisk **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a8784-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="a8784-351">Sprawdź, czy użytkownika jest przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="a8784-352">Jeśli nie, wykonaj kroki opisane w artykule "Jak bezpośrednio przypisać użytkownika do aplikacji" w tym celu.</span><span class="sxs-lookup"><span data-stu-id="a8784-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="a8784-353">Jak przypisać użytkownika bezpośrednio do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="a8784-354">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-355">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego**.</span><span class="sxs-lookup"><span data-stu-id="a8784-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="a8784-356">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-357">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-358">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-359">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a8784-360">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-361">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="a8784-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="a8784-362">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-363">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a8784-364">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a8784-365">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a8784-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a8784-366">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="a8784-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="a8784-367">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="a8784-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="a8784-368">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="a8784-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="a8784-369">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="a8784-370">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="a8784-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="a8784-371">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a8784-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="a8784-372">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a8784-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="a8784-373">Sprawdź, czy użytkownik jest w ramach licencji, związanych z aplikacją</span><span class="sxs-lookup"><span data-stu-id="a8784-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="a8784-374">Aby sprawdzić przypisane licencje użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-375">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a8784-376">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-377">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-378">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="a8784-379">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a8784-379">click **All users**.</span></span>

6.  <span data-ttu-id="a8784-380">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="a8784-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="a8784-381">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje użytkownika został przypisany.</span><span class="sxs-lookup"><span data-stu-id="a8784-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="a8784-382">Jeśli użytkownik jest przypisany do pakietu Office licencji tego Włącz pierwszej strony aplikacjach pakietu Office są wyświetlane w panelu dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="a8784-383">Jak przypisać licencję użytkownika</span><span class="sxs-lookup"><span data-stu-id="a8784-383">How to assign a user a license</span></span> 

<span data-ttu-id="a8784-384">Aby przypisać licencję do użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-385">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a8784-386">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-387">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-388">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="a8784-389">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a8784-389">click **All users**.</span></span>

6.  <span data-ttu-id="a8784-390">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="a8784-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="a8784-391">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje użytkownika został przypisany.</span><span class="sxs-lookup"><span data-stu-id="a8784-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="a8784-392">Kliknij przycisk **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a8784-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="a8784-393">Wybierz **jeden lub więcej produktów** z listy dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="a8784-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="a8784-394">**Opcjonalne** kliknij **opcje przydziału** element, aby przypisać częściami produktów.</span><span class="sxs-lookup"><span data-stu-id="a8784-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="a8784-395">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="a8784-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="a8784-396">Kliknij przycisk **przypisać** przycisk, aby przypisać licencje do tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="a8784-397">Problemy związane z przypisywanie aplikacji do grupy</span><span class="sxs-lookup"><span data-stu-id="a8784-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="a8784-398">Użytkownik może być widoczny aplikacji na ich Panel dostępu, ponieważ są one częścią grupy przypisanej do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="a8784-399">Poniżej przedstawiono kilka sposobów, aby sprawdzić:</span><span class="sxs-lookup"><span data-stu-id="a8784-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="a8784-400">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="a8784-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="a8784-401">Jak przypisać bezpośrednio do grupy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="a8784-402">Sprawdź, czy użytkownik jest częścią grupy przypisane do licencji</span><span class="sxs-lookup"><span data-stu-id="a8784-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="a8784-403">Jak przypisać licencję do grupy</span><span class="sxs-lookup"><span data-stu-id="a8784-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="a8784-404">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="a8784-404">Check a user’s group memberships</span></span>

<span data-ttu-id="a8784-405">Aby sprawdzić członkostwa w grupie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-406">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a8784-407">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-408">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-409">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="a8784-410">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a8784-410">click **All users**.</span></span>

6.  <span data-ttu-id="a8784-411">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="a8784-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="a8784-412">Kliknij przycisk **grup**.</span><span class="sxs-lookup"><span data-stu-id="a8784-412">click **Groups**.</span></span>

8.  <span data-ttu-id="a8784-413">Sprawdź, czy użytkownika jest częścią grupy przypisane do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="a8784-414">Jeśli chcesz usunąć użytkownika z grupy, **kliknij wiersz** grupy i wybierz opcję Usuń.</span><span class="sxs-lookup"><span data-stu-id="a8784-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="a8784-415">Jak przypisać bezpośrednio do grupy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8784-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="a8784-416">Aby przypisać co najmniej jedną grupę aplikacji bezpośrednio, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-417">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego**.</span><span class="sxs-lookup"><span data-stu-id="a8784-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="a8784-418">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-419">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-420">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8784-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8784-421">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a8784-422">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a8784-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8784-423">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="a8784-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="a8784-424">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8784-425">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a8784-426">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="a8784-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a8784-427">Wpisz w **grupy Pełna nazwa** planuje się przypisanie do grupy **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a8784-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a8784-428">Umieść kursor nad **grupy** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="a8784-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="a8784-429">Kliknij pole wyboru obok profilu zdjęcie lub logo, aby dodać użytkownika do grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="a8784-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="a8784-430">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jedną grupę**, typu w innym **grupy Pełna nazwa** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać tę grupę do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="a8784-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="a8784-431">Po wybraniu grup kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="a8784-432">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="a8784-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="a8784-433">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="a8784-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="a8784-434">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a8784-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="a8784-435">Sprawdź, czy użytkownik jest częścią grupy przypisane do licencji</span><span class="sxs-lookup"><span data-stu-id="a8784-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="a8784-436">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a8784-437">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-438">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-439">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="a8784-440">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a8784-440">click **All users**.</span></span>

6.  <span data-ttu-id="a8784-441">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="a8784-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="a8784-442">Kliknij przycisk **grup**.</span><span class="sxs-lookup"><span data-stu-id="a8784-442">click **Groups**.</span></span>

8.  <span data-ttu-id="a8784-443">Kliknij wiersz określonej grupy.</span><span class="sxs-lookup"><span data-stu-id="a8784-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="a8784-444">Kliknij przycisk **licencji** aby zobaczyć, które licencje grupy został przypisany do niej.</span><span class="sxs-lookup"><span data-stu-id="a8784-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="a8784-445">Jeśli ta grupa jest przypisana do licencji pakietu Office, to może włączyć określonych aplikacji pierwszej strony pakietu Office na panelu dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="a8784-446">Jak przypisać licencję do grupy</span><span class="sxs-lookup"><span data-stu-id="a8784-446">How to assign a license to a group</span></span>

<span data-ttu-id="a8784-447">Aby przypisać licencję do grupy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8784-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="a8784-448">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="a8784-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a8784-449">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8784-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8784-450">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8784-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8784-451">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="a8784-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="a8784-452">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="a8784-452">click **All groups**.</span></span>

6.  <span data-ttu-id="a8784-453">**Wyszukiwanie** dla grupy Użytkownicy zainteresowani i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="a8784-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="a8784-454">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje grupy został przypisany.</span><span class="sxs-lookup"><span data-stu-id="a8784-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="a8784-455">Kliknij przycisk **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a8784-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="a8784-456">Wybierz **jeden lub więcej produktów** z listy dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="a8784-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="a8784-457">**Opcjonalne** kliknij **opcje przydziału** element, aby przypisać częściami produktów.</span><span class="sxs-lookup"><span data-stu-id="a8784-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="a8784-458">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="a8784-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="a8784-459">Kliknij przycisk **przypisać** przycisk, aby przypisać licencje do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="a8784-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="a8784-460">Może to zająć dużo czasu, w zależności od rozmiaru i złożoności grupy.</span><span class="sxs-lookup"><span data-stu-id="a8784-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="a8784-461">Aby szybciej to zrobić, należy wziąć pod uwagę tymczasowo bezpośrednio przypisywania licencji do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8784-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="a8784-462">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8784-462">Next steps</span></span>
[<span data-ttu-id="a8784-463">Dodawanie nowych użytkowników do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8784-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

