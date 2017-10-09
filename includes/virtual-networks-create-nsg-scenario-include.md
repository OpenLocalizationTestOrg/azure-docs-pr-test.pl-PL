## <a name="scenario"></a>Scenariusz
toobetter pokazują, jak toocreate grup NSG, ten dokument użyje scenariusz hello poniżej.

![Scenariusz sieci wirtualnych](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

W tym scenariuszu utworzysz grupy NSG dla każdej podsieci w hello **TestVNet** sieci wirtualnej, zgodnie z opisem poniżej: 

* **Grupa NSG frontonu**. Hello frontonu NSG zostaną zastosowane toohello *frontonu* podsieci i zawiera dwie reguły:    
  * **Reguła RDP**. Ta reguła umożliwia toohello ruch RDP *frontonu* podsieci.
  * **Reguła sieci Web**. Ta reguła umożliwia toohello ruch HTTP *frontonu* podsieci.
* **Grupa NSG zaplecza**. Hello wewnętrzna grupa NSG zostaną zastosowane toohello *zaplecza* podsieci i zawiera dwie reguły:    
  * **Reguła SQL**. Ta reguła zezwala na ruch SQL tylko z hello *frontonu* podsieci.
  * **Reguła sieci Web**. Ta reguła nie zezwala na wszystkie internet powiązany ruch z hello *zaplecza* podsieci.

Hello kombinacji tych zasad utworzyć DMZ podobny scenariusz, gdzie podsieci wewnętrznej hello może odbierać ruchu przychodzącego dla serwera SQL z podsieci frontonu hello i ma toohello nie dostępu do Internetu, gdy podsieci frontonu hello może komunikować się z hello Internet, oraz odbieranie przychodzących żądań HTTP.

