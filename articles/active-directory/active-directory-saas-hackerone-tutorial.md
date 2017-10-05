---
title: 'Samouczek: Integracji Azure Active Directory z Hackerone | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Hackerone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="ddc94-103">Samouczek: Integracji Azure Active Directory z HackerOne</span><span class="sxs-lookup"><span data-stu-id="ddc94-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="ddc94-104">Z tego samouczka dowiesz się integrowanie HackerOne z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddc94-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddc94-105">Integracja z usługą Azure AD HackerOne zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ddc94-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ddc94-106">Można kontrolować w usłudze Azure AD, który ma dostęp do HackerOne</span><span class="sxs-lookup"><span data-stu-id="ddc94-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="ddc94-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do HackerOne (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc94-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddc94-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ddc94-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ddc94-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddc94-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddc94-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ddc94-110">Prerequisites</span></span>

<span data-ttu-id="ddc94-111">Aby skonfigurować integrację usługi Azure AD z HackerOne, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ddc94-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="ddc94-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddc94-113">HackerOne logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ddc94-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ddc94-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ddc94-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ddc94-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ddc94-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddc94-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ddc94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ddc94-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddc94-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ddc94-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ddc94-118">Scenario description</span></span>
<span data-ttu-id="ddc94-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ddc94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddc94-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ddc94-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddc94-121">Dodawanie HackerOne z galerii</span><span class="sxs-lookup"><span data-stu-id="ddc94-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="ddc94-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ddc94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="ddc94-123">Dodawanie HackerOne z galerii</span><span class="sxs-lookup"><span data-stu-id="ddc94-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="ddc94-124">Aby skonfigurować integrację usługi Azure AD HackerOne, należy dodać HackerOne z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ddc94-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ddc94-125">**Aby dodać HackerOne z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddc94-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ddc94-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ddc94-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ddc94-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ddc94-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ddc94-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddc94-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ddc94-133">W polu wyszukiwania wpisz **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-133">In the search box, type **HackerOne**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="ddc94-135">W panelu wyników wybierz **HackerOne**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ddc94-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddc94-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ddc94-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="ddc94-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HackerOne na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ddc94-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ddc94-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w HackerOne jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddc94-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="ddc94-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w HackerOne musi się.</span><span class="sxs-lookup"><span data-stu-id="ddc94-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="ddc94-141">W HackerOne, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="ddc94-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ddc94-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HackerOne, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ddc94-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ddc94-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ddc94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ddc94-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ddc94-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddc94-145">**[Tworzenie użytkownika testowego HackerOne](#creating-a-hackerone-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta HackerOne połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddc94-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ddc94-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ddc94-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddc94-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ddc94-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddc94-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ddc94-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddc94-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji HackerOne.</span><span class="sxs-lookup"><span data-stu-id="ddc94-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="ddc94-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z HackerOne, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddc94-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="ddc94-151">W portalu Azure na **HackerOne** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ddc94-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ddc94-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="ddc94-155">Na **HackerOne jeden adres URL logowania i identyfikator** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddc94-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="ddc94-157">a.</span><span class="sxs-lookup"><span data-stu-id="ddc94-157">a.</span></span> <span data-ttu-id="ddc94-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="ddc94-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="ddc94-159">b.</span><span class="sxs-lookup"><span data-stu-id="ddc94-159">b.</span></span> <span data-ttu-id="ddc94-160">W **identyfikator** tekstowym, wpisz adres URL jako:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="ddc94-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ddc94-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ddc94-161">This value is not real.</span></span> <span data-ttu-id="ddc94-162">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ddc94-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ddc94-163">Skontaktuj się z [zespołem pomocy technicznej HackerOne](mailto:support@hackerone.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="ddc94-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="ddc94-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ddc94-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="ddc94-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ddc94-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ddc94-168">Na **konfiguracji HackerOne** , kliknij przycisk **skonfigurować HackerOne** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ddc94-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ddc94-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ddc94-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="ddc94-171">Zaloguj się na dzierżawcy HackerOne jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ddc94-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="ddc94-172">W menu u góry kliknij pozycję "**ustawienia**."</span><span class="sxs-lookup"><span data-stu-id="ddc94-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="ddc94-174">Przejdź do "**uwierzytelniania**"i kliknij przycisk"**Dodaj ustawienia SAML**."</span><span class="sxs-lookup"><span data-stu-id="ddc94-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="ddc94-176">Na **ustawienia SAML** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddc94-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="ddc94-178">a.</span><span class="sxs-lookup"><span data-stu-id="ddc94-178">a.</span></span> <span data-ttu-id="ddc94-179">W **domenę poczty E-mail** tekstowym, wpisz zarejestrowanej domeny.</span><span class="sxs-lookup"><span data-stu-id="ddc94-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="ddc94-180">b.</span><span class="sxs-lookup"><span data-stu-id="ddc94-180">b.</span></span> <span data-ttu-id="ddc94-181">W **jeden znak na adres URL** pól tekstowych, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc94-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ddc94-182">c.</span><span class="sxs-lookup"><span data-stu-id="ddc94-182">c.</span></span> <span data-ttu-id="ddc94-183">Otwórz z **plik certyfikatu** w Notatniku pobrany z portalu Azure, należy skopiować zawartość go do Schowka, a następnie wklej go do **X509 certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ddc94-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="ddc94-184">d.</span><span class="sxs-lookup"><span data-stu-id="ddc94-184">d.</span></span> <span data-ttu-id="ddc94-185">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-185">Click **Save**.</span></span>

11. <span data-ttu-id="ddc94-186">W oknie dialogowym Ustawienia uwierzytelniania wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddc94-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="ddc94-188">a.</span><span class="sxs-lookup"><span data-stu-id="ddc94-188">a.</span></span> <span data-ttu-id="ddc94-189">Kliknij przycisk **testu**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-189">Click **Run test**.</span></span>

    <span data-ttu-id="ddc94-190">b.</span><span class="sxs-lookup"><span data-stu-id="ddc94-190">b.</span></span> <span data-ttu-id="ddc94-191">Jeśli wartość **stan** pola equals **ostatni stan testu: utworzone**, skontaktuj się z Twojego [HackerOne zespołem pomocy technicznej](mailto:support@hackerone.com) Aby zażądać przeglądu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ddc94-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="ddc94-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="ddc94-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ddc94-193">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="ddc94-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ddc94-194">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ddc94-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddc94-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc94-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddc94-196">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ddc94-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ddc94-198">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddc94-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ddc94-199">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ddc94-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddc94-201">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddc94-203">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddc94-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddc94-205">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddc94-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddc94-207">a.</span><span class="sxs-lookup"><span data-stu-id="ddc94-207">a.</span></span> <span data-ttu-id="ddc94-208">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddc94-209">b.</span><span class="sxs-lookup"><span data-stu-id="ddc94-209">b.</span></span> <span data-ttu-id="ddc94-210">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ddc94-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddc94-211">c.</span><span class="sxs-lookup"><span data-stu-id="ddc94-211">c.</span></span> <span data-ttu-id="ddc94-212">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ddc94-213">d.</span><span class="sxs-lookup"><span data-stu-id="ddc94-213">d.</span></span> <span data-ttu-id="ddc94-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="ddc94-215">Tworzenie użytkownika testowego HackerOne</span><span class="sxs-lookup"><span data-stu-id="ddc94-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="ddc94-216">Następnie można utworzyć użytkownika o nazwie Simona Britta w HackerOne.</span><span class="sxs-lookup"><span data-stu-id="ddc94-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="ddc94-217">HackerOne obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="ddc94-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="ddc94-218">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ddc94-218">There is no action item for you in this section.</span></span> <span data-ttu-id="ddc94-219">Po otwarciu HackerOne nowego użytkownika jest tworzony, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="ddc94-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ddc94-220">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się z zespołem pomocy technicznej Certify.</span><span class="sxs-lookup"><span data-stu-id="ddc94-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ddc94-221">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc94-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ddc94-222">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu HackerOne.</span><span class="sxs-lookup"><span data-stu-id="ddc94-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ddc94-224">**Aby przypisać Simona Britta HackerOne, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddc94-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="ddc94-225">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ddc94-227">Na liście aplikacji zaznacz **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-227">In the applications list, select **HackerOne**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="ddc94-229">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ddc94-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ddc94-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ddc94-231">Click **Add** button.</span></span> <span data-ttu-id="ddc94-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddc94-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ddc94-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ddc94-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ddc94-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddc94-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddc94-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddc94-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ddc94-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ddc94-237">Testing single sign-on</span></span>

<span data-ttu-id="ddc94-238">Na koniec należy przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ddc94-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="ddc94-239">Po kliknięciu kafelka HackerOne w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji HackerOne.</span><span class="sxs-lookup"><span data-stu-id="ddc94-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ddc94-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ddc94-240">Additional resources</span></span>

* [<span data-ttu-id="ddc94-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddc94-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddc94-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ddc94-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

