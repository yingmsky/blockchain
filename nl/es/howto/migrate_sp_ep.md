---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Migración de Plan inicial al Plan empresarial
{: #migrate_starter_to_enterprise}


***[¿Le resulta útil esta página? Indíquenos su opinión.](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***


El [Plan inicial](/docs/services/blockchain/starter_plan.html) de la plataforma {{site.data.keyword.blockchainfull}} le ofrece un entorno de prueba y desarrollo para ejecutar sus PoC y demos y para probar su código de encadenamiento y sus aplicaciones. Cuando esté listo para moverse a un entorno de producción, puede migrar de una red del plan inicial a una red del [Plan empresarial](/docs/services/blockchain/enterprise_plan.html).
{:shortdesc}

Las redes del Plan empresarial ofrecen las siguientes características preparadas para la producción para dar soporte a la carga de trabajo de producción:

- Redes blockchain disponibles en ubicaciones globales adicionales a las del Plan inicial.
- No hay límite de almacenamiento, que es de 20 GB en el Plan inicial.
- Gestión mejorada de CPU y RAM para garantizar que todas las redes se ejecutan sin problemas.
- Seguridad mejorada que incluye las funciones siguientes:
  - Secure Service Container (SSC) garantiza que la imagen de blockchain no se puede alterar y cargar en un momento determinado y que el código de dispositivo y los datos confidenciales, tanto activos como inactivos, están protegidos.
  - [Módulo seguro de hardware (HSM)](/docs/services/blockchain/glossary.html#hsm) para la gestión de claves y el almacenamiento de claves.
  - Cifrado de disco de uso generalizado.
- Alta disponibilidad, recuperación tras desastre, tolerancia a errores de bloqueo y actualizaciones constantes.
- Soporte avanzado opcional.

## Consideraciones
{: #migrate_starter_to_enterprise_considerations}

Antes de migrar su red del Plan inicia a una red del Plan empresarial, lea las siguientes consideraciones.

- **Precios:** el coste mensual para su organización de utilizar una red del Plan empresarial incluye 1000 $ de cuota de miembro por instancia a y 1000 $ de cuota por igual. Para obtener más información, consulte [Precios del Plan empresarial](/docs/services/blockchain/howto/pricing.html#enterprise-plan-pricing).
- **Versión de Hyperledger Fabric:** las redes del Plan empresarial se ejecutan en Hyperledger Fabric v1.1. Las redes del Plan inicial se ejecutan en Fabric v1.2. Un componente como, por ejemplo, los
[Datos privados](https://hyperledger-fabric.readthedocs.io/en/release-1.2/private-data/private-data.html) (es decir, un código de encadenamiento desarrollado para utilizar datos privados), que funciona con una red del Plan inicial, no funcionará en el Plan empresarial.
- **Recursos afectados:** código de encadenamiento (contratos inteligentes), definiciones de red de negocio, aplicaciones cliente. De nuevo, tenga en cuenta si el código de encadenamiento hace uso de un componente de Fabric v1.2 o de una función que no es compatible con las redes v1.1.
- **Tiempo necesario: ** tardará al menos medio día en migrar una red básica del Plan inicial a un Plan empresarial.
- Los **datos existentes del libro mayor** no se pueden pasar de redes del Plan inicial a redes del Plan empresarial porque no resulta adecuado que los datos de prueba existan en un entorno de producción.

**Nota:** una red *básica* incluye dos organizaciones con dos iguales, un solo canal y un solo código de encadenamiento o archivo Business Network Archive (`.bna`). El tiempo real para migrar puede variar en función del tamaño y de la complejidad de los componentes de red que necesite en la red del Plan empresarial.

## Lista de comprobación de la migración
{: #migrate_starter_to_enterprise_checklist}

Hay una serie de tareas necesarias para prepararse para pasar a una red del Plan empresarial desde una red del Plan inicial. Encontrará instrucciones detalladas en secciones posteriores, pero aquí hay un resumen:

- Crear una red del Plan empresarial.
- Si ha desarrollado un archivo `.bna` mediante Hyperledger Composer, localizar y migrar el archivo `.bna`.
- Volver a crear la configuración deseada de las organizaciones e iguales desde la red del Plan inicial de prueba.
- Identifique qué código de encadenamiento, escrito en Go o Node, que se ejecutará en la red del Plan empresarial.
- Actualizar las aplicaciones de cliente con la información de punto final de API nueva para la red del Plan empresarial.

### Crear una red del Plan empresarial
{: #migrate_starter_to_enterprise_create_network}

Debe crear una red del Plan empresarial antes de migrar. Para obtener más información, consulte [Creación de una red del Plan empresarial](/docs/services/blockchain/get_start.html#creating-a-network).

### Migrar un archivo `.bna`
{: #migrate_starter_to_enterprise_bna}

**Nota:** puede omitir este paso si no utiliza un archivo `.bna` en la red del Plan inicial.

Si ha utilizado Hyperledger Composer para definir una red de negocio y ha desplegado un archivo `.bna` en la red del Plan inicial, puede desplegar el mismo archivo `.bna` en la red del Plan empresarial.

- Si tiene un archivo de archivado de red empresarial (`.bna`), siga las instrucciones del apartado sobre [Desarrollo de una red empresarial en el Plan empresarial](/docs/services/blockchain/develop_enterprise.html).
- Si no dispone de un archivo `.bna`, utilice el mandato `composer network download` para recuperarlo de la instancia del Plan inicial. Para obtener más información sobre el mandato `composer network download`, consulte la [documentación de línea de mandatos de Hyperledger Composer ![Icono de enlace externo](../images/external_link.svg "Icono de enlace externo")](https://hyperledger.github.io/composer/latest/reference/commands){:new_window}. Luego puede seguir las instrucciones del apartado [Despliegue de una red empresarial en un Plan empresarial](/docs/services/blockchain/develop_enterprise.html).

### Volver a crear la configuración de red
{: #migrate_starter_to_enterprise_config_network}

Puede volver a crear la configuración de las organizaciones (miembros), canales e iguales de la red del Plan inicial en la red del Plan empresarial. Puede utilizar la interfaz de usuario del supervisor de red para volver a crear estos recursos de red invitando a las organizaciones adecuadas (tenga en cuenta que no podrá **cambiar** las organizaciones como en el Plan inicial), crear canales y crear iguales (de nuevo, las organizaciones invitadas tendrán que crear sus propios iguales).

1. Inicie una sesión en la red del Plan empresarial en {{site.data.keyword.cloud_notm}} y entre en el supervisor de red.
2. Vuelva a crear las organizaciones (miembros) en la pantalla "Miembros", vuelva a crear los canales en la pantalla "Canales" y vuelva a crear los pares en la pantalla "Visión general". Para obtener más información sobre la creación de recursos de red, consulte
[Utilización del supervisor de red](/docs/services/blockchain/v10_dashboard.html#overview).
3. Configure los canales añadiendo miembros y estableciendo políticas de canal de la misma manera que en la red del Plan inicial.

**Nota:** para conseguir alta disponibilidad, debe crear al menos dos iguales para su organización, unirlos al mismo canal y codificar las aplicaciones de cliente correctamente para pasar de un igual al otro cuando sea necesario.

### Migrar código de encadenamiento
{: #migrate_starter_to_enterprise_cc}

El código de encadenamiento se desarrolla externamente en el entorno local y se invoca mediante las aplicaciones cliente. Para instalar y crear una instancia de código de encadenamiento, que se ha probado en la red del Plan inicial, en los iguales seleccionados de la red del Plan empresarial siga las instrucciones del apartado sobre [Instalación, creación de instancias y actualización de un código de encadenamiento](/docs/services/blockchain/howto/install_instantiate_chaincode.html#installchaincode).

### Actualizar aplicaciones cliente
{: #migrate_starter_to_enterprise_app}

Es necesario actualizar las aplicaciones cliente existentes, que se prueban en la red del Plan inicial, con la información de punto final de la API para la red del Plan empresarial. Para obtener más información, consulte [Recuperación de credenciales de red y del perfil de conexión](/docs/services/blockchain/get_start.html#retrieving-network-credentials-and-connection-profile).

Con respecto a la alta disponibilidad, es responsabilidad de las aplicaciones cliente detectar cuándo un igual no está respondiendo y direccionar las transacciones a otro igual.

## Qué hacer con las redes existentes del Plan inicial
{: #migrate_starter_to_enterprise_existing_network}

Puede seguir utilizando la red del Plan inicial como entorno de recinto de pruebas para incubar nuevos proyectos y probar cambios en el código de encadenamiento existente. Además, puede mantener en la red del Plan inicial los datos del libro mayor de prueba, que no se migran a la red del Plan empresarial.

No suprima la red del Plan inicial hasta que haya completado todas las pruebas y haya verificado que todo funciona correctamente. Sin embargo, cuando ya no necesite la red del Plan inicial ni los datos del libro mayor que contiene, puede suprimir la red de forma segura. Para obtener más información, consulte [Supresión o abandono de una red](/docs/services/blockchain/get_start_starter_plan.html#deleting-or-leaving-a-network).
