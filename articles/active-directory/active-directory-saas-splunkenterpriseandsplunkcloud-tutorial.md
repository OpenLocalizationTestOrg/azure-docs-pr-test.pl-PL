---
title: "Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługi Azure Active Directory i Splunk Enterprise i Splunk chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 181d0f33245f0811c15c1e7945c797502ef71eba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="97429-103">Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk</span><span class="sxs-lookup"><span data-stu-id="97429-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="97429-104">Z tego samouczka dowiesz integrowanie Splunk przedsiębiorstwa i w chmurze Splunk z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97429-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97429-105">Integracja z usługą Azure AD Splunk przedsiębiorstwa i w chmurze Splunk zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="97429-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="97429-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Splunk przedsiębiorstwa i w chmurze Splunk</span><span class="sxs-lookup"><span data-stu-id="97429-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="97429-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Splunk przedsiębiorstwa i w chmurze Splunk (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97429-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97429-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="97429-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="97429-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97429-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97429-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97429-110">Prerequisites</span></span>

<span data-ttu-id="97429-111">Aby skonfigurować integrację usługi Azure AD z Splunk przedsiębiorstwa i w chmurze Splunk, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="97429-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="97429-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97429-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97429-113">Splunk Enterprise i w chmurze Splunk jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="97429-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97429-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="97429-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97429-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="97429-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97429-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="97429-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97429-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97429-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97429-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="97429-118">Scenario description</span></span>
<span data-ttu-id="97429-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="97429-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97429-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="97429-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97429-121">Dodawanie Splunk przedsiębiorstwa i w chmurze Splunk z galerii</span><span class="sxs-lookup"><span data-stu-id="97429-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="97429-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97429-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="97429-123">Dodawanie Splunk przedsiębiorstwa i w chmurze Splunk z galerii</span><span class="sxs-lookup"><span data-stu-id="97429-123">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="97429-124">Aby skonfigurować integrację Splunk przedsiębiorstwa i Splunk chmury do usługi Azure AD, należy dodać Splunk przedsiębiorstwa i w chmurze Splunk z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="97429-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97429-125">**Aby dodać Splunk przedsiębiorstwa i w chmurze Splunk z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97429-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97429-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97429-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="97429-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="97429-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="97429-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97429-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="97429-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97429-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="97429-133">W polu wyszukiwania wpisz **Splunk przedsiębiorstwa i w chmurze Splunk**.</span><span class="sxs-lookup"><span data-stu-id="97429-133">In the search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="97429-135">W panelu wyników wybierz **Splunk przedsiębiorstwa i w chmurze Splunk**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="97429-135">In the results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97429-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97429-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97429-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="97429-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97429-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Splunk przedsiębiorstwa i w chmurze Splunk jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97429-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="97429-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w organizacji Splunk i w chmurze Splunk musi się.</span><span class="sxs-lookup"><span data-stu-id="97429-140">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="97429-141">Splunk Enterprise i w chmurze Splunk przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="97429-141">In Splunk Enterprise and Splunk Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="97429-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i w chmurze Splunk, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="97429-142">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97429-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="97429-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="97429-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="97429-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97429-145">**[Tworzenie użytkownika testowego Splunk przedsiębiorstwa i w chmurze Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  — mają odpowiednika Simona Britta w przedsiębiorstwie Splunk i Splunk chmurze, która jest połączona z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97429-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="97429-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="97429-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97429-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="97429-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97429-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97429-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97429-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w Splunk przedsiębiorstwa i w chmurze Splunk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97429-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="97429-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97429-150">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="97429-151">W portalu Azure na **Splunk przedsiębiorstwa i w chmurze Splunk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="97429-151">In the Azure portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="97429-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="97429-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="97429-155">Na **Splunk przedsiębiorstwa i adresy URL i domenę chmury Splunk** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="97429-155">On the **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="97429-157">a.</span><span class="sxs-lookup"><span data-stu-id="97429-157">a.</span></span> <span data-ttu-id="97429-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="97429-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="97429-159">b.</span><span class="sxs-lookup"><span data-stu-id="97429-159">b.</span></span> <span data-ttu-id="97429-160">W **identyfikator** tekstowym, wpisz adres URL serwera Splunk.</span><span class="sxs-lookup"><span data-stu-id="97429-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>

    <span data-ttu-id="97429-161">c.</span><span class="sxs-lookup"><span data-stu-id="97429-161">c.</span></span> <span data-ttu-id="97429-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="97429-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97429-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="97429-163">These values are not real.</span></span> <span data-ttu-id="97429-164">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="97429-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="97429-165">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="97429-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="97429-166">Skontaktuj się z [Splunk Enterprise i Splunk chmury klienta obsługuje zespołu](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="97429-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to get these values.</span></span> 

4. <span data-ttu-id="97429-167">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="97429-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="97429-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97429-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="97429-171">Skonfigurować logowanie jednokrotne w **Splunk przedsiębiorstwa i w chmurze Splunk** stronie, musisz wysłać pobrany **XML metadanych** do [Splunk przedsiębiorstwa i w chmurze Splunk obsługuje zespołu](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="97429-171">To configure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need to send the downloaded **Metadata XML** to [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="97429-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="97429-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="97429-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="97429-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="97429-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97429-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97429-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97429-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="97429-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="97429-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="97429-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97429-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97429-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97429-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97429-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="97429-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97429-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97429-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97429-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="97429-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97429-187">a.</span><span class="sxs-lookup"><span data-stu-id="97429-187">a.</span></span> <span data-ttu-id="97429-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97429-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97429-189">b.</span><span class="sxs-lookup"><span data-stu-id="97429-189">b.</span></span> <span data-ttu-id="97429-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97429-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97429-191">c.</span><span class="sxs-lookup"><span data-stu-id="97429-191">c.</span></span> <span data-ttu-id="97429-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="97429-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="97429-193">d.</span><span class="sxs-lookup"><span data-stu-id="97429-193">d.</span></span> <span data-ttu-id="97429-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="97429-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="97429-195">Tworzenie użytkownika testowego Splunk Enterprise i Splunk chmury</span><span class="sxs-lookup"><span data-stu-id="97429-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="97429-196">W tej sekcji utworzysz użytkownika o nazwie Simona Britta w przedsiębiorstwie Splunk i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="97429-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="97429-197">Praca z [Splunk przedsiębiorstwa i w chmurze Splunk obsługuje zespołu](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) Aby dodać użytkowników na platformie Splunk przedsiębiorstwa i w chmurze Splunk.</span><span class="sxs-lookup"><span data-stu-id="97429-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="97429-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97429-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="97429-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Splunk przedsiębiorstwa i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="97429-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Splunk Enterprise and Splunk Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="97429-201">**Aby przypisać Simona Britta do Splunk przedsiębiorstwa i Splunk chmury, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97429-201">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="97429-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97429-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="97429-204">Na liście aplikacji zaznacz **Splunk przedsiębiorstwa i w chmurze Splunk**.</span><span class="sxs-lookup"><span data-stu-id="97429-204">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="97429-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="97429-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="97429-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97429-208">Click **Add** button.</span></span> <span data-ttu-id="97429-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97429-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="97429-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="97429-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="97429-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97429-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97429-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97429-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97429-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97429-214">Testing single sign-on</span></span>

<span data-ttu-id="97429-215">W tej sekcji można przetestować programu Azure AD SSOonfiguration, za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="97429-215">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="97429-216">Po kliknięciu Splunk Enterprise i chmury Splunk kafelka w panelu dostępu, możesz należy pobrać automatycznie zalogowane Splunk przedsiębiorstwa i w chmurze Splunk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97429-216">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97429-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="97429-217">Additional resources</span></span>

* [<span data-ttu-id="97429-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97429-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97429-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97429-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

