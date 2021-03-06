PHP-Web-Service
===============

Php-NuSoap web service oluşturma için wsdl yapmak ve aynı web servise parametre gönderip ilgili işlemleri yaptırabiliriz.

Service.php içerisinde sizde ilgili değişiklikleri yaparak kendize göre uyarlayabilirsiniz.

Wsdl için
```
http://localhost/service.php?wsdl
```

Bilgiler için ve  web servis içerisindeki fonksiyonları görebilirsiniz.
```
http://localhost/service.php
``` 

Bu web servisin deneme için tek methodu var

```
ReceiveOrderResult

```


```php

$server->wsdl->addComplexType(
    'CReceiveOrderResultInput',
    'complexType',
    'struct',
    'sequence',
    '',
    array(
        'OrderObjectId' => array('name'=>'OrderObjectId','type'=>'xsd:string'),
        'GSM'		=> array('name'=>'GSM','type'=>'xsd:string', 'minOccurs'=>0),
	'MPAY'		=> array('name'=>'MPAY','type'=>'xsd:string' ,'minOccurs'=>0),
        'SMSContent'	=> array('name'=>'SMSContent','type'=>'xsd:string','minOccurs'=>0),
	'TotalPrice'	=> array('name'=>'TotalPrice','type'=>'xsd:double'),
	'TotalUnitPrice'=> array('name'=>'TotalUnitPrice','type'=>'xsd:double'),
	'State'		=> array('name'=>'State','type'=>'xsd:int'),
	'StatusCode'	=> array('name'=>'StatusCode','type'=>'xsd:int'),
	'ErrorCode'	=> array('name'=>'ErrorCode','type'=>'xsd:string' ,'minOccurs'=>0),
	'ErrorMessage'	=> array('name'=>'ErrorMessage','type'=>'xsd:string' ,'minOccurs'=>0),
	'PaymentDateTime'=> array('name'=>'PaymentDateTime','type'=>'xsd:dateTime'),
	'GsmOperator'	=> array('name'=>'GsmOperator','type'=>'xsd:int'),
	'GsmType'	=> array('name'=>'GsmType','type'=>'xsd:int'),
	'SubscriberId'	=> array('name'=>'SubscriberId','type'=>'xsd:string'),
	'Products'	=> array('name'=>'Products','type'=>'tns:ArrayOfCSaleProduct','minOccurs'=>0),
	'OrderChannelId'=> array('name'=>'OrderChannelId','type'=>'xsd:int'),
	'PaymentTypeId'	=> array('name'=>'PaymentTypeId','type'=>'xsd:int'),	
	'PaymentCategoryId'=> array('name'=>'PaymentCategoryId','type'=>'xsd:int'),	
	'Pin'		=> array('name'=>'Pin','type'=>'xsd:string' ,'minOccurs'=>0),	
    )
);


$server->wsdl->addComplexType(
    'ArrayOfCSaleProduct',  // Name
    'complexType',    // Type Class
    'array',          // PHP Type
    'sequence',               // Compositor
    '', // Restricted Base
    array(
	'CSaleProduct'=>array('name'=>'CSaleProduct', 'type'=>'tns:CSaleProduct','minOccurs'=>"0", 'maxOccurs'=>"unbounded" )
    )    
); 


$server->wsdl->addComplexType(
    'CSaleProduct',  // Name
    'complexType',    // Type Class
    'array',          // PHP Type
    'sequence',               // Compositor
    '', // Restricted Base
    array(
	'ProductId'=>array('name'=>'ProductId', 'type'=>'xsd:int','minOccurs'=>"0", 'maxOccurs'=>"1" ),
	'ProductCategory'=>array('name'=>'ProductCategory', 'type'=>'xsd:int','minOccurs'=>"0", 'maxOccurs'=>"1" ),
	'ProductDescription'=>array('name'=>'ProductDescription', 'type'=>'xsd:string','minOccurs'=>"0", 'maxOccurs'=>"1" ),
	'BasePrice'=>array('name'=>'BasePrice', 'type'=>'xsd:double','minOccurs'=>"0", 'maxOccurs'=>"1" ),
	'BaseUnitPrice'=>array('name'=>'BaseUnitPrice', 'type'=>'xsd:double','minOccurs'=>"0", 'maxOccurs'=>"1" ),
	'Unit'=>array('name'=>'Unit', 'type'=>'xsd:int','minOccurs'=>"0", 'maxOccurs'=>"1" ),
    )    
);  

$server->wsdl->addComplexType( 
   'CReceiveOrderResultOutput', 
   'complexType', 
   'struct', 
   'sequence', 
   '', 
   array( 
       'StatusCode' => array('name' => 'StatusCode', 'type' => 'xsd:int'),
       'ErrorCode' => array('name' => 'ErrorCode', 'type' => 'xsd:string'),
       'ErrorMessage' => array('name' => 'ErrorMessage', 'type' => 'xsd:string')
    ) 
); 

$server->register( 
   'ReceiveOrderResult', 
   array('ReceiveOrderResult' => 'tns:CReceiveOrderResultInput'), 
   array('ReceiveOrderResultResponse' => 'tns:CReceiveOrderResultOutput'), 
   false,
   false,
   "rpc",
   "literal",
   "return web service"
);


```



