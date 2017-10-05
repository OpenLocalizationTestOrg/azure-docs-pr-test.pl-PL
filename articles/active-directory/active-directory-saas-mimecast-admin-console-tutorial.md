---
title: 'Samouczek: Integracji Azure Active Directory z konsoli administracyjnej Mimecast | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Mimecast konsoli administracyjnej."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="dfe47-103">Samouczek: Integracji Azure Active Directory z konsoli administracyjnej Mimecast</span><span class="sxs-lookup"><span data-stu-id="dfe47-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="dfe47-104">Z tego samouczka dowiesz się integrowanie Mimecast konsoli administracyjnej w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfe47-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dfe47-105">Integrowanie Mimecast konsoli administracyjnej z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="dfe47-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dfe47-106">Można kontrolować w usłudze Azure AD, który ma dostęp do konsoli administracyjnej Mimecast.</span><span class="sxs-lookup"><span data-stu-id="dfe47-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="dfe47-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do konsoli administracyjnej Mimecast (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfe47-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dfe47-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dfe47-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="dfe47-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dfe47-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfe47-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dfe47-110">Prerequisites</span></span>

<span data-ttu-id="dfe47-111">Aby skonfigurować integrację usługi Azure AD z konsoli administracyjnej Mimecast, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="dfe47-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="dfe47-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfe47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dfe47-113">Konsola administracyjna Mimecast logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dfe47-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dfe47-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dfe47-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="dfe47-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dfe47-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="dfe47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dfe47-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfe47-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dfe47-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="dfe47-118">Scenario description</span></span>
<span data-ttu-id="dfe47-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="dfe47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dfe47-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="dfe47-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dfe47-121">Dodawanie Mimecast konsoli administracyjnej z galerii</span><span class="sxs-lookup"><span data-stu-id="dfe47-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="dfe47-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dfe47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="dfe47-123">Dodawanie Mimecast konsoli administracyjnej z galerii</span><span class="sxs-lookup"><span data-stu-id="dfe47-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="dfe47-124">Aby skonfigurować integrację usługi Azure AD Mimecast konsoli administracyjnej, należy dodać Mimecast konsoli administracyjnej z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="dfe47-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dfe47-125">**Aby dodać Mimecast konsoli administracyjnej z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dfe47-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dfe47-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dfe47-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="dfe47-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dfe47-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="dfe47-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="dfe47-133">W polu wyszukiwania wpisz **konsoli administracyjnej Mimecast**, wybierz pozycję **Mimecast konsoli administracyjnej** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="dfe47-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Konsola administracyjna Mimecast na liście wyników](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dfe47-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dfe47-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dfe47-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dfe47-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w konsoli administracyjnej Mimecast jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfe47-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="dfe47-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w konsoli administracyjnej Mimecast musi się.</span><span class="sxs-lookup"><span data-stu-id="dfe47-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="dfe47-139">W konsoli administracyjnej Mimecast, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="dfe47-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dfe47-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mimecast konsoli administracyjnej, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="dfe47-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dfe47-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="dfe47-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dfe47-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dfe47-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dfe47-143">**[Tworzenie użytkownika testowego konsoli administracyjnej Mimecast](#create-a-mimecast-admin-console-test-user)**  — aby odpowiednikiem Simona Britta w konsoli administracyjnej Mimecast połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dfe47-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dfe47-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dfe47-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dfe47-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="dfe47-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dfe47-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dfe47-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dfe47-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w konsoli administracyjnej Mimecast aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dfe47-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="dfe47-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dfe47-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="dfe47-149">W portalu Azure na **konsoli administracyjnej Mimecast** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="dfe47-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="dfe47-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="dfe47-153">Na **adresy URL i domeny konsoli administracyjnej Mimecast** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dfe47-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny konsoli administracyjnej Mimecast pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="dfe47-155">W **adres URL logowania** tekstowym, wpisz adres URL:</span><span class="sxs-lookup"><span data-stu-id="dfe47-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="dfe47-156">Zaloguj się na adres URL jest określonego regionu.</span><span class="sxs-lookup"><span data-stu-id="dfe47-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="dfe47-157">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dfe47-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="dfe47-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dfe47-159">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dfe47-161">Na **Konfiguracja konsoli administratora Mimecast** kliknij **skonfigurować Mimecast konsoli administracyjnej** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="dfe47-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dfe47-162">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="dfe47-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja konsoli administratora Mimecast](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="dfe47-164">W oknie przeglądarki innej witryny sieci web Zaloguj się do konsoli administracyjnej Mimecast jako administrator.</span><span class="sxs-lookup"><span data-stu-id="dfe47-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="dfe47-165">Przejdź do **usług \> aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="dfe47-166">![Usługi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "usług")</span><span class="sxs-lookup"><span data-stu-id="dfe47-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="dfe47-167">Kliknij przycisk **profile uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="dfe47-168">![Profile uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "profile uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="dfe47-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="dfe47-169">Kliknij przycisk **nowy profil uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="dfe47-170">![Nowych profilów uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "nowych profilów uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="dfe47-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="dfe47-171">W **profilu uwierzytelniania** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dfe47-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="dfe47-172">![Profil uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "profilu uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="dfe47-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="dfe47-173">a.</span><span class="sxs-lookup"><span data-stu-id="dfe47-173">a.</span></span> <span data-ttu-id="dfe47-174">W **opis** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dfe47-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="dfe47-175">b.</span><span class="sxs-lookup"><span data-stu-id="dfe47-175">b.</span></span> <span data-ttu-id="dfe47-176">Wybierz **wymusić uwierzytelnianie SAML dla konsoli administracyjnej Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="dfe47-177">c.</span><span class="sxs-lookup"><span data-stu-id="dfe47-177">c.</span></span> <span data-ttu-id="dfe47-178">Jako **dostawcy**, wybierz pozycję **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="dfe47-179">d.</span><span class="sxs-lookup"><span data-stu-id="dfe47-179">d.</span></span> <span data-ttu-id="dfe47-180">Wklej **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure do **adres URL wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="dfe47-181">e.</span><span class="sxs-lookup"><span data-stu-id="dfe47-181">e.</span></span> <span data-ttu-id="dfe47-182">Wklej **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure do **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="dfe47-183">f.</span><span class="sxs-lookup"><span data-stu-id="dfe47-183">f.</span></span> <span data-ttu-id="dfe47-184">Wklej **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure do **adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="dfe47-185">Wartość adresu URL logowania i wartość adresu URL wylogowania dotyczą konsoli administracyjnej Mimecast takie same.</span><span class="sxs-lookup"><span data-stu-id="dfe47-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="dfe47-186">g.</span><span class="sxs-lookup"><span data-stu-id="dfe47-186">g.</span></span> <span data-ttu-id="dfe47-187">Otwórz certyfikat base-64 pobrany z portalu Azure w programie Notatnik, Usuń pierwszy wiersz ("*--*") i ostatniego wiersza ("*--*"), skopiuj pozostała zawartość do sieci Schowka, a następnie wklej go do **certyfikat dostawcy tożsamości (metadanymi)** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="dfe47-188">h.</span><span class="sxs-lookup"><span data-stu-id="dfe47-188">h.</span></span> <span data-ttu-id="dfe47-189">Wybierz **Zezwalaj funkcji logowania jednokrotnego w**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="dfe47-190">i.</span><span class="sxs-lookup"><span data-stu-id="dfe47-190">i.</span></span> <span data-ttu-id="dfe47-191">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dfe47-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="dfe47-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dfe47-193">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="dfe47-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dfe47-194">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dfe47-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dfe47-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfe47-195">Create an Azure AD test user</span></span>

<span data-ttu-id="dfe47-196">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dfe47-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="dfe47-198">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dfe47-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dfe47-199">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dfe47-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="dfe47-201">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="dfe47-203">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="dfe47-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="dfe47-205">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dfe47-205">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dfe47-207">a.</span><span class="sxs-lookup"><span data-stu-id="dfe47-207">a.</span></span> <span data-ttu-id="dfe47-208">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dfe47-209">b.</span><span class="sxs-lookup"><span data-stu-id="dfe47-209">b.</span></span> <span data-ttu-id="dfe47-210">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dfe47-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="dfe47-211">c.</span><span class="sxs-lookup"><span data-stu-id="dfe47-211">c.</span></span> <span data-ttu-id="dfe47-212">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="dfe47-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="dfe47-213">d.</span><span class="sxs-lookup"><span data-stu-id="dfe47-213">d.</span></span> <span data-ttu-id="dfe47-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="dfe47-215">Tworzenie użytkownika testowego Mimecast konsoli administracyjnej</span><span class="sxs-lookup"><span data-stu-id="dfe47-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="dfe47-216">Aby włączyć użytkowników usługi Azure AD zalogować się do konsoli administracyjnej Mimecast, muszą mieć przydzielone do konsoli administracyjnej Mimecast.</span><span class="sxs-lookup"><span data-stu-id="dfe47-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="dfe47-217">W przypadku konsoli administracyjnej Mimecast Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="dfe47-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="dfe47-218">Należy zarejestrować domeny, przed przystąpieniem do tworzenia użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dfe47-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="dfe47-219">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dfe47-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="dfe47-220">Zaloguj się na Twojej **konsoli administracyjnej Mimecast** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="dfe47-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="dfe47-221">Przejdź do **katalogów \> wewnętrzny**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="dfe47-222">![Katalogi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "katalogów")</span><span class="sxs-lookup"><span data-stu-id="dfe47-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="dfe47-223">Kliknij przycisk **zarejestrować nową domenę**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="dfe47-224">![Zarejestrować nową domenę](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "zarejestrować nową domenę")</span><span class="sxs-lookup"><span data-stu-id="dfe47-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="dfe47-225">Po utworzeniu nowej domeny, kliknij przycisk **nowy adres**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="dfe47-226">![Nowy adres](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "nowy adres")</span><span class="sxs-lookup"><span data-stu-id="dfe47-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="dfe47-227">W oknie dialogowym Nowy adres wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dfe47-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="dfe47-228">![Zapisz](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Zapisz")</span><span class="sxs-lookup"><span data-stu-id="dfe47-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="dfe47-229">a.</span><span class="sxs-lookup"><span data-stu-id="dfe47-229">a.</span></span> <span data-ttu-id="dfe47-230">Typ **adres E-mail**, **globalną nazwę**, **hasło**, i **Potwierdź hasło** atrybutów elementów prawidłową usługi Azure AD konto ma chcesz Udostępnij do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="dfe47-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="dfe47-231">b.</span><span class="sxs-lookup"><span data-stu-id="dfe47-231">b.</span></span> <span data-ttu-id="dfe47-232">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="dfe47-233">Inne narzędzia do tworzenia konta użytkownika konsoli administracyjnej Mimecast lub interfejsów API dostarczonych przez Mimecast konsoli administracyjnej można użyć do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfe47-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dfe47-234">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfe47-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="dfe47-235">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do konsoli administracyjnej Mimecast.</span><span class="sxs-lookup"><span data-stu-id="dfe47-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="dfe47-237">**Aby przypisać Simona Britta Mimecast konsoli administracyjnej, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dfe47-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="dfe47-238">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="dfe47-240">Na liście aplikacji zaznacz **konsoli administracyjnej Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![Łącze Mimecast konsoli administracyjnej na liście aplikacji](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="dfe47-242">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dfe47-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="dfe47-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dfe47-244">Click **Add** button.</span></span> <span data-ttu-id="dfe47-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="dfe47-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="dfe47-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dfe47-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dfe47-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dfe47-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dfe47-250">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dfe47-250">Test single sign-on</span></span>

<span data-ttu-id="dfe47-251">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dfe47-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dfe47-252">Po kliknięciu kafelka Mimecast konsoli administracyjnej w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji konsoli administracyjnej Mimecast.</span><span class="sxs-lookup"><span data-stu-id="dfe47-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="dfe47-253">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dfe47-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dfe47-254">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dfe47-254">Additional resources</span></span>

* [<span data-ttu-id="dfe47-255">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfe47-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dfe47-256">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dfe47-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

