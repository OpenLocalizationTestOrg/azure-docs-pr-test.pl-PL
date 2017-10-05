---
title: 'Samouczek: Integracji Azure Active Directory z Work.com | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="18b62-103">Samouczek: Integracji Azure Active Directory z Work.com</span><span class="sxs-lookup"><span data-stu-id="18b62-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="18b62-104">Z tego samouczka dowiesz się integrowanie Work.com z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18b62-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18b62-105">Integracja z usługą Azure AD Work.com zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="18b62-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="18b62-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Work.com</span><span class="sxs-lookup"><span data-stu-id="18b62-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="18b62-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Work.com (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18b62-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18b62-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="18b62-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="18b62-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18b62-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18b62-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="18b62-110">Prerequisites</span></span>

<span data-ttu-id="18b62-111">Aby skonfigurować integrację usługi Azure AD z Work.com, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="18b62-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="18b62-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18b62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18b62-113">Work.com logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="18b62-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18b62-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="18b62-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18b62-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="18b62-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18b62-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="18b62-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18b62-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18b62-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18b62-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="18b62-118">Scenario description</span></span>
<span data-ttu-id="18b62-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="18b62-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18b62-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="18b62-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18b62-121">Dodaj Work.com z galerii</span><span class="sxs-lookup"><span data-stu-id="18b62-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="18b62-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18b62-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="18b62-123">Dodaj Work.com z galerii</span><span class="sxs-lookup"><span data-stu-id="18b62-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="18b62-124">Aby skonfigurować integrację usługi Azure AD Work.com, należy dodać Work.com z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="18b62-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18b62-125">**Aby dodać Work.com z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="18b62-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="18b62-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="18b62-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="18b62-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="18b62-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="18b62-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="18b62-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="18b62-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18b62-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="18b62-133">W polu wyszukiwania wpisz **Work.com**, wybierz pozycję **Work.com** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="18b62-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Dodaj z galerii](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="18b62-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18b62-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="18b62-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Work.com w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="18b62-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18b62-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Work.com jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18b62-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="18b62-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Work.com musi się.</span><span class="sxs-lookup"><span data-stu-id="18b62-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="18b62-139">W Work.com, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="18b62-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="18b62-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Work.com, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="18b62-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="18b62-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="18b62-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="18b62-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="18b62-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18b62-143">**[Tworzenie użytkownika testowego Work.com](#create-a-workcom-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Work.com połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="18b62-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="18b62-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="18b62-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18b62-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="18b62-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="18b62-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18b62-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="18b62-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Work.com.</span><span class="sxs-lookup"><span data-stu-id="18b62-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="18b62-148">Aby skonfigurować logowanie jednokrotne, należy skonfigurować niestandardową nazwę domeny Work.com jeszcze.</span><span class="sxs-lookup"><span data-stu-id="18b62-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="18b62-149">Należy zdefiniować co najmniej nazwę domeny, sprawdzenie nazwę domeny i wdrożyć ją w całej organizacji.</span><span class="sxs-lookup"><span data-stu-id="18b62-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="18b62-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Work.com, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="18b62-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="18b62-151">W portalu Azure na **Work.com** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="18b62-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="18b62-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="18b62-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="18b62-155">Na **Work.com domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="18b62-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Sekcja Work.com domeny i adresy URL](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="18b62-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="18b62-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18b62-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="18b62-158">This value is not real.</span></span> <span data-ttu-id="18b62-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="18b62-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="18b62-160">Skontaktuj się z [zespołem pomocy technicznej klienta Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="18b62-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="18b62-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="18b62-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="18b62-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="18b62-163">Click **Save** button.</span></span>

    ![Przycisk Zapisz](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="18b62-165">Na **konfiguracji Work.com** , kliknij przycisk **skonfigurować Work.com** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="18b62-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="18b62-166">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="18b62-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sekcja konfiguracji Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="18b62-168">Zaloguj się jako administrator dzierżawy Work.com.</span><span class="sxs-lookup"><span data-stu-id="18b62-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="18b62-169">Przejdź do **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="18b62-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="18b62-170">![Instalator](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="18b62-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="18b62-171">W okienku nawigacji po lewej stronie w **Administruj** , kliknij przycisk **Zarządzanie domenami** rozwiń sekcję powiązane, a następnie kliknij przycisk **Moje domeny** otworzyć **Moje domeny** strony.</span><span class="sxs-lookup"><span data-stu-id="18b62-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="18b62-172">![Mojej domeny](./media/active-directory-saas-work-com-tutorial/ic767825.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="18b62-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="18b62-173">Aby sprawdzić, czy domeny nie został skonfigurowany prawidłowo, upewnij się, że jest on "**krok 4 wdrożone dla użytkowników**" i zapoznaj się z "**Moje ustawienia domeny**".</span><span class="sxs-lookup"><span data-stu-id="18b62-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="18b62-174">![Wdrożonego dla użytkownika domeny](./media/active-directory-saas-work-com-tutorial/ic784377.png "wdrożonego dla użytkownika domeny")</span><span class="sxs-lookup"><span data-stu-id="18b62-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="18b62-175">Zaloguj się do dzierżawy Work.com.</span><span class="sxs-lookup"><span data-stu-id="18b62-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="18b62-176">Przejdź do **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="18b62-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="18b62-177">![Instalator](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="18b62-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="18b62-178">Rozwiń węzeł **kontroli bezpieczeństwa** menu, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="18b62-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="18b62-179">![Single Sign-On ustawienia](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="18b62-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="18b62-180">Na **ustawień rejestracji jednokrotnej** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="18b62-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="18b62-181">![Włączone SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML włączone")</span><span class="sxs-lookup"><span data-stu-id="18b62-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="18b62-182">a.</span><span class="sxs-lookup"><span data-stu-id="18b62-182">a.</span></span> <span data-ttu-id="18b62-183">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="18b62-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="18b62-184">b.</span><span class="sxs-lookup"><span data-stu-id="18b62-184">b.</span></span> <span data-ttu-id="18b62-185">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="18b62-185">Click **New**.</span></span>

15. <span data-ttu-id="18b62-186">W **SAML pojedynczego logowania jednokrotnego ustawienia** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="18b62-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="18b62-187">![SAML pojedynczy znak na ustawienie](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML pojedynczy znak na ustawienie")</span><span class="sxs-lookup"><span data-stu-id="18b62-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="18b62-188">a.</span><span class="sxs-lookup"><span data-stu-id="18b62-188">a.</span></span> <span data-ttu-id="18b62-189">W **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="18b62-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="18b62-190">Wartość dla **nazwa** automatycznie wypełnić **Nazwa interfejsu API** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="18b62-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="18b62-191">b.</span><span class="sxs-lookup"><span data-stu-id="18b62-191">b.</span></span> <span data-ttu-id="18b62-192">W **wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="18b62-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="18b62-193">c.</span><span class="sxs-lookup"><span data-stu-id="18b62-193">c.</span></span> <span data-ttu-id="18b62-194">Aby przekazać certyfikat pobrany z portalu Azure, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="18b62-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="18b62-195">d.</span><span class="sxs-lookup"><span data-stu-id="18b62-195">d.</span></span> <span data-ttu-id="18b62-196">W **identyfikator jednostki** pole tekstowe, typ `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="18b62-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="18b62-197">e.</span><span class="sxs-lookup"><span data-stu-id="18b62-197">e.</span></span> <span data-ttu-id="18b62-198">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera identyfikator federacji z obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="18b62-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="18b62-199">f.</span><span class="sxs-lookup"><span data-stu-id="18b62-199">f.</span></span> <span data-ttu-id="18b62-200">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentfier instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="18b62-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="18b62-201">g.</span><span class="sxs-lookup"><span data-stu-id="18b62-201">g.</span></span> <span data-ttu-id="18b62-202">W **adresu URL logowania do dostawcy tożsamości** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="18b62-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="18b62-203">h.</span><span class="sxs-lookup"><span data-stu-id="18b62-203">h.</span></span> <span data-ttu-id="18b62-204">W **adres URL wylogowania dostawcy tożsamości** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="18b62-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="18b62-205">i.</span><span class="sxs-lookup"><span data-stu-id="18b62-205">i.</span></span> <span data-ttu-id="18b62-206">Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="18b62-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="18b62-207">j.</span><span class="sxs-lookup"><span data-stu-id="18b62-207">j.</span></span> <span data-ttu-id="18b62-208">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="18b62-208">Click **Save**.</span></span>

16. <span data-ttu-id="18b62-209">W portalu klasycznym Work.com, w okienku nawigacji po lewej stronie kliknij **Zarządzanie domenami** rozwiń sekcję powiązane, a następnie kliknij przycisk **Moje domeny** otworzyć **Moje domeny** strony.</span><span class="sxs-lookup"><span data-stu-id="18b62-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="18b62-210">![Mojej domeny](./media/active-directory-saas-work-com-tutorial/ic794115.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="18b62-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="18b62-211">Na **Moje domeny** strony w **znakowanie strony logowania** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="18b62-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="18b62-212">![Znakowanie strony logowania](./media/active-directory-saas-work-com-tutorial/ic767826.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="18b62-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="18b62-213">Na **znakowanie strony logowania** strony w **usługi uwierzytelniania** sekcji Nazwa Twojej **ustawienia logowania jednokrotnego SAML** jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="18b62-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="18b62-214">Wybierz go, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="18b62-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="18b62-215">![Znakowanie strony logowania](./media/active-directory-saas-work-com-tutorial/ic784366.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="18b62-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="18b62-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="18b62-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="18b62-217">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="18b62-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="18b62-218">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18b62-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="18b62-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18b62-219">Create an Azure AD test user</span></span>
<span data-ttu-id="18b62-220">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="18b62-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="18b62-222">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="18b62-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="18b62-223">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="18b62-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18b62-225">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="18b62-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18b62-227">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18b62-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18b62-229">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="18b62-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18b62-231">a.</span><span class="sxs-lookup"><span data-stu-id="18b62-231">a.</span></span> <span data-ttu-id="18b62-232">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18b62-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18b62-233">b.</span><span class="sxs-lookup"><span data-stu-id="18b62-233">b.</span></span> <span data-ttu-id="18b62-234">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="18b62-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18b62-235">c.</span><span class="sxs-lookup"><span data-stu-id="18b62-235">c.</span></span> <span data-ttu-id="18b62-236">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="18b62-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="18b62-237">d.</span><span class="sxs-lookup"><span data-stu-id="18b62-237">d.</span></span> <span data-ttu-id="18b62-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="18b62-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="18b62-239">Tworzenie użytkownika testowego Work.com</span><span class="sxs-lookup"><span data-stu-id="18b62-239">Create a Work.com test user</span></span>
<span data-ttu-id="18b62-240">Dla usługi Azure Active Directory aby użytkownicy mogli się zalogować muszą one być przygotowana do Work.com.</span><span class="sxs-lookup"><span data-stu-id="18b62-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="18b62-241">W przypadku Work.com Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="18b62-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="18b62-242">Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="18b62-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="18b62-243">Zalogować się do witryny firmy Work.com jako administrator.</span><span class="sxs-lookup"><span data-stu-id="18b62-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="18b62-244">Przejdź do **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="18b62-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="18b62-245">![Instalator](./media/active-directory-saas-work-com-tutorial/IC794108.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="18b62-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="18b62-246">Przejdź do **Zarządzanie użytkownikami \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="18b62-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="18b62-247">![Zarządzaj użytkownikami](./media/active-directory-saas-work-com-tutorial/IC784369.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="18b62-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="18b62-248">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="18b62-248">Click **New User**.</span></span>
   
    <span data-ttu-id="18b62-249">![Wszyscy użytkownicy](./media/active-directory-saas-work-com-tutorial/IC794117.png "wszyscy użytkownicy")</span><span class="sxs-lookup"><span data-stu-id="18b62-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="18b62-250">W sekcji Edycja użytkownika należy wykonać następujące czynności, w przypadku atrybutów elementów prawidłową Azure AD konta chcesz udostępnić do powiązanych pól tekstowych:</span><span class="sxs-lookup"><span data-stu-id="18b62-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="18b62-251">![Edycja użytkownika](./media/active-directory-saas-work-com-tutorial/ic794118.png "Edycja użytkownika")</span><span class="sxs-lookup"><span data-stu-id="18b62-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="18b62-252">a.</span><span class="sxs-lookup"><span data-stu-id="18b62-252">a.</span></span> <span data-ttu-id="18b62-253">W **imię** pole tekstowe, typ **imię** użytkownika **Britta**.</span><span class="sxs-lookup"><span data-stu-id="18b62-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="18b62-254">b.</span><span class="sxs-lookup"><span data-stu-id="18b62-254">b.</span></span> <span data-ttu-id="18b62-255">W **nazwisko** pole tekstowe, typ **nazwisko** użytkownika **Simona**.</span><span class="sxs-lookup"><span data-stu-id="18b62-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="18b62-256">c.</span><span class="sxs-lookup"><span data-stu-id="18b62-256">c.</span></span> <span data-ttu-id="18b62-257">W **Alias** pole tekstowe, typ **nazwa** użytkownika **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="18b62-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="18b62-258">d.</span><span class="sxs-lookup"><span data-stu-id="18b62-258">d.</span></span> <span data-ttu-id="18b62-259">W **E-mail** pole tekstowe, typ **adres e-mail** użytkownika  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="18b62-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="18b62-260">e.</span><span class="sxs-lookup"><span data-stu-id="18b62-260">e.</span></span> <span data-ttu-id="18b62-261">W **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika użytkownika, takich jak  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="18b62-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="18b62-262">f.</span><span class="sxs-lookup"><span data-stu-id="18b62-262">f.</span></span> <span data-ttu-id="18b62-263">W **pseudonim** pola tekstowego, a typ **pseudonim** użytkownika **Simona**.</span><span class="sxs-lookup"><span data-stu-id="18b62-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="18b62-264">g.</span><span class="sxs-lookup"><span data-stu-id="18b62-264">g.</span></span> <span data-ttu-id="18b62-265">Wybierz **roli**, **licencji użytkownika**, i **profilu**.</span><span class="sxs-lookup"><span data-stu-id="18b62-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="18b62-266">h.</span><span class="sxs-lookup"><span data-stu-id="18b62-266">h.</span></span> <span data-ttu-id="18b62-267">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="18b62-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="18b62-268">Właściciel konta usługi Azure AD otrzyma wiadomość e-mail, łącznie z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="18b62-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="18b62-269">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18b62-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="18b62-270">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Work.com.</span><span class="sxs-lookup"><span data-stu-id="18b62-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="18b62-272">**Aby przypisać Simona Britta Work.com, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="18b62-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="18b62-273">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="18b62-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="18b62-275">Na liście aplikacji zaznacz **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="18b62-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com na liście aplikacji](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="18b62-277">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="18b62-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="18b62-279">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="18b62-279">Click **Add** button.</span></span> <span data-ttu-id="18b62-280">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18b62-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="18b62-282">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="18b62-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="18b62-283">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18b62-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18b62-284">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18b62-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="18b62-285">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18b62-285">Test single sign-on</span></span>

<span data-ttu-id="18b62-286">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="18b62-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="18b62-287">Po kliknięciu kafelka Work.com w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Work.com.</span><span class="sxs-lookup"><span data-stu-id="18b62-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="18b62-288">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18b62-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18b62-289">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="18b62-289">Additional resources</span></span>

* [<span data-ttu-id="18b62-290">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18b62-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18b62-291">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18b62-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

