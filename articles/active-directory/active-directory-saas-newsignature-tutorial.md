---
title: "Samouczek: Integracji Azure Active Directory za pomocą portalu zarządzania w chmurze Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i chmury portalu zarządzania Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: bae5f05a161b2730bf662bcb47f20ab3e1799951
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="f7a8a-103">Samouczek: Integracji Azure Active Directory za pomocą portalu zarządzania w chmurze Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f7a8a-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="f7a8a-104">Z tego samouczka dowiesz się integrowanie portalu zarządzania w chmurze platformy Microsoft Azure z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7a8a-104">In this tutorial, you learn how to integrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7a8a-105">Integrowanie portalu zarządzania w chmurze platformy Microsoft Azure z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7a8a-106">Można kontrolować w usłudze Azure AD, który ma dostęp do portalu zarządzania w chmurze Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f7a8a-106">You can control in Azure AD who has access to Cloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="f7a8a-107">Umożliwia użytkownikom automatycznie pobrać podpisany w chmurze portalu zarządzania Microsoft Azure (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7a8a-107">You can enable your users to automatically get signed-on to Cloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7a8a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f7a8a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f7a8a-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7a8a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7a8a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7a8a-110">Prerequisites</span></span>

<span data-ttu-id="f7a8a-111">Aby skonfigurować integrację usługi Azure AD za pomocą portalu zarządzania w chmurze Microsoft Azure, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-111">To configure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need the following items:</span></span>

- <span data-ttu-id="f7a8a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7a8a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7a8a-113">Portal zarządzania chmury dla Microsoft Azure jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f7a8a-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7a8a-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7a8a-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7a8a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7a8a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7a8a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7a8a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f7a8a-118">Scenario description</span></span>
<span data-ttu-id="f7a8a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7a8a-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7a8a-121">Dodawanie chmury portalu zarządzania Microsoft Azure z galerii</span><span class="sxs-lookup"><span data-stu-id="f7a8a-121">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
2. <span data-ttu-id="f7a8a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f7a8a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-the-gallery"></a><span data-ttu-id="f7a8a-123">Dodawanie chmury portalu zarządzania Microsoft Azure z galerii</span><span class="sxs-lookup"><span data-stu-id="f7a8a-123">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
<span data-ttu-id="f7a8a-124">Aby skonfigurować integrację usługi Azure AD Cloud portalu zarządzania Microsoft Azure, należy dodać Portal zarządzania w chmurze Microsoft Azure z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-124">To configure the integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need to add Cloud Management Portal for Microsoft Azure from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7a8a-125">**Aby dodać chmury portalu zarządzania Microsoft Azure z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7a8a-125">**To add Cloud Management Portal for Microsoft Azure from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7a8a-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f7a8a-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7a8a-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f7a8a-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f7a8a-133">W polu wyszukiwania wpisz **chmury portalu zarządzania Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-133">In the search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="f7a8a-135">W panelu wyników wybierz **chmury portalu zarządzania Microsoft Azure**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-135">In the results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7a8a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f7a8a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7a8a-138">W tej sekcji skonfigurować i przetestować usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania w chmurze platformy Microsoft Azure w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7a8a-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w chmurze Portal zarządzania platformy Microsoft Azure jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cloud Management Portal for Microsoft Azure is to a user in Azure AD.</span></span> <span data-ttu-id="f7a8a-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w chmurze Portal zarządzania platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-140">In other words, a link relationship between an Azure AD user and the related user in Cloud Management Portal for Microsoft Azure needs to be established.</span></span>

<span data-ttu-id="f7a8a-141">W chmurze Portal zarządzania platformy Microsoft Azure, przypisz wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-141">In Cloud Management Portal for Microsoft Azure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7a8a-142">Aby skonfigurować i przetestować usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania w chmurze Microsoft Azure, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-142">To configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7a8a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7a8a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7a8a-145">**[Tworzenie chmury Portal zarządzania dla użytkownika testowego Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  — aby odpowiednikiem Simona Britta w chmurze Portal zarządzania dla programu Microsoft Azure, z którymi jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - to have a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7a8a-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7a8a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7a8a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f7a8a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7a8a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w portalu zarządzania usługi chmury dla aplikacji Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="f7a8a-150">**Aby skonfigurować usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania w chmurze Microsoft Azure, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7a8a-150">**To configure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="f7a8a-151">W portalu Azure na **chmury portalu zarządzania Microsoft Azure** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-151">In the Azure portal, on the **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f7a8a-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="f7a8a-155">Na **chmury portalu zarządzania Microsoft Azure domeny i adresów URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-155">On the **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="f7a8a-157">a.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-157">a.</span></span> <span data-ttu-id="f7a8a-158">W **adres URL logowania** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="f7a8a-159">b.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-159">b.</span></span> <span data-ttu-id="f7a8a-160">W **identyfikator** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="f7a8a-161">c.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-161">c.</span></span> <span data-ttu-id="f7a8a-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="f7a8a-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-163">These values are not real.</span></span> <span data-ttu-id="f7a8a-164">Rzeczywisty adres URL logowania, identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-164">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="f7a8a-165">Skontaktuj się z [chmurze Portal zarządzania dla klienta platformy Microsoft Azure z pomocą techniczną](mailto:jczernuszka@newsignature.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) to get these values.</span></span> 
 
4. <span data-ttu-id="f7a8a-166">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="f7a8a-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f7a8a-170">Na **chmurze Portal zarządzania dla programu Microsoft Azure Configuration** kliknij **skonfigurować Portal zarządzania chmury Microsoft Azure** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-170">On the **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f7a8a-171">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f7a8a-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="f7a8a-173">Skonfigurować logowanie jednokrotne w **chmury portalu zarządzania Microsoft Azure** stronie, musisz wysłać pobrany **certyfikatu**, **Sign-Out adres URL**, **SAML pojedynczy znak na adres URL usługi** i **identyfikator jednostki SAML** do [chmurze Portal zarządzania dla zespołu pomocy technicznej Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="f7a8a-173">To configure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="f7a8a-174">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-174">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f7a8a-175">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f7a8a-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7a8a-176">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7a8a-177">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7a8a-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7a8a-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7a8a-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7a8a-179">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f7a8a-181">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7a8a-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7a8a-182">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7a8a-184">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7a8a-186">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7a8a-188">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f7a8a-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7a8a-190">a.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-190">a.</span></span> <span data-ttu-id="f7a8a-191">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7a8a-192">b.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-192">b.</span></span> <span data-ttu-id="f7a8a-193">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7a8a-194">c.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-194">c.</span></span> <span data-ttu-id="f7a8a-195">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f7a8a-196">d.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-196">d.</span></span> <span data-ttu-id="f7a8a-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="f7a8a-198">Tworzenie chmury Portal zarządzania dla użytkownika testowego Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f7a8a-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="f7a8a-199">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w chmurze portalu zarządzania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-199">The objective of this section is to create a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="f7a8a-200">We współpracy z [chmurze Portal zarządzania dla zespołu pomocy technicznej Microsoft Azure](mailto:jczernuszka@newsignature.com) Aby dodać użytkowników w portalu zarządzania chmury dla konta Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) to add the users in the Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f7a8a-201">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7a8a-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f7a8a-202">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do portalu zarządzania w chmurze platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cloud Management Portal for Microsoft Azure.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f7a8a-204">**Aby przypisać Simona Britta do chmury portalu zarządzania Microsoft Azure, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7a8a-204">**To assign Britta Simon to Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="f7a8a-205">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f7a8a-207">Na liście aplikacji zaznacz **chmury portalu zarządzania Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-207">In the applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="f7a8a-209">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f7a8a-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-211">Click **Add** button.</span></span> <span data-ttu-id="f7a8a-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f7a8a-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7a8a-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7a8a-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7a8a-217">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f7a8a-217">Testing single sign-on</span></span>

<span data-ttu-id="f7a8a-218">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="f7a8a-219">Po kliknięciu chmury portalu zarządzania Microsoft Azure kafelka w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do portalu zarządzania usługi chmury dla aplikacji Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a8a-219">When you click the Cloud Management Portal for Microsoft Azure tile in the Access Panel, you should get automatically signed-on to your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="f7a8a-220">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f7a8a-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7a8a-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f7a8a-221">Additional resources</span></span>

* [<span data-ttu-id="f7a8a-222">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7a8a-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7a8a-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7a8a-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

