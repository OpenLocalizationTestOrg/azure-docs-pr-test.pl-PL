---
title: 'Samouczek: Integracji Azure Active Directory z SumoLogic | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="c0cde-103">Samouczek: Integracji Azure Active Directory z SumoLogic</span><span class="sxs-lookup"><span data-stu-id="c0cde-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="c0cde-104">Z tego samouczka dowiesz się integrowanie SumoLogic z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0cde-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0cde-105">Integracja z usługą Azure AD SumoLogic zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c0cde-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0cde-106">Można kontrolować w usłudze Azure AD, który ma dostęp do SumoLogic</span><span class="sxs-lookup"><span data-stu-id="c0cde-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="c0cde-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do SumoLogic (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0cde-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0cde-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c0cde-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0cde-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0cde-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0cde-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c0cde-110">Prerequisites</span></span>

<span data-ttu-id="c0cde-111">Aby skonfigurować integrację usługi Azure AD z SumoLogic, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c0cde-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="c0cde-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0cde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0cde-113">SumoLogic logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c0cde-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0cde-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0cde-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c0cde-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0cde-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c0cde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0cde-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0cde-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0cde-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c0cde-118">Scenario description</span></span>
<span data-ttu-id="c0cde-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c0cde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0cde-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c0cde-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0cde-121">Dodawanie SumoLogic z galerii</span><span class="sxs-lookup"><span data-stu-id="c0cde-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="c0cde-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0cde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="c0cde-123">Dodawanie SumoLogic z galerii</span><span class="sxs-lookup"><span data-stu-id="c0cde-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="c0cde-124">Aby skonfigurować integrację usługi Azure AD SumoLogic, należy dodać SumoLogic z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0cde-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0cde-125">**Aby dodać SumoLogic z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0cde-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0cde-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0cde-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c0cde-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0cde-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c0cde-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c0cde-133">W polu wyszukiwania wpisz **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-133">In the search box, type **SumoLogic**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="c0cde-135">W panelu wyników wybierz **SumoLogic**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c0cde-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0cde-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0cde-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0cde-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SumoLogic w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0cde-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w SumoLogic jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0cde-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="c0cde-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w SumoLogic musi się.</span><span class="sxs-lookup"><span data-stu-id="c0cde-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="c0cde-141">W SumoLogic, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c0cde-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0cde-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SumoLogic, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c0cde-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0cde-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c0cde-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0cde-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c0cde-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0cde-145">**[Tworzenie użytkownika testowego SumoLogic](#creating-a-sumologic-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SumoLogic połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c0cde-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0cde-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c0cde-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0cde-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c0cde-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0cde-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0cde-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0cde-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c0cde-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="c0cde-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SumoLogic, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0cde-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="c0cde-151">W portalu Azure na **SumoLogic** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c0cde-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c0cde-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="c0cde-155">Na **SumoLogic domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0cde-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="c0cde-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0cde-157">a.</span></span> <span data-ttu-id="c0cde-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="c0cde-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="c0cde-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0cde-159">b.</span></span> <span data-ttu-id="c0cde-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="c0cde-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="c0cde-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c0cde-161">These values are not real.</span></span> <span data-ttu-id="c0cde-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c0cde-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c0cde-163">Skontaktuj się z [zespołem pomocy technicznej klienta SumoLogic](https://www.sumologic.com/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c0cde-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="c0cde-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c0cde-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="c0cde-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0cde-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0cde-168">Na **konfiguracji SumoLogic** , kliknij przycisk **skonfigurować SumoLogic** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c0cde-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c0cde-169">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c0cde-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="c0cde-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c0cde-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="c0cde-172">Przejdź do **zarządzanie \> zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="c0cde-173">![Zarządzanie](./media/active-directory-saas-sumologic-tutorial/ic778556.png "zarządzania")</span><span class="sxs-lookup"><span data-stu-id="c0cde-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="c0cde-174">Kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="c0cde-175">![Ustawienia zabezpieczeń globalnych](./media/active-directory-saas-sumologic-tutorial/ic778557.png "ustawienia zabezpieczeń globalnych")</span><span class="sxs-lookup"><span data-stu-id="c0cde-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="c0cde-176">Z **wybierz konfigurację lub Utwórz nową** wybierz **usługi Azure AD**, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="c0cde-177">![Skonfigurować SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "skonfigurować SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="c0cde-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="c0cde-178">Na **skonfigurować SAML 2.0** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0cde-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c0cde-179">![Skonfigurować SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "skonfigurować SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="c0cde-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="c0cde-180">a.</span><span class="sxs-lookup"><span data-stu-id="c0cde-180">a.</span></span> <span data-ttu-id="c0cde-181">W **Nazwa konfiguracji** pole tekstowe, typ **usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="c0cde-182">b.</span><span class="sxs-lookup"><span data-stu-id="c0cde-182">b.</span></span> <span data-ttu-id="c0cde-183">Wybierz **tryb debugowania**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="c0cde-184">c.</span><span class="sxs-lookup"><span data-stu-id="c0cde-184">c.</span></span> <span data-ttu-id="c0cde-185">W **wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c0cde-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c0cde-186">d.</span><span class="sxs-lookup"><span data-stu-id="c0cde-186">d.</span></span> <span data-ttu-id="c0cde-187">W **URL żądania uwierzytelniania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c0cde-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c0cde-188">e.</span><span class="sxs-lookup"><span data-stu-id="c0cde-188">e.</span></span> <span data-ttu-id="c0cde-189">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej cały certyfikat do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="c0cde-190">f.</span><span class="sxs-lookup"><span data-stu-id="c0cde-190">f.</span></span> <span data-ttu-id="c0cde-191">Jako **atrybut poczty E-mail**, wybierz pozycję **podmiotu SAML użyj**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="c0cde-192">g.</span><span class="sxs-lookup"><span data-stu-id="c0cde-192">g.</span></span> <span data-ttu-id="c0cde-193">Wybierz **SP zainicjował konfiguracji logowania**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="c0cde-194">h.</span><span class="sxs-lookup"><span data-stu-id="c0cde-194">h.</span></span> <span data-ttu-id="c0cde-195">W **ścieżkę logowania** pole tekstowe, typ **Azure** i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c0cde-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c0cde-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0cde-197">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c0cde-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0cde-198">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0cde-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0cde-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0cde-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0cde-200">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c0cde-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c0cde-202">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0cde-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0cde-203">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0cde-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0cde-205">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0cde-207">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0cde-209">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0cde-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0cde-211">a.</span><span class="sxs-lookup"><span data-stu-id="c0cde-211">a.</span></span> <span data-ttu-id="c0cde-212">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0cde-213">b.</span><span class="sxs-lookup"><span data-stu-id="c0cde-213">b.</span></span> <span data-ttu-id="c0cde-214">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0cde-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0cde-215">c.</span><span class="sxs-lookup"><span data-stu-id="c0cde-215">c.</span></span> <span data-ttu-id="c0cde-216">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0cde-217">d.</span><span class="sxs-lookup"><span data-stu-id="c0cde-217">d.</span></span> <span data-ttu-id="c0cde-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="c0cde-219">Tworzenie użytkownika testowego SumoLogic</span><span class="sxs-lookup"><span data-stu-id="c0cde-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="c0cde-220">Aby umożliwić użytkownikom zalogować się do SumoLogic usługi Azure AD, muszą one być przygotowana do SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c0cde-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="c0cde-221">W przypadku SumoLogic Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c0cde-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="c0cde-222">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0cde-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c0cde-223">Zaloguj się do Twojego **SumoLogic** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c0cde-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="c0cde-224">Przejdź do **zarządzanie \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="c0cde-225">![Użytkownicy](./media/active-directory-saas-sumologic-tutorial/ic778561.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c0cde-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="c0cde-226">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-226">Click **Add**.</span></span>
   
    <span data-ttu-id="c0cde-227">![Użytkownicy](./media/active-directory-saas-sumologic-tutorial/ic778562.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c0cde-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="c0cde-228">Na **nowego użytkownika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0cde-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c0cde-229">![Nowy użytkownik](./media/active-directory-saas-sumologic-tutorial/ic778563.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c0cde-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="c0cde-230">a.</span><span class="sxs-lookup"><span data-stu-id="c0cde-230">a.</span></span> <span data-ttu-id="c0cde-231">Wpisz odpowiednie informacje chcesz udostępnić do konta usługi Azure AD **imię**, **nazwisko**, i **E-mail** pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="c0cde-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="c0cde-232">b.</span><span class="sxs-lookup"><span data-stu-id="c0cde-232">b.</span></span> <span data-ttu-id="c0cde-233">Wybierz rolę.</span><span class="sxs-lookup"><span data-stu-id="c0cde-233">Select a role.</span></span>
  
    <span data-ttu-id="c0cde-234">c.</span><span class="sxs-lookup"><span data-stu-id="c0cde-234">c.</span></span> <span data-ttu-id="c0cde-235">Jako **stan**, wybierz pozycję **Active**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="c0cde-236">d.</span><span class="sxs-lookup"><span data-stu-id="c0cde-236">d.</span></span> <span data-ttu-id="c0cde-237">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c0cde-238">Możesz użyć innych SumoLogic użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SumoLogic do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c0cde-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0cde-239">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0cde-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0cde-240">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c0cde-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c0cde-242">**Aby przypisać Simona Britta SumoLogic, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0cde-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="c0cde-243">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c0cde-245">Na liście aplikacji zaznacz **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-245">In the applications list, select **SumoLogic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="c0cde-247">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c0cde-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c0cde-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0cde-249">Click **Add** button.</span></span> <span data-ttu-id="c0cde-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c0cde-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c0cde-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0cde-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0cde-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0cde-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0cde-255">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0cde-255">Testing single sign-on</span></span>

<span data-ttu-id="c0cde-256">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0cde-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0cde-257">Po kliknięciu kafelka SumoLogic w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c0cde-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0cde-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c0cde-258">Additional resources</span></span>

* [<span data-ttu-id="c0cde-259">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0cde-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0cde-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0cde-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

