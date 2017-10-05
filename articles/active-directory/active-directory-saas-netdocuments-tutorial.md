---
title: 'Samouczek: Integracji Azure Active Directory z NetDocuments | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="5fcde-103">Samouczek: Integracji Azure Active Directory z NetDocuments</span><span class="sxs-lookup"><span data-stu-id="5fcde-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="5fcde-104">Z tego samouczka dowiesz się integrowanie NetDocuments z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fcde-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fcde-105">Integracja z usługą Azure AD NetDocuments zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5fcde-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5fcde-106">Można kontrolować w usłudze Azure AD, który ma dostęp do NetDocuments</span><span class="sxs-lookup"><span data-stu-id="5fcde-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="5fcde-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do NetDocuments (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fcde-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5fcde-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5fcde-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5fcde-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fcde-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fcde-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5fcde-110">Prerequisites</span></span>

<span data-ttu-id="5fcde-111">Aby skonfigurować integrację usługi Azure AD z NetDocuments, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5fcde-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="5fcde-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fcde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fcde-113">NetDocuments logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5fcde-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fcde-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5fcde-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fcde-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5fcde-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fcde-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5fcde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fcde-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fcde-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fcde-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5fcde-118">Scenario description</span></span>
<span data-ttu-id="5fcde-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5fcde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fcde-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5fcde-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fcde-121">Dodawanie NetDocuments z galerii</span><span class="sxs-lookup"><span data-stu-id="5fcde-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="5fcde-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5fcde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="5fcde-123">Dodawanie NetDocuments z galerii</span><span class="sxs-lookup"><span data-stu-id="5fcde-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="5fcde-124">Aby skonfigurować integrację usługi Azure AD NetDocuments, należy dodać NetDocuments z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5fcde-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5fcde-125">**Aby dodać NetDocuments z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5fcde-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5fcde-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5fcde-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5fcde-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5fcde-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5fcde-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fcde-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5fcde-133">W polu wyszukiwania wpisz **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-133">In the search box, type **NetDocuments**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="5fcde-135">W panelu wyników wybierz **NetDocuments**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5fcde-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5fcde-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5fcde-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5fcde-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z NetDocuments w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5fcde-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fcde-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w NetDocuments jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fcde-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="5fcde-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w NetDocuments musi się.</span><span class="sxs-lookup"><span data-stu-id="5fcde-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="5fcde-141">W NetDocuments, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5fcde-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5fcde-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z NetDocuments, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5fcde-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5fcde-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5fcde-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5fcde-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5fcde-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fcde-145">**[Tworzenie użytkownika testowego NetDocuments](#creating-a-netdocuments-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta NetDocuments połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5fcde-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fcde-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5fcde-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fcde-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5fcde-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5fcde-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5fcde-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5fcde-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="5fcde-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="5fcde-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z NetDocuments, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5fcde-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="5fcde-151">W portalu Azure na **NetDocuments** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5fcde-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5fcde-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="5fcde-155">Na **NetDocuments domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5fcde-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="5fcde-157">a.</span><span class="sxs-lookup"><span data-stu-id="5fcde-157">a.</span></span> <span data-ttu-id="5fcde-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="5fcde-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="5fcde-159">b.</span><span class="sxs-lookup"><span data-stu-id="5fcde-159">b.</span></span> <span data-ttu-id="5fcde-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="5fcde-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fcde-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5fcde-161">These values are not real.</span></span> <span data-ttu-id="5fcde-162">Rzeczywisty adres URL logowania i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5fcde-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="5fcde-163">Skontaktuj się z [NetDocuments obsługuje zespołu](https://support.netdocuments.com/hc/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="5fcde-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="5fcde-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5fcde-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="5fcde-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fcde-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fcde-168">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy NetDocuments jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5fcde-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="5fcde-169">Przejdź do **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="5fcde-170">Kliknij przycisk **Dodawanie i usuwanie użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="5fcde-171">![Repozytorium](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "repozytorium")</span><span class="sxs-lookup"><span data-stu-id="5fcde-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="5fcde-172">Kliknij przycisk **skonfiguruj zaawansowane opcje uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="5fcde-173">![Skonfiguruj zaawansowane opcje uwierzytelniania](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "skonfiguruj zaawansowane opcje uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="5fcde-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="5fcde-174">Na **tożsamości federacyjnych** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5fcde-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="5fcde-175">![Federacyjna Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "federacyjnych Identitty")</span><span class="sxs-lookup"><span data-stu-id="5fcde-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="5fcde-176">a.</span><span class="sxs-lookup"><span data-stu-id="5fcde-176">a.</span></span> <span data-ttu-id="5fcde-177">Jako **typ serwera tożsamości federacyjnych**, wybierz pozycję **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="5fcde-178">b.</span><span class="sxs-lookup"><span data-stu-id="5fcde-178">b.</span></span> <span data-ttu-id="5fcde-179">Kliknij przycisk **wybierz plik**, aby przekazać plik metadanych pobranych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fcde-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="5fcde-180">c.</span><span class="sxs-lookup"><span data-stu-id="5fcde-180">c.</span></span> <span data-ttu-id="5fcde-181">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="5fcde-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5fcde-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5fcde-183">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5fcde-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5fcde-184">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fcde-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5fcde-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fcde-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="5fcde-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5fcde-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5fcde-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5fcde-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5fcde-189">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5fcde-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5fcde-191">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5fcde-193">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fcde-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5fcde-195">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5fcde-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5fcde-197">a.</span><span class="sxs-lookup"><span data-stu-id="5fcde-197">a.</span></span> <span data-ttu-id="5fcde-198">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fcde-199">b.</span><span class="sxs-lookup"><span data-stu-id="5fcde-199">b.</span></span> <span data-ttu-id="5fcde-200">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5fcde-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5fcde-201">c.</span><span class="sxs-lookup"><span data-stu-id="5fcde-201">c.</span></span> <span data-ttu-id="5fcde-202">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5fcde-203">d.</span><span class="sxs-lookup"><span data-stu-id="5fcde-203">d.</span></span> <span data-ttu-id="5fcde-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="5fcde-205">Tworzenie użytkownika testowego NetDocuments</span><span class="sxs-lookup"><span data-stu-id="5fcde-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="5fcde-206">Aby umożliwić użytkownikom usługi Azure AD zalogować się do NetDocuments, musi być przygotowana do NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="5fcde-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="5fcde-207">W przypadku NetDocuments Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5fcde-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="5fcde-208">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5fcde-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5fcde-209">SING do Twojej **NetDocuments** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5fcde-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="5fcde-210">W menu u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="5fcde-211">![Administrator](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="5fcde-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="5fcde-212">Kliknij przycisk **Dodawanie i usuwanie użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="5fcde-213">![Repozytorium](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "repozytorium")</span><span class="sxs-lookup"><span data-stu-id="5fcde-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="5fcde-214">W **adres E-mail** tekstowym, wpisz adres e-mail prawidłowe konto usługi Azure Active Directory, aby udostępnić, a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="5fcde-215">![Adres e-mail](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "adres E-mail")</span><span class="sxs-lookup"><span data-stu-id="5fcde-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5fcde-216">Właściciel konta usługi Azure Active Directory otrzyma wiadomość e-mail zawierającą łącze do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="5fcde-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="5fcde-217">Możesz użyć innych NetDocuments użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez NetDocuments do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5fcde-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5fcde-218">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fcde-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5fcde-219">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="5fcde-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5fcde-221">**Aby przypisać Simona Britta NetDocuments, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5fcde-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="5fcde-222">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5fcde-224">Na liście aplikacji zaznacz **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-224">In the applications list, select **NetDocuments**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="5fcde-226">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5fcde-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5fcde-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fcde-228">Click **Add** button.</span></span> <span data-ttu-id="5fcde-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fcde-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5fcde-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5fcde-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5fcde-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fcde-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fcde-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fcde-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5fcde-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5fcde-234">Testing single sign-on</span></span>

<span data-ttu-id="5fcde-235">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fcde-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5fcde-236">Po kliknięciu kafelka NetDocuments w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="5fcde-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="5fcde-237">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5fcde-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5fcde-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5fcde-238">Additional resources</span></span>

* [<span data-ttu-id="5fcde-239">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fcde-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fcde-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fcde-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

