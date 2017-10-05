---
title: 'Samouczek: Integracji Azure Active Directory z Agile analiz biznesowych Birst | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Birst Agile analiz biznesowych."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 779f9e0a57ffb2274ea22a90ed9759734ab6916d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="abaf8-103">Samouczek: Integracji Azure Active Directory z Birst Agile analiz biznesowych</span><span class="sxs-lookup"><span data-stu-id="abaf8-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="abaf8-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="abaf8-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="abaf8-105">Integrowanie Birst Agile analiz biznesowych z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="abaf8-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="abaf8-106">Można kontrolować w usłudze Azure AD, który ma dostęp do analiz biznesowych Agile Birst</span><span class="sxs-lookup"><span data-stu-id="abaf8-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="abaf8-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Birst Agile analiz biznesowych (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="abaf8-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="abaf8-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="abaf8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="abaf8-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="abaf8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abaf8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="abaf8-110">Prerequisites</span></span>

<span data-ttu-id="abaf8-111">Aby skonfigurować integrację usługi Azure AD z Birst Agile analiz biznesowych, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="abaf8-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="abaf8-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="abaf8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="abaf8-113">Elastyczne analiz biznesowych Birst jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="abaf8-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="abaf8-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="abaf8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="abaf8-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="abaf8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="abaf8-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="abaf8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="abaf8-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="abaf8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="abaf8-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="abaf8-118">Scenario description</span></span>
<span data-ttu-id="abaf8-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="abaf8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="abaf8-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="abaf8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="abaf8-121">Dodawanie Birst Agile analiz biznesowych z galerii</span><span class="sxs-lookup"><span data-stu-id="abaf8-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="abaf8-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="abaf8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="abaf8-123">Dodawanie Birst Agile analiz biznesowych z galerii</span><span class="sxs-lookup"><span data-stu-id="abaf8-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="abaf8-124">Aby skonfigurować integrację usługi Azure AD Birst Agile analiz biznesowych, należy dodać Birst Agile analiz biznesowych z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="abaf8-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="abaf8-125">**Aby dodać Birst Agile analiz biznesowych z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="abaf8-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="abaf8-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="abaf8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="abaf8-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="abaf8-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="abaf8-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="abaf8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="abaf8-133">W polu wyszukiwania wpisz **Birst Agile analiz biznesowych**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="abaf8-135">W panelu wyników wybierz **Birst Agile analiz biznesowych**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="abaf8-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="abaf8-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="abaf8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="abaf8-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Birst Agile analiz biznesowych na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="abaf8-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="abaf8-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w Birst Agile analiz biznesowych do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abaf8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="abaf8-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="abaf8-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="abaf8-141">W Birst Agile analiz biznesowych, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="abaf8-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="abaf8-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Birst Agile analiz biznesowych, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="abaf8-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="abaf8-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="abaf8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="abaf8-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="abaf8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="abaf8-145">**[Tworzenie użytkownika testowego analiz biznesowych Agile Birst](#creating-a-birst-agile-business-analytics-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Birst Agile analiz biznesowych połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="abaf8-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="abaf8-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="abaf8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="abaf8-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="abaf8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="abaf8-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="abaf8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="abaf8-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="abaf8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="abaf8-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Birst Agile analiz biznesowych, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="abaf8-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="abaf8-151">W portalu Azure na **Birst Agile analiz biznesowych** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="abaf8-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="abaf8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="abaf8-155">Na **Birst Agile domeny analizy biznesowej i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="abaf8-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="abaf8-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="abaf8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="abaf8-158">Adres URL jest zależna od centrum danych znajduje się konto Birst:</span><span class="sxs-lookup"><span data-stu-id="abaf8-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="abaf8-159">Do użytku w USA centrum danych zgodnie ze wzorcem:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="abaf8-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="abaf8-160">Dla Europy centrum danych, użyj następującego wzorca:`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="abaf8-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="abaf8-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="abaf8-161">This value is not real.</span></span> <span data-ttu-id="abaf8-162">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="abaf8-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="abaf8-163">Skontaktuj się z [zespołem pomocy technicznej klienta analizy biznesowej Agile Birst](mailto:info@birst.com) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="abaf8-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
4. <span data-ttu-id="abaf8-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="abaf8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="abaf8-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="abaf8-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="abaf8-168">Na **Birst Agile konfiguracji analizy biznesowej** , kliknij przycisk **skonfigurować Birst Agile analiz biznesowych** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="abaf8-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="abaf8-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="abaf8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="abaf8-171">Skonfigurować logowanie jednokrotne w **Birst Agile analiz biznesowych** stronie, musisz wysłać pobrany **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [Birst Agile analiz biznesowych obsługuje zespołu](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="abaf8-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="abaf8-172">Wspomina do zespołu Birst, że ta integracja wymaga algorytm SHA256 (SHA1 nie będzie obsługiwana) tak, aby ich ustawiona SSO na odpowiedni serwer, takich jak **app2101** itp.</span><span class="sxs-lookup"><span data-stu-id="abaf8-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="abaf8-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="abaf8-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="abaf8-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="abaf8-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="abaf8-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="abaf8-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="abaf8-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="abaf8-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="abaf8-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="abaf8-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="abaf8-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="abaf8-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="abaf8-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="abaf8-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="abaf8-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="abaf8-184">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="abaf8-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="abaf8-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="abaf8-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="abaf8-188">a.</span><span class="sxs-lookup"><span data-stu-id="abaf8-188">a.</span></span> <span data-ttu-id="abaf8-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="abaf8-190">b.</span><span class="sxs-lookup"><span data-stu-id="abaf8-190">b.</span></span> <span data-ttu-id="abaf8-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="abaf8-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="abaf8-192">c.</span><span class="sxs-lookup"><span data-stu-id="abaf8-192">c.</span></span> <span data-ttu-id="abaf8-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="abaf8-194">d.</span><span class="sxs-lookup"><span data-stu-id="abaf8-194">d.</span></span> <span data-ttu-id="abaf8-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="abaf8-196">Tworzenie użytkownika testowego Birst Agile analityka biznesowa</span><span class="sxs-lookup"><span data-stu-id="abaf8-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="abaf8-197">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="abaf8-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="abaf8-198">Praca z [Birst Agile analiz biznesowych obsługuje zespołu](mailto:info@birst.com) Aby dodać użytkowników w ramach konta Birst.</span><span class="sxs-lookup"><span data-stu-id="abaf8-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="abaf8-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="abaf8-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="abaf8-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="abaf8-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="abaf8-202">**Aby przypisać Simona Britta Birst Agile analiz biznesowych, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="abaf8-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="abaf8-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="abaf8-205">Na liście aplikacji zaznacz **Birst Agile analiz biznesowych**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="abaf8-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="abaf8-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="abaf8-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="abaf8-209">Click **Add** button.</span></span> <span data-ttu-id="abaf8-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="abaf8-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="abaf8-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="abaf8-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="abaf8-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="abaf8-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="abaf8-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="abaf8-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="abaf8-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="abaf8-215">Testing single sign-on</span></span>

<span data-ttu-id="abaf8-216">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="abaf8-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="abaf8-217">Po kliknięciu kafelka Birst Agile analiz biznesowych w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="abaf8-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="abaf8-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="abaf8-218">Additional resources</span></span>

* [<span data-ttu-id="abaf8-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="abaf8-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="abaf8-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="abaf8-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

