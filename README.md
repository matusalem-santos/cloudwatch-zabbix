# Objetivo

Monitorar os serviços da AWS pelo Zabbix consultando a API do cloudwatch

# Dependencias 

- Python 3.6 ou maior
- Pip3
- boto3 (Executar: **pip3 install boto3**)

# Como utilizar 

- Criar uma role com permissão de leitura ao Cloudwatch e atachar na maquina do Zabbix ou criar um usuario no IAM com permissão de leitura ao Cloudwatch e passar a acsess_key e o secret_key como paramêtro do script
- Enviar o script [cloudwatch-zabbix.py](cloudwatch-zabbix.py) para a maquina do Zabbix no caminho: **/usr/lib/zabbix/externalscripts**
- Dar permissão de execução no script **cloudwatch-zabbix.py**
```bash
    sudo chmod +x /usr/lib/zabbix/externalscripts/cloudwatch-zabbix.py
``` 

#### Execução

- Executar o script **cloudwatch-zabbix.py** passando os parâmetros usando role na maquina:
```bash
    /usr/lib/zabbix/externalscripts/cloudwatch-zabbix.py MetricName Function DimensionName,DimensionNames DimensionValue,DimensionValues nameSpace Region [period, default=5]
``` 
- Exemplo: 
```bash
    /usr/lib/zabbix/externalscripts/cloudwatch-zabbix.py CPUUtilization Average InstanceID i-09e5c692fa334da13 AWS/EC2 us-east-1 10
``` 
- Executar o script **cloudwatch-zabbix.py** passando os parâmetros usando credenciais do IAM:
```bash
    /usr/lib/zabbix/externalscripts/cloudwatch-zabbix.py MetricName Function DimensionName,DimensionNames DimensionValue,DimensionValues nameSpace Region AccessKey SecretKey [period, default=5]
``` 
- Exemplo: 
```bash
    /usr/lib/zabbix/externalscripts/cloudwatch-zabbix.py CPUUtilization Average InstanceID i-09e5c692fa334da13 AWS/EC2 us-east-1 AccessKey SecretKey 10
``` 
- Criar item no Zabbix com o tipo **External check** passando como key o script e seus paramêtros:

 <img src="http://i.imgur.com/gZwV6LB.png"
     alt="Markdown Monster icon"
     style="float: left; margin-right: 10px;" />