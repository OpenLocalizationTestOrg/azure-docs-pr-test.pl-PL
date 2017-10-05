---
title: "Samouczek: Integracji Azure Active Directory szkolenie świadomości bezpieczeństwa KnowBe4 | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 3b18737112a8aef101fab7fac1904f7c2e194d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="b3992-103">Samouczek: Integracji Azure Active Directory szkolenie świadomości bezpieczeństwa KnowBe4</span><span class="sxs-lookup"><span data-stu-id="b3992-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="b3992-104">Z tego samouczka dowiesz integrowanie świadomości szkolenia w zakresie zabezpieczeń KnowBe4 z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3992-104">In this tutorial, you learn how to integrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3992-105">Integracja z usługą Azure AD świadomości szkolenia w zakresie zabezpieczeń KnowBe4 zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b3992-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b3992-106">Można kontrolować w usłudze Azure AD, który ma dostęp do szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="b3992-106">You can control in Azure AD who has access to KnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="b3992-107">Umożliwia użytkownikom automatycznie pobrać podpisany w zakresie świadomości bezpieczeństwa KnowBe4 (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3992-107">You can enable your users to automatically get signed-on to KnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3992-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b3992-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b3992-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3992-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3992-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3992-110">Prerequisites</span></span>

<span data-ttu-id="b3992-111">Aby skonfigurować integrację usługi Azure AD szkolenie świadomości bezpieczeństwa KnowBe4, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b3992-111">To configure Azure AD integration with KnowBe4 Security Awareness Training, you need the following items:</span></span>

- <span data-ttu-id="b3992-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3992-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3992-113">Rozpoznawanie szkolenia w zakresie zabezpieczeń KnowBe4 logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b3992-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3992-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3992-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3992-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b3992-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3992-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b3992-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3992-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3992-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3992-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b3992-118">Scenario description</span></span>
<span data-ttu-id="b3992-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b3992-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3992-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b3992-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3992-121">Dodawanie KnowBe4 świadomości szkolenia w zakresie zabezpieczeń z galerii</span><span class="sxs-lookup"><span data-stu-id="b3992-121">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
2. <span data-ttu-id="b3992-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3992-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-the-gallery"></a><span data-ttu-id="b3992-123">Dodawanie KnowBe4 świadomości szkolenia w zakresie zabezpieczeń z galerii</span><span class="sxs-lookup"><span data-stu-id="b3992-123">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
<span data-ttu-id="b3992-124">Aby skonfigurować integrację usługi Azure AD szkolenia świadomości bezpieczeństwa KnowBe4, należy dodać świadomości szkolenia w zakresie zabezpieczeń KnowBe4 z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b3992-124">To configure the integration of KnowBe4 Security Awareness Training into Azure AD, you need to add KnowBe4 Security Awareness Training from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b3992-125">**Aby dodać świadomości szkolenia w zakresie zabezpieczeń KnowBe4 z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3992-125">**To add KnowBe4 Security Awareness Training from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b3992-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3992-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b3992-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b3992-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b3992-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3992-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b3992-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3992-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b3992-133">W polu wyszukiwania wpisz **świadomości szkolenia w zakresie zabezpieczeń KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="b3992-133">In the search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="b3992-135">W panelu wyników wybierz **świadomości szkolenia w zakresie zabezpieczeń KnowBe4**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="b3992-135">In the results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3992-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3992-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3992-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z KnowBe4 świadomości szkolenia w zakresie zabezpieczeń w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b3992-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b3992-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w zakresie świadomości bezpieczeństwa KnowBe4 jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3992-139">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 Security Awareness Training is to a user in Azure AD.</span></span> <span data-ttu-id="b3992-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w zakresie świadomości bezpieczeństwa KnowBe4 musi się.</span><span class="sxs-lookup"><span data-stu-id="b3992-140">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 Security Awareness Training needs to be established.</span></span>

