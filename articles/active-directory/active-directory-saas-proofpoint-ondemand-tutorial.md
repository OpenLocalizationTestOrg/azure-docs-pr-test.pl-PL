---
title: "Samouczek: Integracji Azure Active Directory z Proofpoint na żądanie | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Proofpoint na żądanie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="bfd16-103">Samouczek: Integracji Azure Active Directory z Proofpoint na żądanie</span><span class="sxs-lookup"><span data-stu-id="bfd16-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="bfd16-104">Z tego samouczka dowiesz się integrowanie Proofpoint na żądanie z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfd16-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfd16-105">Integrowanie Proofpoint na żądanie z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bfd16-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bfd16-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Proofpoint na żądanie</span><span class="sxs-lookup"><span data-stu-id="bfd16-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="bfd16-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Proofpoint na żądanie (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd16-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfd16-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bfd16-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bfd16-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfd16-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfd16-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bfd16-110">Prerequisites</span></span>

<span data-ttu-id="bfd16-111">Aby skonfigurować integrację usługi Azure AD z Proofpoint na żądanie, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bfd16-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="bfd16-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd16-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfd16-113">Proofpoint na żądanie jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bfd16-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfd16-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bfd16-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfd16-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bfd16-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfd16-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bfd16-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfd16-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfd16-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfd16-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bfd16-118">Scenario description</span></span>
<span data-ttu-id="bfd16-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bfd16-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfd16-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bfd16-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfd16-121">Dodawanie Proofpoint na żądanie z galerii</span><span class="sxs-lookup"><span data-stu-id="bfd16-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="bfd16-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bfd16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="bfd16-123">Dodawanie Proofpoint na żądanie z galerii</span><span class="sxs-lookup"><span data-stu-id="bfd16-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="bfd16-124">Aby skonfigurować integrację Proofpoint na żądanie do usługi Azure AD, należy dodać Proofpoint na żądanie z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bfd16-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bfd16-125">**Aby dodać Proofpoint na żądanie z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfd16-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bfd16-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bfd16-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bfd16-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bfd16-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bfd16-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfd16-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bfd16-133">W polu wyszukiwania wpisz **Proofpoint na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="bfd16-135">W panelu wyników wybierz **Proofpoint na żądanie**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bfd16-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfd16-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bfd16-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfd16-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Proofpoint na żądanie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bfd16-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bfd16-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w Proofpoint na żądanie dla użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfd16-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="bfd16-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Proofpoint na żądanie.</span><span class="sxs-lookup"><span data-stu-id="bfd16-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="bfd16-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Proofpoint na żądanie.</span><span class="sxs-lookup"><span data-stu-id="bfd16-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="bfd16-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Proofpoint na żądanie, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bfd16-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bfd16-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bfd16-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bfd16-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bfd16-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfd16-145">**[Tworzenie na żądanie użytkownika testowego Proofpoint](#creating-a-proofpoint-on-demand-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Proofpoint na żądanie, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bfd16-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfd16-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bfd16-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfd16-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bfd16-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfd16-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bfd16-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfd16-149">W tej sekcji możesz włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i konfigurowania rejestracji jednokrotnej w sieci Proofpoint na żądanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bfd16-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="bfd16-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Proofpoint na żądanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfd16-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="bfd16-151">W portalu Azure na **Proofpoint na żądanie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bfd16-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bfd16-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="bfd16-155">Na **Proofpoint na żądanie domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfd16-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="bfd16-157">a.In **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="bfd16-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="bfd16-158">b.</span><span class="sxs-lookup"><span data-stu-id="bfd16-158">b.</span></span> <span data-ttu-id="bfd16-159">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="bfd16-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="bfd16-160">c.</span><span class="sxs-lookup"><span data-stu-id="bfd16-160">c.</span></span>  <span data-ttu-id="bfd16-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="bfd16-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bfd16-162">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="bfd16-162">These values are not the real.</span></span> <span data-ttu-id="bfd16-163">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="bfd16-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="bfd16-164">Skontaktuj się z [Proofpoint na żądanie klienta zespołem pomocy technicznej](https://www.proofpoint.com/us/support-services) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="bfd16-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="bfd16-165">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bfd16-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="bfd16-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bfd16-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="bfd16-169">Na **Proofpoint na żądanie konfiguracji** kliknij **skonfigurować Proofpoint na żądanie** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bfd16-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bfd16-170">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bfd16-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="bfd16-172">Skonfigurować logowanie jednokrotne w **Proofpoint na żądanie** stronie, musisz wysłać pobrany **Certificate(Base64)**,**identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** do [Proofpoint na żądanie klienta zespołem pomocy technicznej](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="bfd16-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="bfd16-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bfd16-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bfd16-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bfd16-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bfd16-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfd16-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfd16-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd16-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfd16-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bfd16-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bfd16-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfd16-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bfd16-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bfd16-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfd16-182">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="bfd16-182">These values are not the real.</span></span> <span data-ttu-id="bfd16-183">Zaktualizować te wartości z rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="bfd16-183">Update these values with the actual</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfd16-185">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfd16-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfd16-187">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfd16-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfd16-189">a.</span><span class="sxs-lookup"><span data-stu-id="bfd16-189">a.</span></span> <span data-ttu-id="bfd16-190">W **nazwa** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="bfd16-191">b.</span><span class="sxs-lookup"><span data-stu-id="bfd16-191">b.</span></span> <span data-ttu-id="bfd16-192">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bfd16-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bfd16-193">c.</span><span class="sxs-lookup"><span data-stu-id="bfd16-193">c.</span></span> <span data-ttu-id="bfd16-194">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bfd16-195">d.</span><span class="sxs-lookup"><span data-stu-id="bfd16-195">d.</span></span> <span data-ttu-id="bfd16-196">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="bfd16-197">Tworzenie Proofpoint na żądanie użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="bfd16-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="bfd16-198">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Proofpoint na żądanie.</span><span class="sxs-lookup"><span data-stu-id="bfd16-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="bfd16-199">Praca z [Proofpoint na żądanie klienta zespołem pomocy technicznej](https://www.proofpoint.com/us/support-services) do dodawania użytkowników w Proofpoint na platformie żądanie.</span><span class="sxs-lookup"><span data-stu-id="bfd16-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bfd16-200">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd16-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bfd16-201">W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Proofpoint na żądanie.</span><span class="sxs-lookup"><span data-stu-id="bfd16-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bfd16-203">**Aby przypisać Simona Britta Proofpoint na żądanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfd16-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="bfd16-204">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bfd16-206">Na liście aplikacji zaznacz **Proofpoint na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="bfd16-208">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bfd16-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bfd16-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bfd16-210">Click **Add** button.</span></span> <span data-ttu-id="bfd16-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfd16-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bfd16-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bfd16-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bfd16-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfd16-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfd16-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfd16-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bfd16-216">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bfd16-216">Testing single sign-on</span></span>

<span data-ttu-id="bfd16-217">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bfd16-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bfd16-218">Po kliknięciu **Proofpoint na żądanie** Kafelek na panelu dostępu użytkownik powinien automatycznie zalogować się przy do Twojej Proofpoint na żądanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bfd16-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="bfd16-219">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bfd16-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="bfd16-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bfd16-220">Additional resources</span></span>

* [<span data-ttu-id="bfd16-221">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfd16-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfd16-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfd16-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

