---
title: 'Samouczek: Integracji Azure Active Directory z cieplarnianych | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i cieplarnianych."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: d3aba4aab8ded8749db2bf8197f57a6763008c60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="485fa-103">Samouczek: Integracji Azure Active Directory z cieplarnianych</span><span class="sxs-lookup"><span data-stu-id="485fa-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="485fa-104">Z tego samouczka dowiesz się integrowanie cieplarnianych w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="485fa-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="485fa-105">Integracja z usługą Azure AD cieplarnianych zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="485fa-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="485fa-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do cieplarnianych.</span><span class="sxs-lookup"><span data-stu-id="485fa-106">You can control in Azure AD who has access to Greenhouse.</span></span>
- <span data-ttu-id="485fa-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do cieplarnianych (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="485fa-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="485fa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="485fa-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="485fa-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="485fa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="485fa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="485fa-110">Prerequisites</span></span>

<span data-ttu-id="485fa-111">Aby skonfigurować integrację usługi Azure AD z cieplarnianych, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="485fa-111">To configure Azure AD integration with Greenhouse, you need the following items:</span></span>

- <span data-ttu-id="485fa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="485fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="485fa-113">Cieplarnianych logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="485fa-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="485fa-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="485fa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="485fa-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="485fa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="485fa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="485fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="485fa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="485fa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="485fa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="485fa-118">Scenario description</span></span>
<span data-ttu-id="485fa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="485fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="485fa-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="485fa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="485fa-121">Dodawanie cieplarnianych z galerii</span><span class="sxs-lookup"><span data-stu-id="485fa-121">Adding Greenhouse from the gallery</span></span>
2. <span data-ttu-id="485fa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="485fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-the-gallery"></a><span data-ttu-id="485fa-123">Dodawanie cieplarnianych z galerii</span><span class="sxs-lookup"><span data-stu-id="485fa-123">Adding Greenhouse from the gallery</span></span>
<span data-ttu-id="485fa-124">Aby skonfigurować integrację usługi Azure AD cieplarnianych, należy dodać cieplarnianych z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="485fa-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="485fa-125">**Aby dodać cieplarnianych z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="485fa-125">**To add Greenhouse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="485fa-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="485fa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="485fa-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="485fa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="485fa-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="485fa-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="485fa-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="485fa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="485fa-133">W polu wyszukiwania wpisz **cieplarnianych**, wybierz pozycję **cieplarnianych** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="485fa-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span></span>

    ![Cieplarnianych na liście wyników](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="485fa-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="485fa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="485fa-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z cieplarnianych w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="485fa-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="485fa-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w cieplarnianych jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="485fa-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span></span> <span data-ttu-id="485fa-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w cieplarnianych musi się.</span><span class="sxs-lookup"><span data-stu-id="485fa-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span></span>

<span data-ttu-id="485fa-139">W szklarni, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="485fa-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="485fa-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z cieplarnianych, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="485fa-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="485fa-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="485fa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="485fa-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="485fa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="485fa-143">**[Tworzenie użytkownika testowego cieplarnianych](#create-a-greenhouse-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta cieplarnianych połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="485fa-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="485fa-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="485fa-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="485fa-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="485fa-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="485fa-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="485fa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="485fa-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji cieplarnianych.</span><span class="sxs-lookup"><span data-stu-id="485fa-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="485fa-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z cieplarnianych, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="485fa-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="485fa-149">W portalu Azure na **cieplarnianych** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="485fa-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="485fa-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="485fa-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="485fa-153">Na **cieplarnianych domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="485fa-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny cieplarnianych pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="485fa-155">a.</span><span class="sxs-lookup"><span data-stu-id="485fa-155">a.</span></span> <span data-ttu-id="485fa-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="485fa-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="485fa-157">b.</span><span class="sxs-lookup"><span data-stu-id="485fa-157">b.</span></span> <span data-ttu-id="485fa-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="485fa-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="485fa-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="485fa-159">These values are not real.</span></span> <span data-ttu-id="485fa-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="485fa-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="485fa-161">Skontaktuj się z [zespołem pomocy technicznej klienta cieplarnianych](https://www.greenhouse.io/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="485fa-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span></span> 
 


4. <span data-ttu-id="485fa-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="485fa-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="485fa-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="485fa-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="485fa-166">Skonfigurować logowanie jednokrotne w **cieplarnianych** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej cieplarnianych](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="485fa-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="485fa-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="485fa-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="485fa-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="485fa-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="485fa-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="485fa-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="485fa-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="485fa-170">Create an Azure AD test user</span></span>

<span data-ttu-id="485fa-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="485fa-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="485fa-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="485fa-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="485fa-174">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="485fa-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="485fa-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="485fa-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="485fa-178">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="485fa-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="485fa-180">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="485fa-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="485fa-182">a.</span><span class="sxs-lookup"><span data-stu-id="485fa-182">a.</span></span> <span data-ttu-id="485fa-183">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="485fa-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="485fa-184">b.</span><span class="sxs-lookup"><span data-stu-id="485fa-184">b.</span></span> <span data-ttu-id="485fa-185">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="485fa-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="485fa-186">c.</span><span class="sxs-lookup"><span data-stu-id="485fa-186">c.</span></span> <span data-ttu-id="485fa-187">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="485fa-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="485fa-188">d.</span><span class="sxs-lookup"><span data-stu-id="485fa-188">d.</span></span> <span data-ttu-id="485fa-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="485fa-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="485fa-190">Tworzenie użytkownika testowego cieplarnianych</span><span class="sxs-lookup"><span data-stu-id="485fa-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="485fa-191">Aby włączyć użytkowników usługi Azure AD zalogować się do cieplarnianych, muszą mieć przydzielone do cieplarnianych.</span><span class="sxs-lookup"><span data-stu-id="485fa-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="485fa-192">W przypadku szklarni Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="485fa-192">In the case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="485fa-193">Możesz użyć innych cieplarnianych użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez cieplarnianych do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="485fa-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 

<span data-ttu-id="485fa-194">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="485fa-194">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="485fa-195">Zaloguj się do Twojego **cieplarnianych** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="485fa-195">Log in to your **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="485fa-196">W menu u góry kliknij **Konfiguruj**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="485fa-196">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="485fa-197">![Użytkownicy](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="485fa-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="485fa-198">Kliknij przycisk **nowych użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="485fa-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="485fa-199">![Nowy użytkownik](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="485fa-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="485fa-200">W **Dodaj nowego użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="485fa-200">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="485fa-201">![Dodaj nowego użytkownika](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Dodaj nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="485fa-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="485fa-202">a.</span><span class="sxs-lookup"><span data-stu-id="485fa-202">a.</span></span> <span data-ttu-id="485fa-203">W **wprowadź wiadomości e-mail użytkownika** tekstowym, wpisz adres e-mail prawidłowe konto usługi Azure Active Directory, aby udostępnić.</span><span class="sxs-lookup"><span data-stu-id="485fa-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>

   <span data-ttu-id="485fa-204">b.</span><span class="sxs-lookup"><span data-stu-id="485fa-204">b.</span></span> <span data-ttu-id="485fa-205">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="485fa-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="485fa-206">Posiadaczy konta usługi Azure Active Directory zostanie wysłana wiadomość e-mail, łącznie z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="485fa-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="485fa-207">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="485fa-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="485fa-208">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu cieplarnianych.</span><span class="sxs-lookup"><span data-stu-id="485fa-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="485fa-210">**Aby przypisać Simona Britta cieplarnianych, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="485fa-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="485fa-211">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="485fa-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="485fa-213">Na liście aplikacji zaznacz **cieplarnianych**.</span><span class="sxs-lookup"><span data-stu-id="485fa-213">In the applications list, select **Greenhouse**.</span></span>

    ![Łącze cieplarnianych na liście aplikacji](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="485fa-215">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="485fa-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="485fa-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="485fa-217">Click **Add** button.</span></span> <span data-ttu-id="485fa-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="485fa-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="485fa-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="485fa-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="485fa-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="485fa-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="485fa-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="485fa-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="485fa-223">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="485fa-223">Test single sign-on</span></span>

<span data-ttu-id="485fa-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="485fa-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="485fa-225">Po kliknięciu kafelka cieplarnianych w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji cieplarnianych.</span><span class="sxs-lookup"><span data-stu-id="485fa-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span></span>
<span data-ttu-id="485fa-226">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="485fa-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="485fa-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="485fa-227">Additional resources</span></span>

* [<span data-ttu-id="485fa-228">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="485fa-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="485fa-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="485fa-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

