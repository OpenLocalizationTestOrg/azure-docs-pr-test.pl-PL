---
title: 'Samouczek: Integracji Azure Active Directory z TargetProcess | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d15931a5d430252bbd9ae342e1f8fde1a539355b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="9a946-103">Samouczek: Integracji Azure Active Directory z TargetProcess</span><span class="sxs-lookup"><span data-stu-id="9a946-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="9a946-104">Z tego samouczka dowiesz się integrowanie TargetProcess z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a946-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a946-105">Integracja z usługą Azure AD TargetProcess zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9a946-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a946-106">Można kontrolować w usłudze Azure AD, który ma dostęp do TargetProcess</span><span class="sxs-lookup"><span data-stu-id="9a946-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="9a946-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do TargetProcess (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a946-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a946-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9a946-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9a946-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a946-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a946-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9a946-110">Prerequisites</span></span>

<span data-ttu-id="9a946-111">Aby skonfigurować integrację usługi Azure AD z TargetProcess, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9a946-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="9a946-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a946-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a946-113">TargetProcess logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9a946-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a946-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9a946-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a946-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9a946-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a946-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9a946-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a946-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a946-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a946-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9a946-118">Scenario description</span></span>
<span data-ttu-id="9a946-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9a946-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a946-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9a946-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a946-121">Dodaj TargetProcess z galerii</span><span class="sxs-lookup"><span data-stu-id="9a946-121">Add TargetProcess from the gallery</span></span>
2. <span data-ttu-id="9a946-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9a946-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="9a946-123">Dodaj TargetProcess z galerii</span><span class="sxs-lookup"><span data-stu-id="9a946-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="9a946-124">Aby skonfigurować integrację usługi Azure AD TargetProcess, należy dodać TargetProcess z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9a946-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a946-125">**Aby dodać TargetProcess z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a946-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a946-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9a946-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9a946-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9a946-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a946-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9a946-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9a946-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a946-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9a946-133">W polu wyszukiwania wpisz **TargetProcess**, wybierz pozycję **TargetProcess** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9a946-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![Dodaj TargetProcess z galerii](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a946-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9a946-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9a946-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TargetProcess w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9a946-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a946-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w TargetProcess jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a946-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="9a946-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w TargetProcess musi się.</span><span class="sxs-lookup"><span data-stu-id="9a946-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="9a946-139">W TargetProcess, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="9a946-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9a946-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TargetProcess, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9a946-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a946-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9a946-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a946-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9a946-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a946-143">**[Tworzenie użytkownika testowego TargetProcess](#create-a-targetprocess-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta TargetProcess połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9a946-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a946-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9a946-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a946-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9a946-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a946-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9a946-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a946-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="9a946-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="9a946-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z TargetProcess, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a946-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="9a946-149">W portalu Azure na **TargetProcess** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9a946-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9a946-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9a946-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="9a946-153">Na **TargetProcess domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9a946-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Sekcja TargetProcess domeny i adresy URL](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="9a946-155">a.</span><span class="sxs-lookup"><span data-stu-id="9a946-155">a.</span></span> <span data-ttu-id="9a946-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="9a946-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="9a946-157">b.</span><span class="sxs-lookup"><span data-stu-id="9a946-157">b.</span></span> <span data-ttu-id="9a946-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="9a946-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a946-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9a946-159">These values are not real.</span></span> <span data-ttu-id="9a946-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9a946-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9a946-161">Skontaktuj się z [zespołem pomocy technicznej klienta TargetProcess](mailto:support@targetprocess.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="9a946-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
4. <span data-ttu-id="9a946-162">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9a946-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="9a946-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9a946-164">Click **Save** button.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9a946-166">Na **konfiguracji TargetProcess** , kliknij przycisk **skonfigurować TargetProcess** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9a946-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9a946-167">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9a946-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sekcja konfiguracji TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="9a946-169">Logowanie do aplikacji TargetProcess jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9a946-169">Sign-on to your TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="9a946-170">W menu u góry kliknij **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="9a946-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Konfiguracja](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="9a946-172">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="9a946-172">Click **Settings**.</span></span>
   
    ![Ustawienia](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="9a946-174">Kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9a946-174">Click **Single Sign-on**.</span></span>
   
    ![Kliknij przycisk rejestracji jednokrotnej](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="9a946-176">W oknie Ustawienia logowania jednokrotnego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9a946-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="9a946-178">a.</span><span class="sxs-lookup"><span data-stu-id="9a946-178">a.</span></span> <span data-ttu-id="9a946-179">Kliknij przycisk **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="9a946-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="9a946-180">b.</span><span class="sxs-lookup"><span data-stu-id="9a946-180">b.</span></span> <span data-ttu-id="9a946-181">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9a946-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9a946-182">c.</span><span class="sxs-lookup"><span data-stu-id="9a946-182">c.</span></span> <span data-ttu-id="9a946-183">Otwórz w Notatniku pobranego certyfikatu, skopiuj zawartość, a następnie wklej go do **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9a946-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="9a946-184">d.</span><span class="sxs-lookup"><span data-stu-id="9a946-184">d.</span></span> <span data-ttu-id="9a946-185">Kliknij przycisk **włączyć udostępniania JIT**.</span><span class="sxs-lookup"><span data-stu-id="9a946-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="9a946-186">e.</span><span class="sxs-lookup"><span data-stu-id="9a946-186">e.</span></span> <span data-ttu-id="9a946-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9a946-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9a946-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9a946-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a946-189">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9a946-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a946-190">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a946-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a946-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a946-191">Create an Azure AD test user</span></span>
<span data-ttu-id="9a946-192">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9a946-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9a946-194">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a946-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a946-195">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9a946-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a946-197">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9a946-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Aby wyświetlić listę użytkowników](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a946-199">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a946-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Dodawanie przycisku](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a946-201">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9a946-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Sekcja użytkownika](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a946-203">a.</span><span class="sxs-lookup"><span data-stu-id="9a946-203">a.</span></span> <span data-ttu-id="9a946-204">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a946-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a946-205">b.</span><span class="sxs-lookup"><span data-stu-id="9a946-205">b.</span></span> <span data-ttu-id="9a946-206">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a946-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a946-207">c.</span><span class="sxs-lookup"><span data-stu-id="9a946-207">c.</span></span> <span data-ttu-id="9a946-208">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9a946-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a946-209">d.</span><span class="sxs-lookup"><span data-stu-id="9a946-209">d.</span></span> <span data-ttu-id="9a946-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9a946-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="9a946-211">Tworzenie użytkownika testowego TargetProcess</span><span class="sxs-lookup"><span data-stu-id="9a946-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="9a946-212">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="9a946-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="9a946-213">TargetProcess obsługę w czasie.</span><span class="sxs-lookup"><span data-stu-id="9a946-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="9a946-214">Została już włączona w [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9a946-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="9a946-215">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9a946-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9a946-216">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a946-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="9a946-217">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="9a946-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9a946-219">**Aby przypisać Simona Britta TargetProcess, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a946-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="9a946-220">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9a946-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9a946-222">Na liście aplikacji zaznacz **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="9a946-222">In the applications list, select **TargetProcess**.</span></span>

    ![TargetProcess listy aplikacji](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="9a946-224">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9a946-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9a946-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9a946-226">Click **Add** button.</span></span> <span data-ttu-id="9a946-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a946-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9a946-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9a946-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a946-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a946-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a946-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a946-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a946-232">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9a946-232">Test single sign-on</span></span>

<span data-ttu-id="9a946-233">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9a946-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9a946-234">Po kliknięciu kafelka TargetProcess w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="9a946-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="9a946-235">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a946-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a946-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9a946-236">Additional resources</span></span>

* [<span data-ttu-id="9a946-237">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a946-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a946-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a946-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

