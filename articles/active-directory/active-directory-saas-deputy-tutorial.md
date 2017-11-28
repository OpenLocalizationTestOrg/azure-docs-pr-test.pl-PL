---
title: "Samouczek: Integracji Azure Active Directory z zastępcy | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i zastępcy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="b84d9-103">Samouczek: Integracji Azure Active Directory z zastępcy</span><span class="sxs-lookup"><span data-stu-id="b84d9-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="b84d9-104">Z tego samouczka dowiesz się integrowanie zastępcy w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b84d9-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b84d9-105">Integracja z usługą Azure AD zastępcy zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b84d9-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b84d9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do zastępcy</span><span class="sxs-lookup"><span data-stu-id="b84d9-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="b84d9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do zastępcy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b84d9-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b84d9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b84d9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b84d9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b84d9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b84d9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b84d9-110">Prerequisites</span></span>

<span data-ttu-id="b84d9-111">Aby skonfigurować integrację usługi Azure AD z zastępcy, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b84d9-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="b84d9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b84d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b84d9-113">Zastępcy logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b84d9-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b84d9-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b84d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b84d9-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b84d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b84d9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b84d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b84d9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b84d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b84d9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b84d9-118">Scenario description</span></span>
<span data-ttu-id="b84d9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b84d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b84d9-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b84d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b84d9-121">Dodawanie zastępcy z galerii</span><span class="sxs-lookup"><span data-stu-id="b84d9-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="b84d9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b84d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="b84d9-123">Dodawanie zastępcy z galerii</span><span class="sxs-lookup"><span data-stu-id="b84d9-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="b84d9-124">Aby skonfigurować integrację usługi Azure AD zastępcy, należy dodać zastępcy z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b84d9-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b84d9-125">**Aby dodać zastępcy z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b84d9-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d9-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b84d9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b84d9-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b84d9-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b84d9-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b84d9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b84d9-133">W polu wyszukiwania wpisz **zastępcy**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-133">In the search box, type **Deputy**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="b84d9-135">W panelu wyników wybierz **zastępcy**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="b84d9-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b84d9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b84d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b84d9-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zastępcy oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b84d9-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b84d9-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w zastępcy jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b84d9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="b84d9-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w zastępcy musi się.</span><span class="sxs-lookup"><span data-stu-id="b84d9-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="b84d9-141">W zastępcy, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="b84d9-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b84d9-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zastępcy, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="b84d9-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b84d9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b84d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b84d9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b84d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b84d9-145">**[Tworzenie użytkownika testowego zastępcy](#creating-a-deputy-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta zastępcy połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b84d9-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b84d9-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b84d9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b84d9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="b84d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b84d9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b84d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b84d9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji zastępcy.</span><span class="sxs-lookup"><span data-stu-id="b84d9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="b84d9-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z zastępcy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b84d9-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d9-151">W portalu Azure na **zastępcy** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b84d9-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="b84d9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="b84d9-155">Na **zastępcy domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="b84d9-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="b84d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="b84d9-157">a.</span></span> <span data-ttu-id="b84d9-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="b84d9-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="b84d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="b84d9-159">b.</span></span> <span data-ttu-id="b84d9-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="b84d9-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="b84d9-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="b84d9-162">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="b84d9-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="b84d9-164">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="b84d9-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="b84d9-165">Sufiks region zastępcy jest opcjonalne, lub go należy użyć jednej z tych: Australia | na | Europa | jako | la | af | | Australia Enterprise | Enterprise na | Enterprise eu | Enterprise — jako | Enterprise la | Enterprise af | usługi Enterprise</span><span class="sxs-lookup"><span data-stu-id="b84d9-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b84d9-166">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b84d9-166">These values are not real.</span></span> <span data-ttu-id="b84d9-167">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="b84d9-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b84d9-168">Skontaktuj się z [zespołem pomocy technicznej zastępcy](https://www.deputy.com/call-centers-customer-support-scheduling-software) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="b84d9-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="b84d9-169">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b84d9-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="b84d9-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b84d9-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="b84d9-173">Na **konfiguracji zastępcy** , kliknij przycisk **skonfigurować zastępcy** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b84d9-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b84d9-174">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b84d9-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="b84d9-176">Przejdź do następującego adresu URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="b84d9-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="b84d9-177">Przejdź do **ustawienia zabezpieczeń** i kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="b84d9-179">Na tym **ustawienia zabezpieczeń** wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="b84d9-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="b84d9-181">a.</span><span class="sxs-lookup"><span data-stu-id="b84d9-181">a.</span></span> <span data-ttu-id="b84d9-182">Włącz **społecznościowych logowania**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="b84d9-183">b.</span><span class="sxs-lookup"><span data-stu-id="b84d9-183">b.</span></span> <span data-ttu-id="b84d9-184">Otwórz z certyfikatu szyfrowania Base64 pobrany z portalu Azure w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu biblioteki OpenSSL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b84d9-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="b84d9-185">c.</span><span class="sxs-lookup"><span data-stu-id="b84d9-185">c.</span></span> <span data-ttu-id="b84d9-186">W polu tekstowym adres URL logowania jednokrotnego SAML wpisz`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="b84d9-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="b84d9-187">d.</span><span class="sxs-lookup"><span data-stu-id="b84d9-187">d.</span></span> <span data-ttu-id="b84d9-188">W polu tekstowym adres URL logowania jednokrotnego SAML Zastąp `<your subdomain>` z Twojej domeny podrzędnej.</span><span class="sxs-lookup"><span data-stu-id="b84d9-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="b84d9-189">e.</span><span class="sxs-lookup"><span data-stu-id="b84d9-189">e.</span></span> <span data-ttu-id="b84d9-190">W polu tekstowym adres URL logowania jednokrotnego SAML Zastąp `<saml sso url>` z **SAML pojedynczy znak na adres URL usługi** zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b84d9-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="b84d9-191">f.</span><span class="sxs-lookup"><span data-stu-id="b84d9-191">f.</span></span> <span data-ttu-id="b84d9-192">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="b84d9-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="b84d9-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b84d9-194">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="b84d9-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b84d9-195">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b84d9-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b84d9-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b84d9-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="b84d9-197">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b84d9-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b84d9-199">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b84d9-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d9-200">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b84d9-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b84d9-202">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b84d9-204">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b84d9-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b84d9-206">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b84d9-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b84d9-208">a.</span><span class="sxs-lookup"><span data-stu-id="b84d9-208">a.</span></span> <span data-ttu-id="b84d9-209">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b84d9-210">b.</span><span class="sxs-lookup"><span data-stu-id="b84d9-210">b.</span></span> <span data-ttu-id="b84d9-211">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b84d9-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b84d9-212">c.</span><span class="sxs-lookup"><span data-stu-id="b84d9-212">c.</span></span> <span data-ttu-id="b84d9-213">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b84d9-214">d.</span><span class="sxs-lookup"><span data-stu-id="b84d9-214">d.</span></span> <span data-ttu-id="b84d9-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="b84d9-216">Tworzenie użytkownika testowego zastępcy</span><span class="sxs-lookup"><span data-stu-id="b84d9-216">Creating a Deputy test user</span></span>

<span data-ttu-id="b84d9-217">Aby umożliwić użytkownikom usługi Azure AD zalogować się do zastępcy, muszą mieć przydzielone do zastępcy.</span><span class="sxs-lookup"><span data-stu-id="b84d9-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="b84d9-218">W przypadku zastępcy Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b84d9-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="b84d9-219">Aby udostępnić konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b84d9-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="b84d9-220">Zaloguj się do witryny firmy zastępcy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b84d9-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="b84d9-221">W okienku górnym menu nawigacyjnym kliknij **osób**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="b84d9-222">![Osoby](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "osób")</span><span class="sxs-lookup"><span data-stu-id="b84d9-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="b84d9-223">Kliknij przycisk **dodać osób** przycisk **dodać jedną osobę**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="b84d9-224">![Dodaj użytkowników](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Dodaj użytkowników")</span><span class="sxs-lookup"><span data-stu-id="b84d9-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="b84d9-225">Wykonaj poniższe czynności, a następnie kliknij przycisk **Zapisz & zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="b84d9-226">![Nowy użytkownik](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="b84d9-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="b84d9-227">a.</span><span class="sxs-lookup"><span data-stu-id="b84d9-227">a.</span></span> <span data-ttu-id="b84d9-228">W **nazwa** pole tekstowe, nazwa typu użytkownika, takich jak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="b84d9-229">b.</span><span class="sxs-lookup"><span data-stu-id="b84d9-229">b.</span></span> <span data-ttu-id="b84d9-230">W **E-mail** tekstowym, wpisz adres e-mail konta usługi Azure AD, aby udostępnić.</span><span class="sxs-lookup"><span data-stu-id="b84d9-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="b84d9-231">c.</span><span class="sxs-lookup"><span data-stu-id="b84d9-231">c.</span></span> <span data-ttu-id="b84d9-232">W **działania na** tekstowym, wpisz nazwę biznesowych.</span><span class="sxs-lookup"><span data-stu-id="b84d9-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="b84d9-233">d.</span><span class="sxs-lookup"><span data-stu-id="b84d9-233">d.</span></span> <span data-ttu-id="b84d9-234">Kliknij przycisk **Zapisz & zaprosić** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b84d9-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="b84d9-235">Właściciel konta usługi AAD otrzymuje wiadomość e-mail i następuje łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="b84d9-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="b84d9-236">Możesz użyć innych zastępcy użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez zastępcy do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="b84d9-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b84d9-237">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b84d9-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b84d9-238">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu zastępcy.</span><span class="sxs-lookup"><span data-stu-id="b84d9-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b84d9-240">**Aby przypisać Simona Britta zastępcy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b84d9-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d9-241">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b84d9-243">Na liście aplikacji zaznacz **zastępcy**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-243">In the applications list, select **Deputy**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="b84d9-245">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b84d9-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b84d9-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b84d9-247">Click **Add** button.</span></span> <span data-ttu-id="b84d9-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b84d9-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b84d9-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="b84d9-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b84d9-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b84d9-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b84d9-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b84d9-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b84d9-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b84d9-253">Testing single sign-on</span></span>

<span data-ttu-id="b84d9-254">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b84d9-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b84d9-255">Po kliknięciu kafelka zastępcy w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji zastępcy.</span><span class="sxs-lookup"><span data-stu-id="b84d9-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b84d9-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b84d9-256">Additional resources</span></span>

* [<span data-ttu-id="b84d9-257">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b84d9-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b84d9-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b84d9-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

