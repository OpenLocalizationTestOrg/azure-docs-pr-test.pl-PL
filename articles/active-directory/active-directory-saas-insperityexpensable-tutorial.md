---
title: 'Samouczek: Integracji Azure Active Directory z Insperity ExpensAble | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: b50e10be54b1fc413be10bee5b58631790629335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="9495c-103">Samouczek: Integracji Azure Active Directory z Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="9495c-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="9495c-104">Z tego samouczka dowiesz się integrowanie Insperity ExpensAble w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9495c-104">In this tutorial, you learn how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9495c-105">Integrowanie Insperity ExpensAble z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9495c-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9495c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="9495c-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
- <span data-ttu-id="9495c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Insperity ExpensAble (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9495c-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9495c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9495c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9495c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9495c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9495c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9495c-110">Prerequisites</span></span>

<span data-ttu-id="9495c-111">Aby skonfigurować integrację usługi Azure AD z Insperity ExpensAble, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9495c-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

- <span data-ttu-id="9495c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9495c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9495c-113">Insperity ExpensAble jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9495c-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9495c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9495c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9495c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9495c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9495c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9495c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9495c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9495c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9495c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9495c-118">Scenario description</span></span>
<span data-ttu-id="9495c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9495c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9495c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9495c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9495c-121">Dodawanie Insperity ExpensAble z galerii</span><span class="sxs-lookup"><span data-stu-id="9495c-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="9495c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9495c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="9495c-123">Dodawanie Insperity ExpensAble z galerii</span><span class="sxs-lookup"><span data-stu-id="9495c-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="9495c-124">Aby skonfigurować integrację Insperity ExpensAble do usługi Azure AD, należy dodać do listy zarządzane aplikacje SaaS Insperity ExpensAble z galerii.</span><span class="sxs-lookup"><span data-stu-id="9495c-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9495c-125">**Aby dodać Insperity ExpensAble z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9495c-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9495c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9495c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9495c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9495c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9495c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9495c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9495c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9495c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9495c-133">W polu wyszukiwania wpisz **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="9495c-133">In the search box, type **Insperity ExpensAble**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="9495c-135">W panelu wyników wybierz **Insperity ExpensAble**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9495c-135">In the results panel, select **Insperity ExpensAble**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9495c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9495c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9495c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Insperity ExpensAble w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9495c-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9495c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Insperity ExpensAble jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9495c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble is to a user in Azure AD.</span></span> <span data-ttu-id="9495c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Insperity ExpensAble musi się.</span><span class="sxs-lookup"><span data-stu-id="9495c-140">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>

<span data-ttu-id="9495c-141">W Insperity ExpensAble przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="9495c-141">In Insperity ExpensAble, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9495c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Insperity ExpensAble, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9495c-142">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9495c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9495c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9495c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9495c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9495c-145">**[Tworzenie Insperity ExpensAble użytkownika testowego](#creating-an-insperity-expensable-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Insperity ExpensAble połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9495c-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9495c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9495c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9495c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9495c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9495c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9495c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9495c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w Insperity ExpensAble aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9495c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="9495c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Insperity ExpensAble, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9495c-150">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="9495c-151">W portalu Azure na **Insperity ExpensAble** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9495c-151">In the Azure portal, on the **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9495c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9495c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="9495c-155">Na **Insperity ExpensAble domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9495c-155">On the **Insperity ExpensAble Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="9495c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9495c-157">a.</span></span> <span data-ttu-id="9495c-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="9495c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9495c-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9495c-159">This value is not real.</span></span> <span data-ttu-id="9495c-160">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="9495c-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="9495c-161">Skontaktuj się z [zespołem pomocy technicznej klienta ExpensAble Insperity](http://expensable.com/support/support-overview) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="9495c-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) to get this value.</span></span> 
 
4. <span data-ttu-id="9495c-162">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9495c-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="9495c-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9495c-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9495c-166">Na **konfiguracji ExpensAble Insperity** , kliknij przycisk **skonfigurować ExpensAble Insperity** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9495c-166">On the **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9495c-167">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9495c-167">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="9495c-169">Aby skonfigurować logowanie jednokrotne w **Insperity ExpensAble** stronie, musisz wysłać pobrany **XML metadanych**, **SAML pojedynczy znak na adres URL usługi** i  **Identyfikator jednostki SAML** do [Insperity ExpensAble zespołem pomocy technicznej](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="9495c-169">To configure single sign-on on **Insperity ExpensAble** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="9495c-170">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="9495c-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9495c-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9495c-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9495c-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9495c-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9495c-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9495c-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9495c-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9495c-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="9495c-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9495c-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9495c-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9495c-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9495c-178">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9495c-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9495c-180">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9495c-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9495c-182">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9495c-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9495c-184">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9495c-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9495c-186">a.</span><span class="sxs-lookup"><span data-stu-id="9495c-186">a.</span></span> <span data-ttu-id="9495c-187">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9495c-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9495c-188">b.</span><span class="sxs-lookup"><span data-stu-id="9495c-188">b.</span></span> <span data-ttu-id="9495c-189">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9495c-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9495c-190">c.</span><span class="sxs-lookup"><span data-stu-id="9495c-190">c.</span></span> <span data-ttu-id="9495c-191">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9495c-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9495c-192">d.</span><span class="sxs-lookup"><span data-stu-id="9495c-192">d.</span></span> <span data-ttu-id="9495c-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9495c-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="9495c-194">Tworzenie Insperity ExpensAble użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="9495c-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="9495c-195">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="9495c-195">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="9495c-196">We współpracy z [Insperity ExpensAble zespołem pomocy technicznej](http://expensable.com/support/support-overview) Aby dodać użytkowników w ramach Insperity ExpensAble konta.</span><span class="sxs-lookup"><span data-stu-id="9495c-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) to add the users in the Insperity ExpensAble account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9495c-197">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9495c-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9495c-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="9495c-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insperity ExpensAble.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9495c-200">**Aby przypisać Simona Britta Insperity ExpensAble, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9495c-200">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="9495c-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9495c-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9495c-203">Na liście aplikacji zaznacz **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="9495c-203">In the applications list, select **Insperity ExpensAble**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="9495c-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9495c-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9495c-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9495c-207">Click **Add** button.</span></span> <span data-ttu-id="9495c-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9495c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9495c-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9495c-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9495c-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9495c-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9495c-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9495c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9495c-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9495c-213">Testing single sign-on</span></span>

<span data-ttu-id="9495c-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9495c-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9495c-215">Po kliknięciu kafelka Insperity ExpensAble w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Insperity ExpensAble aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9495c-215">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>
<span data-ttu-id="9495c-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9495c-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9495c-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9495c-217">Additional resources</span></span>

* [<span data-ttu-id="9495c-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9495c-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9495c-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9495c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

