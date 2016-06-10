$this->loadModel('Sumario');
        $options['fields'] = array(
            'count(SUM_ESTADO_DESCRIPCION) AS Cantidad',
            'SUM_ESTADO_DESCRIPCION AS Estado'
            );
        $options['group'] = array('SUM_ESTADO_DESCRIPCION');

        $sumarioTmp = $this->Sumario->find('all', $options);
        print_a($sumarioTmp);
        foreach ($sumarioTmp as  $value) :
            $sumario[$value['Sumario']['Estado']] = $value['0']['Cantidad'];
        endforeach;
        print_a($sumario);
        $sumario = Set::combine($sumarioTmp, '{n}.Sumario.Estado', '{n}.0.Cantidad');
        print_a($sumario);


        $this->set(compact('sumario'));
