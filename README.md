# Suite-mCommerce-iOS Objective-C

## Requerimientos
La Suite mCommerce es compatible con apps para iOS 7.0 o superior.

## Integración

### Primeros pasos
1. Descargar el framework de esta plataforma.
2. Ponerse en contacto con nosotros para solicitar datos de prueba.

### Añadir el framework a tu proyecto
1. Crear un proyecto en Xcode en lenguaje Objective-C.
2. En la sección General en el apartado Embebed Binaries añadir el framework previamente descargado.

###Guia de Integración

#### Inicialización Controlador

Para inicializar un objeto SuiteController se utiliza el método: 

`- (id) initOnEnvironment:(Environment) environment
    currentViewController:(UIViewController *) viewController
                 delegate:(id<SuiteControllerDelegate>) delegate;`

Donde:
* **environment** es un enum correspondiente a un ambiente (SANDBOX, DEV, QA, PROD)
* **viewController** es el ViewController actual desde el cual se lanzarán las peticiones.
* **delegate** es la interfaz implementada con la cual se comunicará el controlador.


El activity o contexto que necesite alguno de los servicios deberá implementar la _interfaz_ `SuiteControllerDelegate`.

En caso de que alguno de estos parámetros estén incorrectos, se regresará un error:

* **C001**	Compañía invalida
* **C002**	Ambiente invalido
* **C003**	Contexto invalido
* **S001**	Error de conexión
* **S002**	Excepción de llave


### Autenticación

Para invocar el servicio de autenticación

`- (void) AuthenticateWithBeanTokenization:(BeanTokenization*) beanTokenization
                                  bean3DS:(Bean3DS*) bean3DS;`

Donde `beeanTokenization` tiene los siguientes atributos:

* **branch** es la sucursal de la empresa
* **company** es el ID de la compañía de CDP
* **country** es el código de pais
* **user** es usuario de CDP.
* **password** es la contraseña asociada al usuario CDP.
* **merchant** es la afiliación
* **currency** es un enum que corresponde al tipo de moneda (MXN, USD)
* **operationType** es el número de operativa para realizar el cobro.
* **reference** es la referencia con la cual se realizará el cobro.



Donde `bean3DS` tiene los siguientes atributos:

* **company** es el ID de la compañía de CDP
* **branch**: es la sucursal de la empresa
* **country**: es el código de pais
* **user**: es usuario de CDP.
* **password**: es la contraseña asociada al usuario CDP.
* **merchant**: es la afiliación
* **currency**: es un enum que corresponde al tipo de moneda (MXN, USD)
* **authKey**: es la llave para procesar la autenticación proporcionada al comercio
* **reference**: es la referencia con la cual se autenticará.
**(NOTA: Estos datos le serán proporcionados por MIT)**


Ejecutará una vista donde se capturarán los datos del tarjetahabiente. 


El delegado que responde a esta función es `-(void)didFinishAuthenticationProcess:(BeanTokenizeResponse*) tokenizeResponse error:(SuiteError*) error;`


Donde en caso de que el proceso sea exitoso la información de token vendrá en el `beanTokenizeResponse` y el objeto `suiteError` vendrá nulo. El bean tiene los siguientes atributos:

* **token**: Token
* **nbResponse**: Success o error
* **tokenReference**: Referencia de token

Caso contrario la descripción de porque no se realizó la autenticación vendrá en el objeto `suiteError`

* **A001**	Branch invalido
* **A002**	Country ainvalido
* **A003**	Usuario invalido
* **A004**	Contraseña invalida
* **A005**	Merchant invalido
* **A006**	Moneda invalida
* **A007**	Llave invalida
* **A008**	Parámetros inválidos
* **A009**	Compañía invalida
* **A010**	Autenticación fallida

### Cobro con Token

Para invocar el servicio de cobro

`- (void) sndPayWithTokenWithBeanTokenization:(BeanTokenization*) beanTokenization
                                     bean3DS:(Bean3DS*) bean3DS;`

Donde `beeanTokenization` tiene los siguientes atributos:

* **branch** es la sucursal de la empresa
* **company** es el ID de la compañía de CDP
* **country** es el código de pais
* **user** es usuario de CDP.
* **password** es la contraseña asociada al usuario CDP.
* **merchant** es la afiliación
* **currency** es un enum que corresponde al tipo de moneda (MXN, USD)
* **operationType** es el número de operativa para realizar el cobro.
* **token** es el token asociado a una tarjeta
* **reference** es la referencia con la cual se realizará el cobro.
* **amount** es el monto por el cual se realizará el cobro.
* **(NOTA: Estos datos le serán proporcionados por MIT)**

Y donde `bean3DS` tiene los siguientes atributos:

* **branch** es la sucursal de la empresa
* **company** es el ID de la compañía de CDP
* **country** es el código de pais
* **user** es usuario de CDP.
* **password** es la contraseña asociada al usuario CDP.
* **merchant** es la afiliación
* **currency** es un enum que corresponde al tipo de moneda (MXN, USD)
* **authKey** es la llave para procesar la autenticación proporcionada al comercio
* **reference** es la referencia con la cual se autenticará.
* **(NOTA: Estos datos le serán proporcionados por MIT)**

El delegado que responde a esta función es `-(void)didFinishTokenizeTransantion:(BeanPaymentWithToken*) beanPaymentWithToken error:(SuiteError*) error`

Donde en caso de que el proceso sea exitoso la información del cobro vendrá en el `beanPaymentWithToken` y el objeto `suiteError` vendrá nulo. El bean tiene los siguientes atributos:

* **Reference**: Referencia del cobro
* **Response**: approved/denied/error
* **Auth**: Numero de autorización de cobro
* **Folio**: Folio de la transacción
* **Amount**: Monto de la transacción
* **Date**: Fecha de la transacción
* **Error**: Descripción en caso de que la transacción haya sido denegada o errónea

En caso de que haya un error, el objeto `beanPaymentWithToken` vendrá nulo y el objeto `suiteError` tendrá la información asociada al error.

* **T001**	Branch invalido
* **T002**	Usuario invalido
* **T003**	Contraseña invalida
* **T004**	Tarjeta invalida
* **T005**	País invalido 
* **T006**	Merchant invalido
* **T007**	Referencia invalida
* **T008**	Tipo de operación invalida
* **T009**	Token invalido
* **T010**	Monto invalido
* **T011**	Moneda invalida
* **T012**	Parámetros inválidos
* **T013**	La tarjeta proporcionada no corresponde con el token
* **T014**	Compañía invalida



### Contacto Mesa de Ayuda MIT
Para la atención de los requerimientos de soporte, contamos con mesa de ayuda con los siguientes números en ciudad de México para resolver dudas y orientación para explotar eficientemente los recursos de nuestra plataforma.

Teléfono en la ciudad de México 
**(01.55) 1500.9000**

Correo electrónico 
**soporte.centrodepagos@mitec.com.mx**
