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
# <a name="app-service-environment-management-addresses"></a>Adresy zarządzania środowiska usługi aplikacji

Environment(ASE) usługi aplikacji to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet).  ASE musi być dostępny z usługi aplikacji Azure, dzięki czemu można nim zarządzać.  Ten ruch związany z zarządzaniem ASE jest przesyłany w sieci kontrolowanego przez użytkownika.  Pochodzi on z serwerów zarządzania w usłudze Azure App Service do publicznego adresu IP, który jest skojarzony z ASE.  Szczegółowe informacje na temat ASE networking zależności odczytu [sieci zagadnienia i środowiska usługi aplikacji][networking].  Ogólne informacje na temat ASE można uruchomić z [wprowadzenie do środowiska usługi aplikacji][intro].

Ten dokument zawiera listę źródło adresy IP do ASE ruch związany z zarządzaniem. Te adresy służy do tworzenia grup zabezpieczeń sieci, aby zablokować ruch przychodzący lub używać ich w tabele tras, zgodnie z potrzebami.  Aby użyć tych informacji należy użyć:

* adresy IP, które są wyświetlane dla wszystkich regionów
* adresy IP, które pasują do regionu użytkownika ASE wdrożonej do.

Przychodzący ruch związany z zarządzaniem pochodzi się z tych adresów IP w portach 454 i 455.

| Region | Adresy |
|--------|-----------|
| Wszystkie regiony | 70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141 |
| Południowo środkowe stany USA & Północna środkowe stany USA | 23.102.188.65, 191.236.154.88 |
| Południowo-Wschodnia Australia & Wschodnia Australia | 23.101.234.41, 104.210.90.65 |
| Zachodnie stany USA & wschodnie stany USA | 104.45.227.37, 191.236.60.72 |
| Europa Zachodnia & Europa Północna | 191.233.94.45, 191.237.222.191 |
| Środkowe stany USA zachodnie & zachodnie stany USA 2 | 13.78.148.75, 13.66.225.188 |
| Środkowe stany USA & wschodnie stany USA 2 | 104.43.165.73, 104.46.108.135 |
| Azja Wschodnia & Azja południowo-wschodnia | 23.99.115.5, 104.215.158.33 |
| Japonia Wschodnia & Japonia Zachodnia | 104.41.185.116, 191.239.104.48 |
| Kanada Środkowa & Kanada Wschodnia | 40.85.230.101, 40.86.229.100 |
| Wielka Brytania Zachodnia & Wielka Brytania Południowa | 51.141.8.34, 51.140.185.75 |
| Centrum Korei i Południowej Korei | 52.231.200.177, 52.231.32.117 |
| Brazylia Południowa & południowo środkowe stany USA| 104.41.46.178, 23.102.188.65 |
| Indie środkowe & Indie Południowe | 104.211.98.24, 104.211.225.66 |
| Indie Zachodnie & Indie Południowe | 104.211.160.229, 104.211.225.66 |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
