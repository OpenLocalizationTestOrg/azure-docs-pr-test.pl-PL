---
title: 'Samouczek: Integracji Azure Active Directory z Strona stanu | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Strona stanu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="6f252-103">Samouczek: Integracji Azure Active Directory z Strona stanu</span><span class="sxs-lookup"><span data-stu-id="6f252-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="6f252-104">Z tego samouczka dowiesz się integrowanie Strona stanu w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f252-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f252-105">Integrowanie Strona stanu z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6f252-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6f252-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Strona stanu</span><span class="sxs-lookup"><span data-stu-id="6f252-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="6f252-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Strona stanu (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f252-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f252-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6f252-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6f252-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f252-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f252-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6f252-110">Prerequisites</span></span>

<span data-ttu-id="6f252-111">Aby skonfigurować integrację usługi Azure AD z Strona stanu, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6f252-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="6f252-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f252-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f252-113">Strona stanu logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6f252-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f252-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6f252-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f252-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6f252-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f252-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6f252-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f252-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f252-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f252-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6f252-118">Scenario description</span></span>
<span data-ttu-id="6f252-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6f252-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f252-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6f252-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f252-121">Strona Dodawanie stanu z galerii</span><span class="sxs-lookup"><span data-stu-id="6f252-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="6f252-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6f252-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="6f252-123">Strona Dodawanie stanu z galerii</span><span class="sxs-lookup"><span data-stu-id="6f252-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="6f252-124">Aby skonfigurować integrację usługi Azure AD Strona stanu, należy dodać Strona stanu z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6f252-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6f252-125">**Aby dodać Strona stanu z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6f252-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6f252-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6f252-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6f252-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6f252-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6f252-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6f252-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6f252-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6f252-133">W polu wyszukiwania wpisz **Strona stanu**.</span><span class="sxs-lookup"><span data-stu-id="6f252-133">In the search box, type **StatusPage**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="6f252-135">W panelu wyników wybierz **Strona stanu**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6f252-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f252-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6f252-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f252-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Strona stanu w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f252-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Strona stanu jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f252-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="6f252-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Strona stanu.</span><span class="sxs-lookup"><span data-stu-id="6f252-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="6f252-141">Strona stanu, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="6f252-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6f252-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Strona stanu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6f252-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6f252-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6f252-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6f252-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6f252-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f252-145">**[Tworzenie użytkownika testowego Strona stanu](#creating-a-statuspage-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Strona stanu powiązaną z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f252-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f252-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6f252-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f252-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6f252-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f252-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6f252-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f252-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji strona stanu.</span><span class="sxs-lookup"><span data-stu-id="6f252-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="6f252-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Strona stanu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6f252-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="6f252-151">W portalu Azure na **Strona stanu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6f252-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6f252-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6f252-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="6f252-155">Na **domeny Strona stanu i adresów URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f252-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="6f252-157">a.</span><span class="sxs-lookup"><span data-stu-id="6f252-157">a.</span></span> <span data-ttu-id="6f252-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="6f252-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="6f252-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f252-159">b.</span></span> <span data-ttu-id="6f252-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="6f252-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="6f252-161">Skontaktuj się z zespołem pomocy technicznej Strona stanu na [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)żądania metadanych niezbędnych do skonfigurowania rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6f252-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="6f252-162">a.</span><span class="sxs-lookup"><span data-stu-id="6f252-162">a.</span></span> <span data-ttu-id="6f252-163">Metadane, skopiuj wartości wystawcy, a następnie wklej go do **identyfikator** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="6f252-164">b.</span><span class="sxs-lookup"><span data-stu-id="6f252-164">b.</span></span> <span data-ttu-id="6f252-165">Z metadanych, skopiuj adres URL odpowiedzi, a następnie wklej go do **adres URL odpowiedzi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="6f252-166">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6f252-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="6f252-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6f252-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f252-170">Na **Strona stanu konfiguracji** kliknij **strona Konfigurowanie stanu** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6f252-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6f252-171">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6f252-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="6f252-173">W innym oknie przeglądarki należy zalogować się jako administrator do witryny firmy Strona stanu.</span><span class="sxs-lookup"><span data-stu-id="6f252-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="6f252-174">Na głównym pasku narzędzi, kliknij przycisk **Zarządzaj kontem**.</span><span class="sxs-lookup"><span data-stu-id="6f252-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="6f252-176">Kliknij przycisk **rejestracji jednokrotnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="6f252-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="6f252-178">Na stronie Ustawienia logowania jednokrotnego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f252-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="6f252-181">a.</span><span class="sxs-lookup"><span data-stu-id="6f252-181">a.</span></span> <span data-ttu-id="6f252-182">W **logowania jednokrotnego, docelowy adres URL** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6f252-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6f252-183">b.</span><span class="sxs-lookup"><span data-stu-id="6f252-183">b.</span></span> <span data-ttu-id="6f252-184">Otwórz w Notatniku pobranego certyfikatu, skopiuj zawartość, a następnie wklej go do **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="6f252-185">c.</span><span class="sxs-lookup"><span data-stu-id="6f252-185">c.</span></span> <span data-ttu-id="6f252-186">Kliknij przycisk **Zapisywanie konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="6f252-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="6f252-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6f252-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6f252-188">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6f252-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6f252-189">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f252-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f252-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f252-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f252-191">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6f252-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6f252-193">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6f252-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6f252-194">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6f252-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f252-196">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6f252-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f252-198">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f252-200">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f252-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f252-202">a.</span><span class="sxs-lookup"><span data-stu-id="6f252-202">a.</span></span> <span data-ttu-id="6f252-203">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f252-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f252-204">b.</span><span class="sxs-lookup"><span data-stu-id="6f252-204">b.</span></span> <span data-ttu-id="6f252-205">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f252-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f252-206">c.</span><span class="sxs-lookup"><span data-stu-id="6f252-206">c.</span></span> <span data-ttu-id="6f252-207">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6f252-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6f252-208">d.</span><span class="sxs-lookup"><span data-stu-id="6f252-208">d.</span></span> <span data-ttu-id="6f252-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6f252-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="6f252-210">Tworzenie użytkownika testowego Strona stanu</span><span class="sxs-lookup"><span data-stu-id="6f252-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="6f252-211">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Strona stanu.</span><span class="sxs-lookup"><span data-stu-id="6f252-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="6f252-212">Strona stanu obsługę w czasie.</span><span class="sxs-lookup"><span data-stu-id="6f252-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="6f252-213">Została już włączona w [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="6f252-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="6f252-214">**Aby utworzyć użytkownika o nazwie Simona Britta w Strona stanu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6f252-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="6f252-215">Logowanie do witryny firmy Strona stanu jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6f252-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="6f252-216">W menu u góry kliknij **Zarządzaj kontem**.</span><span class="sxs-lookup"><span data-stu-id="6f252-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="6f252-218">Kliknij przycisk **członków zespołu** kartę.</span><span class="sxs-lookup"><span data-stu-id="6f252-218">Click the **Team Members** tab.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="6f252-220">Kliknij przycisk **członek zespołu Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6f252-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="6f252-222">Typ **adres E-mail**, **imię**, i **nazwisko** z prawidłowym użytkownikiem ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="6f252-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="6f252-224">Jako **roli**, wybierz **Administrator klienta**.</span><span class="sxs-lookup"><span data-stu-id="6f252-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="6f252-225">Kliknij przycisk **Utwórz konto**.</span><span class="sxs-lookup"><span data-stu-id="6f252-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6f252-226">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f252-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6f252-227">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Strona stanu.</span><span class="sxs-lookup"><span data-stu-id="6f252-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6f252-229">**Aby przypisać Simona Britta Strona stanu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6f252-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="6f252-230">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6f252-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6f252-232">Na liście aplikacji zaznacz **Strona stanu**.</span><span class="sxs-lookup"><span data-stu-id="6f252-232">In the applications list, select **StatusPage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="6f252-234">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6f252-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6f252-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6f252-236">Click **Add** button.</span></span> <span data-ttu-id="6f252-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6f252-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6f252-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6f252-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f252-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6f252-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f252-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6f252-242">Testing single sign-on</span></span>

<span data-ttu-id="6f252-243">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6f252-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6f252-244">Po kliknięciu kafelka Strona stanu w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Strona stanu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f252-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f252-245">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6f252-245">Additional resources</span></span>

* [<span data-ttu-id="6f252-246">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f252-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f252-247">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6f252-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

