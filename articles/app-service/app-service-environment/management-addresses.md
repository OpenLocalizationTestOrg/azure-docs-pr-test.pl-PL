---
title: "Adresy zarządzania środowiska usługi aplikacji Azure"
description: "Wyświetla listę adresów zarządzania używany do poleceń środowiska usługi aplikacji"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: e97a084772fd16252d925b62498d2e696629a25d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="0561b-103">Adresy zarządzania środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="0561b-103">App Service Environment management addresses</span></span>

<span data-ttu-id="0561b-104">Environment(ASE) usługi aplikacji to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="0561b-104">The App Service Environment(ASE) is a deployment of the Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="0561b-105">ASE musi być dostępny z usługi aplikacji Azure, dzięki czemu można nim zarządzać.</span><span class="sxs-lookup"><span data-stu-id="0561b-105">The ASE must be accessible from the Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="0561b-106">Ten ruch związany z zarządzaniem ASE jest przesyłany w sieci kontrolowanego przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0561b-106">This ASE management traffic traverses the user controlled network.</span></span>  <span data-ttu-id="0561b-107">Pochodzi on z serwerów zarządzania w usłudze Azure App Service do publicznego adresu IP, który jest skojarzony z ASE.</span><span class="sxs-lookup"><span data-stu-id="0561b-107">It comes from Azure App Service management servers to the public VIP that is associated with the ASE.</span></span>  <span data-ttu-id="0561b-108">Szczegółowe informacje na temat ASE networking zależności odczytu [sieci zagadnienia i środowiska usługi aplikacji][networking].</span><span class="sxs-lookup"><span data-stu-id="0561b-108">For details on the ASE networking dependencies read [Networking considerations and the App Service Environment][networking].</span></span>  <span data-ttu-id="0561b-109">Ogólne informacje na temat ASE można uruchomić z [wprowadzenie do środowiska usługi aplikacji][intro].</span><span class="sxs-lookup"><span data-stu-id="0561b-109">For general information on the ASE you can start with [Introduction to the App Service Environment][intro].</span></span>

<span data-ttu-id="0561b-110">Ten dokument zawiera listę źródło adresy IP do ASE ruch związany z zarządzaniem.</span><span class="sxs-lookup"><span data-stu-id="0561b-110">This document lists the source IPs for management traffic to the ASE.</span></span> <span data-ttu-id="0561b-111">Te adresy służy do tworzenia grup zabezpieczeń sieci, aby zablokować ruch przychodzący lub używać ich w tabele tras, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="0561b-111">You can use these addresses to create Network Security Groups to lock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="0561b-112">Aby użyć tych informacji należy użyć:</span><span class="sxs-lookup"><span data-stu-id="0561b-112">To use this information you need to use:</span></span>

* <span data-ttu-id="0561b-113">adresy IP, które są wyświetlane dla wszystkich regionów</span><span class="sxs-lookup"><span data-stu-id="0561b-113">the IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="0561b-114">adresy IP, które pasują do regionu użytkownika ASE wdrożonej do.</span><span class="sxs-lookup"><span data-stu-id="0561b-114">the IP addresses that match to the region that your ASE is deployed into.</span></span>

<span data-ttu-id="0561b-115">Przychodzący ruch związany z zarządzaniem pochodzi się z tych adresów IP w portach 454 i 455.</span><span class="sxs-lookup"><span data-stu-id="0561b-115">The incoming management traffic comes in from these IP addresses to ports 454 and 455.</span></span>

| <span data-ttu-id="0561b-116">Region</span><span class="sxs-lookup"><span data-stu-id="0561b-116">Region</span></span> | <span data-ttu-id="0561b-117">Adresy</span><span class="sxs-lookup"><span data-stu-id="0561b-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="0561b-118">Wszystkie regiony</span><span class="sxs-lookup"><span data-stu-id="0561b-118">All regions</span></span> | <span data-ttu-id="0561b-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="0561b-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="0561b-120">Południowo środkowe stany USA & Północna środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="0561b-120">South Central US & North Central US</span></span> | <span data-ttu-id="0561b-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="0561b-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="0561b-122">Południowo-Wschodnia Australia & Wschodnia Australia</span><span class="sxs-lookup"><span data-stu-id="0561b-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="0561b-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="0561b-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="0561b-124">Zachodnie stany USA & wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="0561b-124">US West & US East</span></span> | <span data-ttu-id="0561b-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="0561b-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="0561b-126">Europa Zachodnia & Europa Północna</span><span class="sxs-lookup"><span data-stu-id="0561b-126">West Europe & North Europe</span></span> | <span data-ttu-id="0561b-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="0561b-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="0561b-128">Środkowe stany USA zachodnie & zachodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="0561b-128">West Central US & West US 2</span></span> | <span data-ttu-id="0561b-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="0561b-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="0561b-130">Środkowe stany USA & wschodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="0561b-130">Central US & East US 2</span></span> | <span data-ttu-id="0561b-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="0561b-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="0561b-132">Azja Wschodnia & Azja południowo-wschodnia</span><span class="sxs-lookup"><span data-stu-id="0561b-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="0561b-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="0561b-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="0561b-134">Japonia Wschodnia & Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="0561b-134">Japan East & Japan West</span></span> | <span data-ttu-id="0561b-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="0561b-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="0561b-136">Kanada Środkowa & Kanada Wschodnia</span><span class="sxs-lookup"><span data-stu-id="0561b-136">Canada Central & Canada East</span></span> | <span data-ttu-id="0561b-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="0561b-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="0561b-138">Wielka Brytania Zachodnia & Wielka Brytania Południowa</span><span class="sxs-lookup"><span data-stu-id="0561b-138">UK West & UK South</span></span> | <span data-ttu-id="0561b-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="0561b-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="0561b-140">Centrum Korei i Południowej Korei</span><span class="sxs-lookup"><span data-stu-id="0561b-140">Korea South & Korea Central</span></span> | <span data-ttu-id="0561b-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="0561b-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="0561b-142">Brazylia Południowa & południowo środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="0561b-142">Brazil South & South Central US</span></span>| <span data-ttu-id="0561b-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="0561b-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="0561b-144">Indie środkowe & Indie Południowe</span><span class="sxs-lookup"><span data-stu-id="0561b-144">Central India & South India</span></span> | <span data-ttu-id="0561b-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="0561b-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="0561b-146">Indie Zachodnie & Indie Południowe</span><span class="sxs-lookup"><span data-stu-id="0561b-146">West India & South India</span></span> | <span data-ttu-id="0561b-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="0561b-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
