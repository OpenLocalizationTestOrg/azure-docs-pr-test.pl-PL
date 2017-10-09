## <a name="scenario"></a>Scenariusz
Ten dokument przeprowadzi wdrożenia korzystającego z wielu kart sieciowych w maszynach wirtualnych w danego scenariusza. W tym scenariuszu należy obciążenia IaaS dwuwarstwowej hostowana na platformie Azure. Każda warstwa została wdrożona w jego własnej podsieci w sieci wirtualnej (VNet). warstwy frontonu Hello składa się z kilku serwerów sieci web, zgrupowane w ustawić wysoką dostępność usługi równoważenia obciążenia. Warstwa zaplecza Hello składa się z kilku serwerów baz danych. Te serwery baz danych zostanie wdrożona w dwie karty sieciowe, jeden dla dostępu do bazy danych, hello innych dla zarządzania. Witaj scenariusz obejmuje również toocontrol grup zabezpieczeń sieci (NSG) jest dozwolone w jaki ruch we wdrożeniu hello tooeach podsieci i karty Sieciowej. na poniższym rysunku Hello przedstawiono hello podstawowej architektury tego scenariusza.  

![Scenariusz MultiNIC](./media/virtual-network-deploy-multinic-scenario-include/Figure1.png)

