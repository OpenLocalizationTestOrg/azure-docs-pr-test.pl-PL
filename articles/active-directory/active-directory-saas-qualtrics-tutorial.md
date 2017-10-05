---
title: 'Samouczek: Integracji Azure Active Directory z Qualtrics | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać Qualtrics usłudze Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="61b8d-103">Samouczek: Integracji Azure Active Directory z Qualtrics</span><span class="sxs-lookup"><span data-stu-id="61b8d-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="61b8d-104">Celem tego samouczka jest pokazanie integracji Azure i Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="61b8d-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="61b8d-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="61b8d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="61b8d-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="61b8d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="61b8d-107">Qualtrics rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="61b8d-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="61b8d-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do Qualtrics będzie można funkcji logowania jednokrotnego do aplikacji w witrynie firmy Qualtrics (usługa zainicjował dostawcy logowania) lub przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="61b8d-109">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="61b8d-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="61b8d-110">Włączanie integracji aplikacji dla Qualtrics</span><span class="sxs-lookup"><span data-stu-id="61b8d-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="61b8d-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="61b8d-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="61b8d-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="61b8d-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="61b8d-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="61b8d-113">Assigning users</span></span>

<span data-ttu-id="61b8d-114">![Scenariusz](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="61b8d-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="61b8d-115">Włączanie integracji aplikacji dla Qualtrics</span><span class="sxs-lookup"><span data-stu-id="61b8d-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="61b8d-116">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="61b8d-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="61b8d-117">**Aby włączyć integrację aplikacji dla Qualtrics, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="61b8d-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="61b8d-118">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="61b8d-119">![Usługi Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="61b8d-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="61b8d-120">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="61b8d-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="61b8d-121">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="61b8d-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="61b8d-122">![Aplikacje](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="61b8d-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="61b8d-123">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="61b8d-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="61b8d-124">![Dodaj aplikację](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="61b8d-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="61b8d-125">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="61b8d-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="61b8d-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="61b8d-127">W **pole wyszukiwania**, typ **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="61b8d-128">![Galerii aplikacji](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="61b8d-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="61b8d-129">W okienku wyników wybierz **Qualtrics**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="61b8d-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="61b8d-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="61b8d-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="61b8d-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="61b8d-131">Configure single sign-on</span></span>

<span data-ttu-id="61b8d-132">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na Qualtrics do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="61b8d-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="61b8d-133">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="61b8d-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="61b8d-134">W klasycznym portalu Azure na **Qualtrics** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61b8d-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="61b8d-135">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="61b8d-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="61b8d-136">Na **jak chcesz użytkownikom zalogować się na Qualtrics** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="61b8d-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="61b8d-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="61b8d-138">Na **Konfigurowanie adresu URL aplikacji** strony w **Qualtrics na adres URL logowania** pole tekstowe, wpisz adres URL (np.: "*https://ssotest2ut1.qualtrics.com*"), a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="61b8d-139">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="61b8d-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="61b8d-140">Na **skonfigurować logowanie jednokrotne w Qualtrics** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="61b8d-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="61b8d-141">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="61b8d-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="61b8d-142">Wyślij plik metadanych do Qualtrics zespołu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="61b8d-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="61b8d-143">Konfiguracji logowania jednokrotnego musi zostać wykonana przez zespół pomocy technicznej Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="61b8d-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="61b8d-144">Otrzymasz powiadomienie, natychmiast po zakończeniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61b8d-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="61b8d-145">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61b8d-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="61b8d-146">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="61b8d-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="61b8d-147">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="61b8d-147">Configure user provisioning</span></span>

<span data-ttu-id="61b8d-148">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej Qualtrics użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61b8d-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="61b8d-149">Gdy przypisany użytkownik próbuje zalogować się przy użyciu panelu dostępu Qualtrics, Qualtrics sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="61b8d-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="61b8d-150">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="61b8d-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="61b8d-151">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="61b8d-151">Assign users</span></span>
<span data-ttu-id="61b8d-152">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="61b8d-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="61b8d-153">**Do przypisywania użytkowników do Qualtrics, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="61b8d-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="61b8d-154">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="61b8d-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="61b8d-155">Na **Qualtrics** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="61b8d-156">![Przypisywanie użytkowników](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="61b8d-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="61b8d-157">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="61b8d-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="61b8d-158">![Tak](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="61b8d-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="61b8d-159">Jeśli chcesz przetestować ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="61b8d-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="61b8d-160">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