<span data-ttu-id="b3992-141">W zakresie świadomości bezpieczeństwa KnowBe4, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="b3992-141">In KnowBe4 Security Awareness Training, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b3992-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej szkolenie świadomości bezpieczeństwa KnowBe4, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="b3992-142">To configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b3992-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b3992-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b3992-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3992-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3992-145">**[Tworzenie użytkownika testowego świadomości szkolenia w zakresie zabezpieczeń KnowBe4](#creating-a-knowbe4-security-awareness-training-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta KnowBe4 świadomości szkolenia w zakresie zabezpieczeń połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b3992-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - to have a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3992-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b3992-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3992-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="b3992-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3992-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3992-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3992-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w zakresie świadomości bezpieczeństwa KnowBe4 aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b3992-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="b3992-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3992-150">**To configure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="b3992-151">W portalu Azure na **świadomości szkolenia w zakresie zabezpieczeń KnowBe4** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b3992-151">In the Azure portal, on the **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b3992-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="b3992-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="b3992-155">Na **KnowBe4 zabezpieczeń świadomości szkolenia domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3992-155">On the **KnowBe4 Security Awareness Training Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="b3992-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b3992-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3992-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b3992-158">The value is not real.</span></span> <span data-ttu-id="b3992-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="b3992-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="b3992-160">Skontaktuj się z [zespołem pomocy technicznej klienta szkolenia świadomości bezpieczeństwa KnowBe4](mailto:support@KnowBe4.com) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="b3992-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) to get the value.</span></span> 
 

4. <span data-ttu-id="b3992-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b3992-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="b3992-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3992-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3992-165">Na **konfiguracji szkolenia świadomości bezpieczeństwa KnowBe4** , kliknij przycisk **skonfigurować KnowBe4 świadomości szkolenia w zakresie zabezpieczeń** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b3992-165">On the **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b3992-166">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b3992-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="b3992-168">Skonfigurować logowanie jednokrotne w **świadomości szkolenia w zakresie zabezpieczeń KnowBe4** stronie, musisz wysłać pobrany **certyfikatu (Raw)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej klienta szkolenia świadomości bezpieczeństwa KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="b3992-168">To configure single sign-on on **KnowBe4 Security Awareness Training** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="b3992-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="b3992-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b3992-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="b3992-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b3992-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3992-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3992-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3992-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3992-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3992-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b3992-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3992-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b3992-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3992-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3992-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b3992-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3992-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3992-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3992-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3992-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3992-184">a.</span><span class="sxs-lookup"><span data-stu-id="b3992-184">a.</span></span> <span data-ttu-id="b3992-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3992-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3992-186">b.</span><span class="sxs-lookup"><span data-stu-id="b3992-186">b.</span></span> <span data-ttu-id="b3992-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b3992-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3992-188">c.</span><span class="sxs-lookup"><span data-stu-id="b3992-188">c.</span></span> <span data-ttu-id="b3992-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b3992-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b3992-190">d.</span><span class="sxs-lookup"><span data-stu-id="b3992-190">d.</span></span> <span data-ttu-id="b3992-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b3992-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="b3992-192">Tworzenie użytkownika testowego świadomości szkolenia w zakresie zabezpieczeń KnowBe4</span><span class="sxs-lookup"><span data-stu-id="b3992-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="b3992-193">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w zakresie świadomości bezpieczeństwa KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="b3992-193">The objective of this section is to create a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="b3992-194">Rozpoznawanie szkolenia w zakresie zabezpieczeń KnowBe4 obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="b3992-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b3992-195">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b3992-195">There is no action item for you in this section.</span></span> <span data-ttu-id="b3992-196">Nowy użytkownik jest tworzony podczas próby dostępu do szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="b3992-196">A new user is created during an attempt to access KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="b3992-197">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej w zakresie świadomości bezpieczeństwa KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="b3992-197">If you need to create a user manually, you need to contact the [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b3992-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3992-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b3992-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b3992-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowBe4 Security Awareness Training.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b3992-201">**Aby przypisać Simona Britta do szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3992-201">**To assign Britta Simon to KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="b3992-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3992-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b3992-204">Na liście aplikacji zaznacz **świadomości szkolenia w zakresie zabezpieczeń KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="b3992-204">In the applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="b3992-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b3992-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b3992-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3992-208">Click **Add** button.</span></span> <span data-ttu-id="b3992-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3992-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b3992-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="b3992-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b3992-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3992-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3992-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3992-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3992-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3992-214">Testing single sign-on</span></span>

<span data-ttu-id="b3992-215">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b3992-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="b3992-216">Po kliknięciu kafelka świadomości szkolenia w zakresie zabezpieczeń KnowBe4 w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b3992-216">When you click the KnowBe4 Security Awareness Training tile in the Access Panel, you should get automatically signed-on to your KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3992-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b3992-217">Additional resources</span></span>

* [<span data-ttu-id="b3992-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3992-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3992-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b3992-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

