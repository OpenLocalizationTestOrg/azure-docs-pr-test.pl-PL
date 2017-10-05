---
title: 'Samouczek: Integracji Azure Active Directory z Benefitsolver | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać Benefitsolver usłudze Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="e54d3-103">Samouczek: Integracji Azure Active Directory z Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="e54d3-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="e54d3-104">Celem tego samouczka jest pokazanie integracji Azure i Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="e54d3-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="e54d3-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e54d3-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="e54d3-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e54d3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e54d3-107">Benefitsolver rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e54d3-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="e54d3-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do Benefitsolver będzie można funkcji logowania jednokrotnego do aplikacji przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e54d3-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="e54d3-109">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="e54d3-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="e54d3-110">Włączanie integracji aplikacji dla Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="e54d3-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="e54d3-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="e54d3-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="e54d3-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="e54d3-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="e54d3-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="e54d3-113">Assigning users</span></span>

<span data-ttu-id="e54d3-114">![Scenariusz](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="e54d3-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="e54d3-115">Włączanie integracji aplikacji dla Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="e54d3-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="e54d3-116">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="e54d3-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="e54d3-117">Aby włączyć integrację aplikacji dla Benefitsolver, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e54d3-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="e54d3-118">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="e54d3-119">![Usługi Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e54d3-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e54d3-120">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="e54d3-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e54d3-121">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="e54d3-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="e54d3-122">![Aplikacje](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="e54d3-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e54d3-123">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="e54d3-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="e54d3-124">![Dodaj aplikację](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="e54d3-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e54d3-125">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="e54d3-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="e54d3-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e54d3-127">W **pole wyszukiwania**, typ **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="e54d3-128">![Galerii aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="e54d3-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="e54d3-129">W okienku wyników wybierz **Benefitsolver**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e54d3-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="e54d3-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="e54d3-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e54d3-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e54d3-131">Configure single sign-on</span></span>

<span data-ttu-id="e54d3-132">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na Benefitsolver do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="e54d3-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="e54d3-133">Aplikacja Benefitsolver oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do Twojej **atrybuty tokenu saml** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e54d3-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="e54d3-134">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="e54d3-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="e54d3-135">![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="e54d3-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="e54d3-136">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e54d3-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="e54d3-137">W klasycznym portalu Azure na **Benefitsolver** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e54d3-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="e54d3-138">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e54d3-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="e54d3-139">Na **jak chcesz użytkownikom zalogować się na Benefitsolver** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="e54d3-140">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e54d3-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="e54d3-141">Na **Konfigurowanie ustawień aplikacji** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e54d3-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="e54d3-142">![Konfiguruj ustawienia aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Konfiguruj ustawienia aplikacji")</span><span class="sxs-lookup"><span data-stu-id="e54d3-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="e54d3-143">W **na adres URL logowania** pole tekstowe, typ **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="e54d3-144">W **adres URL odpowiedzi** pole tekstowe, typ **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="e54d3-145">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-145">Click **Next**.</span></span>
4. <span data-ttu-id="e54d3-146">Na **skonfigurować logowanie jednokrotne w Benefitsolver** , aby pobrać metadane, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e54d3-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="e54d3-147">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e54d3-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="e54d3-148">Wyślij plik metadanych pobranych Benefitsolver zespołowi pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="e54d3-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e54d3-149">Z zespołem pomocy technicznej Benefitsolver ma robić rzeczywista konfiguracja logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="e54d3-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="e54d3-150">Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e54d3-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="e54d3-151">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e54d3-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="e54d3-152">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e54d3-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="e54d3-153">W menu u góry kliknij **atrybuty** otworzyć **atrybuty tokenu SAML** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e54d3-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="e54d3-154">![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="e54d3-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="e54d3-155">Aby dodać mapowania wymaganego atrybutu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e54d3-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="e54d3-156">![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="e54d3-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="e54d3-157">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="e54d3-157">Attribute Name</span></span> | <span data-ttu-id="e54d3-158">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="e54d3-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="e54d3-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="e54d3-159">ClientID</span></span> |<span data-ttu-id="e54d3-160">Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="e54d3-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="e54d3-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="e54d3-161">ClientKey</span></span> |<span data-ttu-id="e54d3-162">Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="e54d3-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="e54d3-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="e54d3-163">LogoutURL</span></span> |<span data-ttu-id="e54d3-164">Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="e54d3-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="e54d3-165">Identyfikator pracownika</span><span class="sxs-lookup"><span data-stu-id="e54d3-165">EmployeeID</span></span> |<span data-ttu-id="e54d3-166">Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="e54d3-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="e54d3-167">Dla każdego wiersza danych w tabeli powyżej, kliknij przycisk **Dodaj atrybut użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="e54d3-168">W **nazwa atrybutu** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="e54d3-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="e54d3-169">W **wartość atrybutu** pole tekstowe, wybierz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="e54d3-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="e54d3-170">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="e54d3-170">Click **Complete**.</span></span>
9. <span data-ttu-id="e54d3-171">Kliknij przycisk **Zastosuj zmiany**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="e54d3-172">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="e54d3-172">Configure user provisioning</span></span>
<span data-ttu-id="e54d3-173">Aby włączyć użytkowników usługi Azure AD zalogować się do Benefitsolver, musi być przygotowana do Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="e54d3-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="e54d3-174">W przypadku Benefitsolver pracownika danych jest w aplikacji wypełniać za pomocą pliku spisu z systemu HRIS (zazwyczaj co noc).</span><span class="sxs-lookup"><span data-stu-id="e54d3-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="e54d3-175">Możesz użyć innych Benefitsolver użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Benefitsolver do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="e54d3-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="e54d3-176">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="e54d3-176">Assigning users</span></span>
<span data-ttu-id="e54d3-177">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="e54d3-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="e54d3-178">Do przypisywania użytkowników do Benefitsolver, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e54d3-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="e54d3-179">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="e54d3-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e54d3-180">Na ** Benefitsolver ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e54d3-181">![Przypisywanie użytkowników](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="e54d3-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="e54d3-182">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="e54d3-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="e54d3-183">![Tak](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="e54d3-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e54d3-184">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="e54d3-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="e54d3-185">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e54d3-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

