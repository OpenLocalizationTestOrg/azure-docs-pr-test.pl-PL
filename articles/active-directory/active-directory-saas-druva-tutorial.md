---
title: 'Samouczek: Integracji Azure Active Directory z Druva | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="3a2c5-103">Samouczek: Integracji Azure Active Directory z Druva</span><span class="sxs-lookup"><span data-stu-id="3a2c5-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="3a2c5-104">Z tego samouczka dowiesz się integrowanie Druva z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a2c5-105">Integracja z usługą Azure AD Druva zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a2c5-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Druva.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="3a2c5-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Druva (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3a2c5-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3a2c5-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a2c5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3a2c5-110">Prerequisites</span></span>

<span data-ttu-id="3a2c5-111">Aby skonfigurować integrację usługi Azure AD z Druva, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="3a2c5-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a2c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a2c5-113">Druva logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3a2c5-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a2c5-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a2c5-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a2c5-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a2c5-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a2c5-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3a2c5-118">Scenario description</span></span>
<span data-ttu-id="3a2c5-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a2c5-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a2c5-121">Dodawanie Druva z galerii</span><span class="sxs-lookup"><span data-stu-id="3a2c5-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="3a2c5-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3a2c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="3a2c5-123">Dodawanie Druva z galerii</span><span class="sxs-lookup"><span data-stu-id="3a2c5-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="3a2c5-124">Aby skonfigurować integrację usługi Azure AD Druva, należy dodać Druva z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a2c5-125">**Aby dodać Druva z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3a2c5-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a2c5-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="3a2c5-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a2c5-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="3a2c5-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="3a2c5-133">W polu wyszukiwania wpisz **Druva**, wybierz pozycję **Druva** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva na liście wyników](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3a2c5-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3a2c5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3a2c5-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Druva w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a2c5-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Druva jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="3a2c5-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Druva musi się.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="3a2c5-139">W Druva, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3a2c5-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Druva, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a2c5-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a2c5-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a2c5-143">**[Tworzenie użytkownika testowego Druva](#create-a-druva-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Druva połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a2c5-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a2c5-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3a2c5-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3a2c5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3a2c5-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Druva.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="3a2c5-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Druva, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3a2c5-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="3a2c5-149">W portalu Azure na **Druva** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="3a2c5-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="3a2c5-153">Na **Druva domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="3a2c5-155">W **adres URL logowania** tekstowym, wpisz adres URL:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="3a2c5-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="3a2c5-156">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="3a2c5-158">Aplikacja Druva oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do Twojej **atrybuty tokenu SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="3a2c5-160">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na powyższej ilustracji i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="3a2c5-161">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="3a2c5-161">Attribute Name</span></span>      | <span data-ttu-id="3a2c5-162">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="3a2c5-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="3a2c5-163">zsynchronizowana\_uwierzytelniania\_tokenu</span><span class="sxs-lookup"><span data-stu-id="3a2c5-163">insync\_auth\_token</span></span> |<span data-ttu-id="3a2c5-164">Wprowadź wartość tokenu w wygenerowanym</span><span class="sxs-lookup"><span data-stu-id="3a2c5-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="3a2c5-165">a.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-165">a.</span></span> <span data-ttu-id="3a2c5-166">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="3a2c5-169">b.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-169">b.</span></span> <span data-ttu-id="3a2c5-170">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3a2c5-171">c.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-171">c.</span></span> <span data-ttu-id="3a2c5-172">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="3a2c5-173">Wartość tokenu wygenerowanego znajduje się w dalszej części samouczka.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="3a2c5-174">d.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-174">d.</span></span> <span data-ttu-id="3a2c5-175">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="3a2c5-176">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-176">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3a2c5-178">Na **konfiguracji Druva** , kliknij przycisk **skonfigurować Druva** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3a2c5-179">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="3a2c5-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="3a2c5-181">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Druva.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="3a2c5-182">Przejdź do **zarządzanie \> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="3a2c5-183">![Ustawienia](./media/active-directory-saas-druva-tutorial/ic795091.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="3a2c5-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="3a2c5-184">W oknie dialogowym Ustawienia rejestracji jednokrotnej wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="3a2c5-185">![Single Sign-On ustawienia](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="3a2c5-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="3a2c5-186">a.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-186">a.</span></span> <span data-ttu-id="3a2c5-187">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **adres URL logowania dostawcy identyfikator** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="3a2c5-188">b.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-188">b.</span></span> <span data-ttu-id="3a2c5-189">Wklej **Sign-Out URL** wartość, która została skopiowana z portalu Azure do **adres URL wylogowania dostawcy identyfikator** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="3a2c5-190">c.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-190">c.</span></span> <span data-ttu-id="3a2c5-191">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikat dostawcy identyfikator** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="3a2c5-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="3a2c5-192">d.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-192">d.</span></span> <span data-ttu-id="3a2c5-193">Aby otworzyć **ustawienia** kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="3a2c5-194">Na **ustawienia** kliknij przycisk **generowania tokenu rejestracji Jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="3a2c5-195">![Ustawienia](./media/active-directory-saas-druva-tutorial/ic795093.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="3a2c5-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="3a2c5-196">Na **pojedynczego logowania jednokrotnego tokenu uwierzytelniania** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="3a2c5-197">![Token rejestracji Jednokrotnej](./media/active-directory-saas-druva-tutorial/ic795094.png "tokenu rejestracji Jednokrotnej")</span><span class="sxs-lookup"><span data-stu-id="3a2c5-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="3a2c5-198">a.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-198">a.</span></span> <span data-ttu-id="3a2c5-199">Kliknij przycisk **kopiowania**, wklej skopiowane wartości w **wartość** textbox w **Dodawanie atrybutu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="3a2c5-200">b.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-200">b.</span></span> <span data-ttu-id="3a2c5-201">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="3a2c5-202">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="3a2c5-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a2c5-203">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a2c5-204">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a2c5-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3a2c5-205">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a2c5-205">Create an Azure AD test user</span></span>

<span data-ttu-id="3a2c5-206">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="3a2c5-208">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3a2c5-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a2c5-209">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3a2c5-211">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3a2c5-213">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3a2c5-215">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3a2c5-217">a.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-217">a.</span></span> <span data-ttu-id="3a2c5-218">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a2c5-219">b.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-219">b.</span></span> <span data-ttu-id="3a2c5-220">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3a2c5-221">c.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-221">c.</span></span> <span data-ttu-id="3a2c5-222">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3a2c5-223">d.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-223">d.</span></span> <span data-ttu-id="3a2c5-224">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="3a2c5-225">Tworzenie użytkownika testowego Druva</span><span class="sxs-lookup"><span data-stu-id="3a2c5-225">Create a Druva test user</span></span>

<span data-ttu-id="3a2c5-226">Aby umożliwić użytkownikom zalogować się do Druva usługi Azure AD, musi być przygotowana do Druva.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="3a2c5-227">W przypadku Druva Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="3a2c5-228">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3a2c5-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3a2c5-229">Zaloguj się do Twojego **Druva** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="3a2c5-230">Przejdź do **zarządzanie \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="3a2c5-231">![Zarządzaj użytkownikami](./media/active-directory-saas-druva-tutorial/ic795097.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="3a2c5-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="3a2c5-232">Kliknij przycisk **tworzenia nowych**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="3a2c5-233">![Zarządzaj użytkownikami](./media/active-directory-saas-druva-tutorial/ic795098.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="3a2c5-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="3a2c5-234">W oknie dialogowym Tworzenie nowego użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="3a2c5-235">![Utwórz NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "utworzyć NewUser")</span><span class="sxs-lookup"><span data-stu-id="3a2c5-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="3a2c5-236">a.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-236">a.</span></span> <span data-ttu-id="3a2c5-237">W **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="3a2c5-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="3a2c5-238">b.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-238">b.</span></span> <span data-ttu-id="3a2c5-239">W **nazwa** pole tekstowe, wprowadź nazwę użytkownika, takich jak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="3a2c5-240">c.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-240">c.</span></span> <span data-ttu-id="3a2c5-241">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="3a2c5-242">Możesz użyć innych Druva użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Druva do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3a2c5-243">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a2c5-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="3a2c5-244">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Druva.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="3a2c5-246">**Aby przypisać Simona Britta Druva, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3a2c5-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="3a2c5-247">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3a2c5-249">Na liście aplikacji zaznacz **Druva**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-249">In the applications list, select **Druva**.</span></span>

    ![Łącze Druva na liście aplikacji](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="3a2c5-251">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="3a2c5-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-253">Click **Add** button.</span></span> <span data-ttu-id="3a2c5-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="3a2c5-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a2c5-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a2c5-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3a2c5-259">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3a2c5-259">Test single sign-on</span></span>

<span data-ttu-id="3a2c5-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a2c5-261">Po kliknięciu kafelka Druva w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Druva.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="3a2c5-262">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3a2c5-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3a2c5-263">Additional resources</span></span>

* [<span data-ttu-id="3a2c5-264">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a2c5-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a2c5-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a2c5-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

