---
title: 'Samouczek: Integracji Azure Active Directory z O.C. Napisu Czarnecka - AppreciateHub | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i O.C. Napisu Czarnecka - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="1782b-105">Samouczek: Integracji Azure Active Directory z O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="1782b-106">Napisu Czarnecka - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="1782b-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="1782b-107">W tym samouczku opisano sposób integracji O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="1782b-108">Napisu Czarnecka - AppreciateHub z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1782b-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1782b-109">Integrowanie O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-109">Integrating O.C.</span></span> <span data-ttu-id="1782b-110">Napisu Czarnecka - AppreciateHub z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1782b-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1782b-111">Można kontrolować w usłudze Azure AD, który ma dostęp do O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="1782b-112">Napisu Czarnecka - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="1782b-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="1782b-113">Umożliwia użytkownikom automatycznie pobrać zalogowane do O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="1782b-114">Napisu Czarnecka - AppreciateHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1782b-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1782b-115">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1782b-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1782b-116">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1782b-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1782b-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1782b-117">Prerequisites</span></span>

<span data-ttu-id="1782b-118">Aby skonfigurować integrację usługi Azure AD z O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="1782b-119">Napisu Czarnecka - AppreciateHub, potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1782b-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="1782b-120">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1782b-120">An Azure AD subscription</span></span>
- <span data-ttu-id="1782b-121">O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-121">A O.C.</span></span> <span data-ttu-id="1782b-122">Napisu Czarnecka - AppreciateHub logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1782b-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1782b-123">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1782b-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1782b-124">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1782b-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1782b-125">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1782b-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1782b-126">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1782b-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1782b-127">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1782b-127">Scenario description</span></span>
<span data-ttu-id="1782b-128">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1782b-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1782b-129">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1782b-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1782b-130">Dodawanie O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-130">Adding O.C.</span></span> <span data-ttu-id="1782b-131">Napisu Czarnecka - AppreciateHub z galerii</span><span class="sxs-lookup"><span data-stu-id="1782b-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="1782b-132">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1782b-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="1782b-133">Dodawanie O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-133">Adding O.C.</span></span> <span data-ttu-id="1782b-134">Napisu Czarnecka - AppreciateHub z galerii</span><span class="sxs-lookup"><span data-stu-id="1782b-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="1782b-135">Aby skonfigurować integrację O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-135">To configure the integration of O.C.</span></span> <span data-ttu-id="1782b-136">Napisu Czarnecka - AppreciateHub do usługi Azure AD, należy dodać O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="1782b-137">Napisu Czarnecka - AppreciateHub z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1782b-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1782b-138">**Aby dodać O.C. Napisu Czarnecka - AppreciateHub z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1782b-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1782b-139">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1782b-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1782b-141">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1782b-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1782b-142">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1782b-142">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1782b-144">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1782b-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1782b-146">W polu wyszukiwania wpisz **O.C. Napisu Czarnecka - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="1782b-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="1782b-148">W panelu wyników wybierz **O.C. Napisu Czarnecka - AppreciateHub**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1782b-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1782b-150">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1782b-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1782b-151">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="1782b-152">Napisu Czarnecka - AppreciateHub w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="1782b-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1782b-153">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, jaki użytkownik odpowiednika w O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="1782b-154">Napisu Czarnecka - AppreciateHub jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1782b-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="1782b-155">Innymi słowy relacja linku między użytkownika usługi Azure AD i danemu użytkownikowi w O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="1782b-156">Napisu Czarnecka - AppreciateHub musi się.</span><span class="sxs-lookup"><span data-stu-id="1782b-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="1782b-157">W O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-157">In O.C.</span></span> <span data-ttu-id="1782b-158">Napisu Czarnecka - AppreciateHub, przypisz wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="1782b-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1782b-159">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="1782b-160">Napisu Czarnecka - AppreciateHub, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1782b-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1782b-161">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1782b-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1782b-162">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1782b-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1782b-163">**[Tworzenie O.C. Napisu Czarnecka - użytkownika testowego AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="1782b-164">Napisu Czarnecka - AppreciateHub połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1782b-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1782b-165">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1782b-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1782b-166">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1782b-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1782b-167">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1782b-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1782b-168">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w sieci O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="1782b-169">Napisu Czarnecka - AppreciateHub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1782b-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="1782b-170">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z O.C. Napisu Czarnecka - AppreciateHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1782b-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="1782b-171">W portalu Azure na **O.C. Napisu Czarnecka - AppreciateHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1782b-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1782b-173">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1782b-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="1782b-175">Na **O.C. Napisu Czarnecka - AppreciateHub domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1782b-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="1782b-177">a.</span><span class="sxs-lookup"><span data-stu-id="1782b-177">a.</span></span> <span data-ttu-id="1782b-178">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="1782b-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1782b-179">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1782b-179">This value is not real.</span></span> <span data-ttu-id="1782b-180">Zaktualizuj tę wartość przy rzeczywisty adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1782b-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="1782b-181">Skontaktuj się z [O.C. Napisu Czarnecka - zespołem pomocy technicznej AppreciateHub](mailto:sso@octanner.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="1782b-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="1782b-182">b.</span><span class="sxs-lookup"><span data-stu-id="1782b-182">b.</span></span> <span data-ttu-id="1782b-183">Otwórz plik metadanych, korzystając z następującego łącza: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="1782b-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="1782b-184">c.</span><span class="sxs-lookup"><span data-stu-id="1782b-184">c.</span></span> <span data-ttu-id="1782b-185">Zlokalizuj **md:AssertionConsumerService** węzła.</span><span class="sxs-lookup"><span data-stu-id="1782b-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="1782b-186">d.</span><span class="sxs-lookup"><span data-stu-id="1782b-186">d.</span></span> <span data-ttu-id="1782b-187">Skopiuj wartość **lokalizacji** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="1782b-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![Konfiguruj ustawienia aplikacji][12]
   
    <span data-ttu-id="1782b-189">e.</span><span class="sxs-lookup"><span data-stu-id="1782b-189">e.</span></span> <span data-ttu-id="1782b-190">W **na adres URL logowania** pole tekstowe poza wartości zostały uzyskane w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="1782b-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="1782b-191">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1782b-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="1782b-193">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1782b-193">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1782b-195">Aby skonfigurować logowanie jednokrotne w **O.C. Napisu Czarnecka - AppreciateHub** stronie, musisz wysłać pobrany **XML metadanych** do [O.C. Napisu Czarnecka - zespołem pomocy technicznej AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="1782b-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="1782b-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="1782b-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1782b-197">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="1782b-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1782b-198">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1782b-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1782b-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1782b-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="1782b-200">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1782b-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1782b-202">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1782b-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1782b-203">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1782b-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1782b-205">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1782b-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1782b-207">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1782b-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1782b-209">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1782b-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1782b-211">a.</span><span class="sxs-lookup"><span data-stu-id="1782b-211">a.</span></span> <span data-ttu-id="1782b-212">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1782b-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1782b-213">b.</span><span class="sxs-lookup"><span data-stu-id="1782b-213">b.</span></span> <span data-ttu-id="1782b-214">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1782b-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1782b-215">c.</span><span class="sxs-lookup"><span data-stu-id="1782b-215">c.</span></span> <span data-ttu-id="1782b-216">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1782b-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1782b-217">d.</span><span class="sxs-lookup"><span data-stu-id="1782b-217">d.</span></span> <span data-ttu-id="1782b-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1782b-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="1782b-219">Tworzenie O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-219">Creating a O.C.</span></span> <span data-ttu-id="1782b-220">Napisu Czarnecka - AppreciateHub użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="1782b-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="1782b-221">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="1782b-222">Napisu Czarnecka - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="1782b-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="1782b-223">**Aby utworzyć użytkownika o nazwie Simona Britta w O.C. Napisu Czarnecka - AppreciateHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1782b-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="1782b-224">Skontaktuj się z [O.C. Napisu Czarnecka - zespołem pomocy technicznej AppreciateHub](mailto:sso@octanner.com) można utworzyć użytkownika, który ma atrybut nameID taką samą wartość jak nazwa użytkownika Simona Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1782b-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1782b-225">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1782b-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1782b-226">W tej sekcji Włącz Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="1782b-227">Napisu Czarnecka - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="1782b-227">Tanner - AppreciateHub.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1782b-229">**Aby przypisać Simona Britta O.C. Napisu Czarnecka - AppreciateHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1782b-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="1782b-230">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1782b-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1782b-232">Na liście aplikacji zaznacz **O.C. Napisu Czarnecka - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="1782b-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="1782b-234">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1782b-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1782b-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1782b-236">Click **Add** button.</span></span> <span data-ttu-id="1782b-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1782b-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1782b-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1782b-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1782b-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1782b-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1782b-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1782b-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1782b-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1782b-242">Testing single sign-on</span></span>

<span data-ttu-id="1782b-243">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1782b-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="1782b-244">Po kliknięciu O.C.</span><span class="sxs-lookup"><span data-stu-id="1782b-244">When you click the O.C.</span></span> <span data-ttu-id="1782b-245">Napisu Czarnecka - AppreciateHub kafelka w panelu dostępu użytkownik powinien uzyskać automatycznie podpisany w przypadku O.C. Twojego</span><span class="sxs-lookup"><span data-stu-id="1782b-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="1782b-246">Napisu Czarnecka - AppreciateHub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1782b-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1782b-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1782b-247">Additional resources</span></span>

* [<span data-ttu-id="1782b-248">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1782b-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1782b-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1782b-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

