---
title: 'Samouczek: Integracji Azure Active Directory z Nexonia | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="bf4a3-103">Samouczek: Integracji Azure Active Directory z Nexonia</span><span class="sxs-lookup"><span data-stu-id="bf4a3-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="bf4a3-104">Z tego samouczka dowiesz się integrowanie Nexonia z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf4a3-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf4a3-105">Integracja z usługą Azure AD Nexonia zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf4a3-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Nexonia</span><span class="sxs-lookup"><span data-stu-id="bf4a3-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="bf4a3-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Nexonia (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf4a3-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf4a3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bf4a3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf4a3-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="bf4a3-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf4a3-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf4a3-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bf4a3-111">Prerequisites</span></span>

<span data-ttu-id="bf4a3-112">Aby skonfigurować integrację usługi Azure AD z Nexonia, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="bf4a3-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf4a3-113">An Azure AD subscription</span></span>
- <span data-ttu-id="bf4a3-114">Nexonia jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bf4a3-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf4a3-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf4a3-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf4a3-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf4a3-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf4a3-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf4a3-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bf4a3-119">Scenario description</span></span>
<span data-ttu-id="bf4a3-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf4a3-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf4a3-122">Dodawanie Nexonia z galerii</span><span class="sxs-lookup"><span data-stu-id="bf4a3-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="bf4a3-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf4a3-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="bf4a3-124">Dodawanie Nexonia z galerii</span><span class="sxs-lookup"><span data-stu-id="bf4a3-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="bf4a3-125">Aby skonfigurować integrację usługi Azure AD Nexonia, należy dodać Nexonia z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf4a3-126">**Aby dodać Nexonia z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf4a3-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bf4a3-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf4a3-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bf4a3-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bf4a3-134">W polu wyszukiwania wpisz **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-134">In the search box, type **Nexonia**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="bf4a3-136">W panelu wyników wybierz **Nexonia**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf4a3-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf4a3-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf4a3-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Nexonia na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bf4a3-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf4a3-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Nexonia jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="bf4a3-141">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Nexonia musi się.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="bf4a3-142">W Nexonia, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf4a3-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Nexonia, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf4a3-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bf4a3-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf4a3-146">**[Tworzenie użytkownika testowego Nexonia](#creating-a-nexonia-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Nexonia połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf4a3-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf4a3-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf4a3-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf4a3-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf4a3-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Nexonia.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="bf4a3-151">Jeśli występują problemy w ramach integracji, zobacz to [łącze](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) dla przewodnik rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="bf4a3-152">Jeśli nadal nie wykryto rozwiązania, następnie podnieść żądania obsługi z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="bf4a3-153">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Nexonia, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="bf4a3-154">W portalu Azure na **Nexonia** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bf4a3-156">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="bf4a3-158">Na **Nexonia domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="bf4a3-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="bf4a3-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf4a3-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-161">This value is not real.</span></span> <span data-ttu-id="bf4a3-162">Zaktualizuj tę wartość przy rzeczywisty adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="bf4a3-163">Skontaktuj się z [zespołem pomocy technicznej Nexonia](https://nexonia.zendesk.com/hc/requests/new) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="bf4a3-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="bf4a3-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bf4a3-168">Na **konfiguracji Nexonia** , kliknij przycisk **skonfigurować Nexonia** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bf4a3-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="bf4a3-171">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej Nexonia](https://nexonia.zendesk.com/hc/requests/new) i podaj następujące:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="bf4a3-172">• Pobrany **certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="bf4a3-173">• **Identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="bf4a3-174">• **Adres URL usługi rejestracji jednokrotnej SAML**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="bf4a3-175">• **Adresu URL wylogowania**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="bf4a3-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bf4a3-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf4a3-177">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf4a3-178">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf4a3-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf4a3-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf4a3-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf4a3-180">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bf4a3-182">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf4a3-183">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf4a3-185">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf4a3-187">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf4a3-189">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bf4a3-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf4a3-191">a.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-191">a.</span></span> <span data-ttu-id="bf4a3-192">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf4a3-193">b.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-193">b.</span></span> <span data-ttu-id="bf4a3-194">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf4a3-195">c.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-195">c.</span></span> <span data-ttu-id="bf4a3-196">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf4a3-197">d.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-197">d.</span></span> <span data-ttu-id="bf4a3-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="bf4a3-199">Tworzenie użytkownika testowego Nexonia</span><span class="sxs-lookup"><span data-stu-id="bf4a3-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="bf4a3-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Nexonia.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="bf4a3-201">Praca z [zespołem pomocy technicznej Nexonia](https://nexonia.zendesk.com/hc/requests/new) Aby dodać użytkowników do platformy Nexonia.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="bf4a3-202">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf4a3-203">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf4a3-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf4a3-204">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Nexonia.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bf4a3-206">**Aby przypisać Simona Britta Nexonia, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf4a3-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="bf4a3-207">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bf4a3-209">Na liście aplikacji zaznacz **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-209">In the applications list, select **Nexonia**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="bf4a3-211">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bf4a3-213">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-213">Click **Add** button.</span></span> <span data-ttu-id="bf4a3-214">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bf4a3-216">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bf4a3-217">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf4a3-218">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf4a3-219">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf4a3-219">Testing single sign-on</span></span>

<span data-ttu-id="bf4a3-220">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bf4a3-221">Po kliknięciu kafelka Nexonia w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Nexonia.</span><span class="sxs-lookup"><span data-stu-id="bf4a3-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="bf4a3-222">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="bf4a3-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf4a3-223">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bf4a3-223">Additional resources</span></span>

* [<span data-ttu-id="bf4a3-224">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf4a3-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf4a3-225">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf4a3-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

