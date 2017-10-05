---
title: 'Samouczek: Integracji Azure Active Directory z Lucidchart | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="92ff7-103">Samouczek: Integracji Azure Active Directory z Lucidchart</span><span class="sxs-lookup"><span data-stu-id="92ff7-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="92ff7-104">Z tego samouczka dowiesz się integrowanie Lucidchart z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92ff7-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92ff7-105">Integracja z usługą Azure AD Lucidchart zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="92ff7-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92ff7-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Lucidchart</span><span class="sxs-lookup"><span data-stu-id="92ff7-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="92ff7-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Lucidchart (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92ff7-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92ff7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="92ff7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92ff7-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92ff7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92ff7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="92ff7-110">Prerequisites</span></span>

<span data-ttu-id="92ff7-111">Aby skonfigurować integrację usługi Azure AD z Lucidchart, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="92ff7-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="92ff7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92ff7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92ff7-113">Lucidchart logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="92ff7-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92ff7-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92ff7-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="92ff7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92ff7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="92ff7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92ff7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92ff7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92ff7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="92ff7-118">Scenario description</span></span>
<span data-ttu-id="92ff7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="92ff7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92ff7-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="92ff7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92ff7-121">Dodawanie Lucidchart z galerii</span><span class="sxs-lookup"><span data-stu-id="92ff7-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="92ff7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="92ff7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="92ff7-123">Dodawanie Lucidchart z galerii</span><span class="sxs-lookup"><span data-stu-id="92ff7-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="92ff7-124">Aby skonfigurować integrację usługi Azure AD Lucidchart, należy dodać Lucidchart z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="92ff7-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92ff7-125">**Aby dodać Lucidchart z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92ff7-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92ff7-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="92ff7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="92ff7-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92ff7-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="92ff7-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="92ff7-133">W polu wyszukiwania wpisz **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-133">In the search box, type **Lucidchart**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="92ff7-135">W panelu wyników wybierz **Lucidchart**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="92ff7-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92ff7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="92ff7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92ff7-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Lucidchart w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92ff7-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Lucidchart jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92ff7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="92ff7-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Lucidchart musi się.</span><span class="sxs-lookup"><span data-stu-id="92ff7-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="92ff7-141">W Lucidchart, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="92ff7-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92ff7-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Lucidchart, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="92ff7-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92ff7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="92ff7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92ff7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="92ff7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92ff7-145">**[Tworzenie użytkownika testowego Lucidchart](#creating-a-lucidchart-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Lucidchart połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92ff7-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92ff7-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="92ff7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92ff7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="92ff7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92ff7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="92ff7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92ff7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="92ff7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="92ff7-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Lucidchart, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92ff7-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="92ff7-151">W portalu Azure na **Lucidchart** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="92ff7-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="92ff7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="92ff7-155">Na **Lucidchart domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92ff7-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="92ff7-157">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="92ff7-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="92ff7-158">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="92ff7-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="92ff7-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="92ff7-160">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92ff7-162">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Lucidchart jako administrator.</span><span class="sxs-lookup"><span data-stu-id="92ff7-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="92ff7-163">W menu u góry kliknij **zespołu**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="92ff7-164">![Zespół](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "zespołu")</span><span class="sxs-lookup"><span data-stu-id="92ff7-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="92ff7-165">Kliknij przycisk **aplikacji \> Zarządzanie SAML**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="92ff7-166">![Zarządzanie SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Zarządzanie SAML")</span><span class="sxs-lookup"><span data-stu-id="92ff7-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="92ff7-167">Na **ustawienia uwierzytelniania SAML** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92ff7-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="92ff7-168">a.</span><span class="sxs-lookup"><span data-stu-id="92ff7-168">a.</span></span> <span data-ttu-id="92ff7-169">Wybierz **Włącz uwierzytelnianie SAML**, a następnie kliknij przycisk **opcjonalnie**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="92ff7-170">![Ustawienia uwierzytelniania SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML ustawienia uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="92ff7-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="92ff7-171">b.</span><span class="sxs-lookup"><span data-stu-id="92ff7-171">b.</span></span> <span data-ttu-id="92ff7-172">W **domeny** tekstowym, wpisz domenę, a następnie kliknij przycisk **zmiana certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="92ff7-173">![Zmienianie certyfikatu](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Zmienianie certyfikatu")</span><span class="sxs-lookup"><span data-stu-id="92ff7-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="92ff7-174">c.</span><span class="sxs-lookup"><span data-stu-id="92ff7-174">c.</span></span> <span data-ttu-id="92ff7-175">Otwórz plik metadanych pobranych, skopiuj zawartość, a następnie wklej go do **przekazać metadanych** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="92ff7-176">![Przekaż metadanych](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "przekazać metadanych")</span><span class="sxs-lookup"><span data-stu-id="92ff7-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="92ff7-177">d.</span><span class="sxs-lookup"><span data-stu-id="92ff7-177">d.</span></span> <span data-ttu-id="92ff7-178">Wybierz **automatyczne dodawanie nowych użytkowników do zespołu**, a następnie kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="92ff7-179">![Zapisz zmiany](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "zapisać zmiany")</span><span class="sxs-lookup"><span data-stu-id="92ff7-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="92ff7-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="92ff7-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92ff7-181">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="92ff7-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92ff7-182">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92ff7-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92ff7-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92ff7-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="92ff7-184">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="92ff7-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="92ff7-186">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92ff7-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92ff7-187">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="92ff7-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92ff7-189">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92ff7-191">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92ff7-193">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92ff7-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92ff7-195">a.</span><span class="sxs-lookup"><span data-stu-id="92ff7-195">a.</span></span> <span data-ttu-id="92ff7-196">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92ff7-197">b.</span><span class="sxs-lookup"><span data-stu-id="92ff7-197">b.</span></span> <span data-ttu-id="92ff7-198">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92ff7-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92ff7-199">c.</span><span class="sxs-lookup"><span data-stu-id="92ff7-199">c.</span></span> <span data-ttu-id="92ff7-200">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92ff7-201">d.</span><span class="sxs-lookup"><span data-stu-id="92ff7-201">d.</span></span> <span data-ttu-id="92ff7-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="92ff7-203">Tworzenie użytkownika testowego Lucidchart</span><span class="sxs-lookup"><span data-stu-id="92ff7-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="92ff7-204">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej Lucidchart użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92ff7-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="92ff7-205">Gdy przypisany użytkownik próbuje zalogować się przy użyciu panelu dostępu Lucidchart, Lucidchart sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="92ff7-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="92ff7-206">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="92ff7-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92ff7-207">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92ff7-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92ff7-208">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="92ff7-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="92ff7-210">**Aby przypisać Simona Britta Lucidchart, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92ff7-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="92ff7-211">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="92ff7-213">Na liście aplikacji zaznacz **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-213">In the applications list, select **Lucidchart**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="92ff7-215">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="92ff7-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="92ff7-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="92ff7-217">Click **Add** button.</span></span> <span data-ttu-id="92ff7-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="92ff7-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="92ff7-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92ff7-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92ff7-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92ff7-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92ff7-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="92ff7-223">Testing single sign-on</span></span>

<span data-ttu-id="92ff7-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="92ff7-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92ff7-225">Po kliknięciu kafelka Lucidchart w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="92ff7-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="92ff7-226">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92ff7-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92ff7-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="92ff7-227">Additional resources</span></span>

* [<span data-ttu-id="92ff7-228">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92ff7-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92ff7-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92ff7-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

