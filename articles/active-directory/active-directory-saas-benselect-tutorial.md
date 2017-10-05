---
title: 'Samouczek: Integracji Azure Active Directory z BenSelect | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="02966-103">Samouczek: Integracji Azure Active Directory z BenSelect</span><span class="sxs-lookup"><span data-stu-id="02966-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="02966-104">Z tego samouczka dowiesz się integrowanie BenSelect z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02966-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02966-105">Integracja z usługą Azure AD BenSelect zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="02966-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02966-106">Można kontrolować w usłudze Azure AD, który ma dostęp do BenSelect</span><span class="sxs-lookup"><span data-stu-id="02966-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="02966-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do BenSelect (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="02966-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02966-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="02966-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="02966-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02966-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02966-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="02966-110">Prerequisites</span></span>

<span data-ttu-id="02966-111">Aby skonfigurować integrację usługi Azure AD z BenSelect, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="02966-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="02966-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="02966-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02966-113">BenSelect logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="02966-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02966-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="02966-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02966-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="02966-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02966-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="02966-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02966-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02966-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02966-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="02966-118">Scenario description</span></span>
<span data-ttu-id="02966-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="02966-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02966-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="02966-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02966-121">Dodawanie BenSelect z galerii</span><span class="sxs-lookup"><span data-stu-id="02966-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="02966-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="02966-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="02966-123">Dodawanie BenSelect z galerii</span><span class="sxs-lookup"><span data-stu-id="02966-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="02966-124">Aby skonfigurować integrację usługi Azure AD BenSelect, należy dodać BenSelect z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="02966-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02966-125">**Aby dodać BenSelect z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="02966-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02966-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="02966-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="02966-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="02966-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02966-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="02966-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="02966-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="02966-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="02966-133">W polu wyszukiwania wpisz **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="02966-133">In the search box, type **BenSelect**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="02966-135">W panelu wyników wybierz **BenSelect**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="02966-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02966-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="02966-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02966-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BenSelect na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="02966-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="02966-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w BenSelect jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02966-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="02966-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w BenSelect musi się.</span><span class="sxs-lookup"><span data-stu-id="02966-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="02966-141">W BenSelect, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="02966-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="02966-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BenSelect, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="02966-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02966-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="02966-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02966-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="02966-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02966-145">**[Tworzenie użytkownika testowego BenSelect](#creating-a-benselect-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta BenSelect połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02966-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="02966-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="02966-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02966-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="02966-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02966-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="02966-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02966-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji BenSelect.</span><span class="sxs-lookup"><span data-stu-id="02966-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="02966-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z BenSelect, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="02966-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="02966-151">W portalu Azure na **BenSelect** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="02966-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="02966-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="02966-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="02966-155">Na **BenSelect domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="02966-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="02966-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="02966-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02966-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="02966-158">This value is not real.</span></span> <span data-ttu-id="02966-159">Zaktualizuj tę wartość przy rzeczywisty adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="02966-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="02966-160">Skontaktuj się z [zespołem pomocy technicznej BenSelect](mailto:support@selerix.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="02966-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="02966-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="02966-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="02966-163">Aplikacja BenSelect oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="02966-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="02966-164">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02966-164">Configure the following claims for this application.</span></span> <span data-ttu-id="02966-165">Możesz zarządzać wartości tych atrybutów z **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02966-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="02966-166">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="02966-166">The following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="02966-168">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="02966-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="02966-169">a.</span><span class="sxs-lookup"><span data-stu-id="02966-169">a.</span></span> <span data-ttu-id="02966-170">W **identyfikator użytkownika** listy rozwijanej wybierz **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="02966-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="02966-171">b.</span><span class="sxs-lookup"><span data-stu-id="02966-171">b.</span></span> <span data-ttu-id="02966-172">W **poczty** listy rozwijanej wybierz **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="02966-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="02966-173">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="02966-173">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="02966-175">Na **konfiguracji BenSelect** , kliknij przycisk **skonfigurować BenSelect** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="02966-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="02966-176">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="02966-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="02966-178">Aby skonfigurować logowanie jednokrotne w **BenSelect** stronie, musisz wysłać pobrany **Certificate(Raw)** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi**do [zespołem pomocy technicznej BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="02966-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="02966-179">Należy podać, czy ta integracja wymaga algorytm SHA256 (SHA1 nie jest obsługiwana) można ustawić logowania jednokrotnego dla odpowiedniego serwera, takich jak app2101 itd.</span><span class="sxs-lookup"><span data-stu-id="02966-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="02966-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="02966-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="02966-181">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="02966-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="02966-182">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="02966-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02966-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="02966-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="02966-184">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="02966-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="02966-186">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="02966-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02966-187">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="02966-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02966-189">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="02966-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02966-191">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="02966-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02966-193">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="02966-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02966-195">a.</span><span class="sxs-lookup"><span data-stu-id="02966-195">a.</span></span> <span data-ttu-id="02966-196">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02966-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02966-197">b.</span><span class="sxs-lookup"><span data-stu-id="02966-197">b.</span></span> <span data-ttu-id="02966-198">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02966-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02966-199">c.</span><span class="sxs-lookup"><span data-stu-id="02966-199">c.</span></span> <span data-ttu-id="02966-200">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="02966-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="02966-201">d.</span><span class="sxs-lookup"><span data-stu-id="02966-201">d.</span></span> <span data-ttu-id="02966-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="02966-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="02966-203">Tworzenie użytkownika testowego BenSelect</span><span class="sxs-lookup"><span data-stu-id="02966-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="02966-204">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w BenSelect.</span><span class="sxs-lookup"><span data-stu-id="02966-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="02966-205">Praca z [zespołem pomocy technicznej BenSelect](mailto:support@selerix.com) Aby dodać użytkowników w ramach konta BenSelect.</span><span class="sxs-lookup"><span data-stu-id="02966-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="02966-206">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="02966-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="02966-207">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu BenSelect.</span><span class="sxs-lookup"><span data-stu-id="02966-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="02966-209">**Aby przypisać Simona Britta BenSelect, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="02966-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="02966-210">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="02966-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="02966-212">Na liście aplikacji zaznacz **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="02966-212">In the applications list, select **BenSelect**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="02966-214">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="02966-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="02966-216">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="02966-216">Click **Add** button.</span></span> <span data-ttu-id="02966-217">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="02966-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="02966-219">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="02966-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02966-220">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="02966-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02966-221">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="02966-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02966-222">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="02966-222">Testing single sign-on</span></span>

<span data-ttu-id="02966-223">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="02966-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="02966-224">Po kliknięciu kafelka BenSelect w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji BenSelect.</span><span class="sxs-lookup"><span data-stu-id="02966-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02966-225">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="02966-225">Additional resources</span></span>

* [<span data-ttu-id="02966-226">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02966-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02966-227">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02966-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

