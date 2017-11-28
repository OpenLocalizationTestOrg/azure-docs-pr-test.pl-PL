---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Rally | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między oprogramowaniem Rally i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="0a979-103">Samouczek: Azure Active Directory integracji z oprogramowaniem Rally</span><span class="sxs-lookup"><span data-stu-id="0a979-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="0a979-104">Z tego samouczka dowiesz się integrowanie Rally oprogramowania z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a979-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a979-105">Integrowanie Rally oprogramowania z usługi Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0a979-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a979-106">Można kontrolować w usłudze Azure AD, który ma dostęp do oprogramowania Rally.</span><span class="sxs-lookup"><span data-stu-id="0a979-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="0a979-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Rally oprogramowania (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a979-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0a979-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a979-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0a979-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a979-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a979-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0a979-110">Prerequisites</span></span>

<span data-ttu-id="0a979-111">Aby skonfigurować integrację usługi Azure AD z oprogramowaniem Rally, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0a979-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="0a979-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a979-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a979-113">Oprogramowanie Rally logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0a979-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a979-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0a979-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a979-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0a979-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a979-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0a979-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a979-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a979-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a979-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0a979-118">Scenario description</span></span>
<span data-ttu-id="0a979-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0a979-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a979-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0a979-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a979-121">Dodawanie oprogramowania Rally z galerii</span><span class="sxs-lookup"><span data-stu-id="0a979-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="0a979-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0a979-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="0a979-123">Dodawanie oprogramowania Rally z galerii</span><span class="sxs-lookup"><span data-stu-id="0a979-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="0a979-124">Aby skonfigurować integrację usługi Azure AD Rally oprogramowania, należy dodać Rally oprogramowania z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0a979-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a979-125">**Aby dodać Rally oprogramowanie z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a979-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a979-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a979-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="0a979-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0a979-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a979-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a979-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="0a979-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a979-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="0a979-133">W polu wyszukiwania wpisz **Rally oprogramowania**, wybierz pozycję **Rally oprogramowania** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="0a979-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally oprogramowania z listy wyników](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0a979-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a979-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0a979-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0a979-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a979-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem Rally oprogramowanie jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a979-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="0a979-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w oprogramowaniu Rally musi określone.</span><span class="sxs-lookup"><span data-stu-id="0a979-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="0a979-139">Rally oprogramowania, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="0a979-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0a979-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="0a979-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a979-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a979-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a979-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a979-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a979-143">**[Tworzenie użytkownika testowego Rally oprogramowania](#create-a-rally-software-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Rally oprogramowania połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a979-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a979-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a979-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a979-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="0a979-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0a979-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a979-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0a979-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji oprogramowania Rally.</span><span class="sxs-lookup"><span data-stu-id="0a979-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="0a979-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Rally oprogramowania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a979-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="0a979-149">W portalu Azure na **Rally oprogramowania** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0a979-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="0a979-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="0a979-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="0a979-153">Na **Rally domeny oprogramowania i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a979-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Rally domeny oprogramowania i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="0a979-155">a.</span><span class="sxs-lookup"><span data-stu-id="0a979-155">a.</span></span> <span data-ttu-id="0a979-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="0a979-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="0a979-157">b.</span><span class="sxs-lookup"><span data-stu-id="0a979-157">b.</span></span> <span data-ttu-id="0a979-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="0a979-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a979-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0a979-159">These values are not real.</span></span> <span data-ttu-id="0a979-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="0a979-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0a979-161">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania Rally](https://help.rallydev.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="0a979-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="0a979-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0a979-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="0a979-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a979-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a979-166">Na **Rally konfiguracji oprogramowania** kliknij **Konfigurowanie oprogramowania Rally** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0a979-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a979-167">Kopiuj **Sign-Out adresu URL i identyfikator jednostki SAML** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0a979-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Rally konfiguracji oprogramowania](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="0a979-169">Zaloguj się do Twojego **Rally oprogramowania** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="0a979-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="0a979-170">Na pasku narzędzi u góry kliknij **Instalator**, a następnie wybierz **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="0a979-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="0a979-171">![Subskrypcja](./media/active-directory-saas-rally-software-tutorial/ic769531.png "subskrypcji")</span><span class="sxs-lookup"><span data-stu-id="0a979-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="0a979-172">Kliknij przycisk **akcji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a979-172">Click the **Action** button.</span></span> <span data-ttu-id="0a979-173">Wybierz **edytować subskrypcji** w górnym rogu paska narzędzi.</span><span class="sxs-lookup"><span data-stu-id="0a979-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="0a979-174">Na **subskrypcji** strony okna dialogowego, wykonaj następujące czynności, a następnie kliknij **Zapisz i Zamknij**:</span><span class="sxs-lookup"><span data-stu-id="0a979-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="0a979-175">![Uwierzytelnianie](./media/active-directory-saas-rally-software-tutorial/ic769542.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="0a979-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="0a979-176">a.</span><span class="sxs-lookup"><span data-stu-id="0a979-176">a.</span></span> <span data-ttu-id="0a979-177">Wybierz **uwierzytelniania Rally lub logowania jednokrotnego** z listy rozwijanej uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0a979-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="0a979-178">b.</span><span class="sxs-lookup"><span data-stu-id="0a979-178">b.</span></span> <span data-ttu-id="0a979-179">W **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a979-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0a979-180">c.</span><span class="sxs-lookup"><span data-stu-id="0a979-180">c.</span></span> <span data-ttu-id="0a979-181">W **wylogowania logowania jednokrotnego** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a979-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="0a979-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="0a979-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a979-183">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="0a979-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a979-184">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a979-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0a979-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a979-185">Create an Azure AD test user</span></span>

<span data-ttu-id="0a979-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a979-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="0a979-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a979-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a979-189">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a979-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0a979-191">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0a979-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0a979-193">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0a979-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0a979-195">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a979-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0a979-197">a.</span><span class="sxs-lookup"><span data-stu-id="0a979-197">a.</span></span> <span data-ttu-id="0a979-198">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a979-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a979-199">b.</span><span class="sxs-lookup"><span data-stu-id="0a979-199">b.</span></span> <span data-ttu-id="0a979-200">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a979-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0a979-201">c.</span><span class="sxs-lookup"><span data-stu-id="0a979-201">c.</span></span> <span data-ttu-id="0a979-202">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="0a979-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0a979-203">d.</span><span class="sxs-lookup"><span data-stu-id="0a979-203">d.</span></span> <span data-ttu-id="0a979-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0a979-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="0a979-205">Tworzenie użytkownika testowego Rally oprogramowania</span><span class="sxs-lookup"><span data-stu-id="0a979-205">Create a Rally Software test user</span></span>

<span data-ttu-id="0a979-206">Dla użytkowników usługi Azure AD można było się zalogować musi być przygotowana do aplikacji Rally oprogramowania przy użyciu nazwy użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a979-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="0a979-207">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a979-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0a979-208">Zaloguj się do dzierżawy Rally oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="0a979-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="0a979-209">Przejdź do **Instalator \> użytkowników**, a następnie kliknij przycisk **+ Dodaj nowy**.</span><span class="sxs-lookup"><span data-stu-id="0a979-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="0a979-210">![Użytkownicy](./media/active-directory-saas-rally-software-tutorial/ic781039.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="0a979-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="0a979-211">Wpisz nazwę w polu tekstowym nowego użytkownika, a następnie kliknij przycisk **Dodaj szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="0a979-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="0a979-212">W **Tworzenie użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a979-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="0a979-213">![Utwórz użytkownika](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="0a979-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="0a979-214">a.</span><span class="sxs-lookup"><span data-stu-id="0a979-214">a.</span></span> <span data-ttu-id="0a979-215">W **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika, takich jak **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="0a979-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="0a979-216">b.</span><span class="sxs-lookup"><span data-stu-id="0a979-216">b.</span></span> <span data-ttu-id="0a979-217">W **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="0a979-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="0a979-218">c.</span><span class="sxs-lookup"><span data-stu-id="0a979-218">c.</span></span> <span data-ttu-id="0a979-219">W **imię** tekst Wprowadź imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0a979-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="0a979-220">d.</span><span class="sxs-lookup"><span data-stu-id="0a979-220">d.</span></span> <span data-ttu-id="0a979-221">W **nazwisko** tekst Wprowadź nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="0a979-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="0a979-222">e.</span><span class="sxs-lookup"><span data-stu-id="0a979-222">e.</span></span> <span data-ttu-id="0a979-223">Kliknij przycisk **Zapisz i Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="0a979-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="0a979-224">Inne narzędzia do tworzenia konta użytkownika Rally oprogramowania lub interfejsów API dostarczonych przez Rally oprogramowanie służy do obsługi administracyjnej kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a979-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0a979-225">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a979-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="0a979-226">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do oprogramowania Rally.</span><span class="sxs-lookup"><span data-stu-id="0a979-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="0a979-228">**Aby przypisać Simona Britta Rally oprogramowania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a979-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="0a979-229">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a979-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0a979-231">Na liście aplikacji zaznacz **Rally oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="0a979-231">In the applications list, select **Rally Software**.</span></span>

    ![Łącze Rally oprogramowania na liście aplikacji](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="0a979-233">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0a979-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="0a979-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a979-235">Click **Add** button.</span></span> <span data-ttu-id="0a979-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a979-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="0a979-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="0a979-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a979-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a979-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a979-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a979-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0a979-241">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a979-241">Test single sign-on</span></span>

<span data-ttu-id="0a979-242">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0a979-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a979-243">Po kliknięciu kafelka Rally oprogramowania w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji oprogramowania Rally.</span><span class="sxs-lookup"><span data-stu-id="0a979-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a979-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0a979-244">Additional resources</span></span>

* [<span data-ttu-id="0a979-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a979-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a979-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a979-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

